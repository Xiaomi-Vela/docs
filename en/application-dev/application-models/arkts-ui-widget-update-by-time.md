# Configuring a Widget to Update Periodically

The widget framework provides the following modes of updating widgets periodically:


- Setting the update interval: The widget will be updated at the specified interval by calling [onUpdateForm](../reference/apis/js-apis-app-form-formExtensionAbility.md#onupdateform). You can specify the interval by setting the [updateDuration](arkts-ui-widget-configuration.md) field in the **form_config.json** file. For example, you can configure the widget to update once an hour.

  > **NOTE**
  >
  > Before configuring a widget to update periodically, enable the periodic update feature by setting the **updateEnabled** field to **true** in the **form_config.json** file.
  >
  > **updateDuration** takes precedence over **scheduledUpdateTime**. If both are specified, the value specified by **updateDuration** is used.

  ```json
  {
    "forms": [
      {
        "name": "widget",
        "description": "This is a service widget.",
        "src": "./ets/widget/pages/WidgetCard.ets",
        "uiSyntax": "arkts",
        "window": {
          "designWidth": 720,
          "autoDesignWidth": true
        },
        "colorMode": "auto",
        "isDefault": true,
        "updateEnabled": true,
        "scheduledUpdateTime": "10:30",
        "updateDuration": 2,
        "defaultDimension": "2*2",
        "supportDimensions": ["2*2"]
      }
    ]
  }
  ```

- Setting the scheduled update time: The widget will be updated at the scheduled time every day. You can specify the time by setting the [scheduledUpdateTime](arkts-ui-widget-configuration.md) field in the **form_config.json** file. For example, you can configure the widget to update at 10:30 a.m. every day.

  > **NOTE**
  >
  > **updateDuration** takes precedence over **scheduledUpdateTime**. For the **scheduledUpdateTime** settings to take effect, set **updateDuration** to **0**.


  ```json
  {
    "forms": [
      {
        "name": "widget",
        "description": "This is a service widget.",
        "src": "./ets/widget/pages/WidgetCard.ets",
        "uiSyntax": "arkts",
        "window": {
          "designWidth": 720,
          "autoDesignWidth": true
        },
        "colorMode": "auto",
        "isDefault": true,
        "updateEnabled": true,
        "scheduledUpdateTime": "10:30",
        "updateDuration": 0,
        "defaultDimension": "2*2",
        "supportDimensions": ["2*2"]
      }
    ]
  }
  ```

- Setting the next update time: The widget will be updated next time at the specified time. You can specify the time by calling the [setFormNextRefreshTime()](../reference/apis/js-apis-app-form-formProvider.md#setformnextrefreshtime) API. The minimum update interval is 5 minutes. For example, you can configure the widget to update within 5 minutes after the API is called.

  ```ts
  import formProvider from '@ohos.app.form.formProvider';
  import Base from '@ohos.base';

  let formId: string = '123456789'; // Use the actual widget ID in real-world scenarios.
  try {
    // Configure the widget to update in 5 minutes.
    formProvider.setFormNextRefreshTime(formId, 5, (err: Base.BusinessError) => {
      if (err) {
        console.error(`Failed to setFormNextRefreshTime. Code: ${err.code}, message: ${err.message}`);
        return;
      } else {
        console.info('Succeeded in setFormNextRefreshTimeing.');
      }
    });
  } catch (err) {
    console.error(`Failed to setFormNextRefreshTime. Code: ${(err as Base.BusinessError).code}, message: ${(err as Base.BusinessError).message}`);
  }
  ```


When periodic update is triggered, the system calls the [onUpdateForm()](../reference/apis/js-apis-app-form-formExtensionAbility.md#onupdateform) lifecycle callback of the FormExtensionAbility. In the callback, [updateForm()](../reference/apis/js-apis-app-form-formProvider.md#updateform) can be used to update the widget. For details about how to use **onUpdateForm()**, see [Updating Widget Content Through FormExtensionAbility](arkts-ui-widget-event-formextensionability.md).


> **NOTE**
> - Each widget can be updated at the specified interval for a maximum of 50 times every day, including updates triggered by setting [updateDuration](arkts-ui-widget-configuration.md) or calling [setFormNextRefreshTime()](../reference/apis/js-apis-app-form-formProvider.md#setformnextrefreshtime). When the limit is reached, the widget cannot be updated in this mode again. The number of update times is reset at 00:00 every day.
>- A single timer is used for timing updates at the specified interval. Therefore, if a widget is configured to update at scheduled intervals, the first scheduled update may have a maximum deviation of 30 minutes. For example, if widget A (updated every half an hour) is added at 03:20 and widget B (also updated every half an hour) is added at 03:40, the first update of widget B has a deviation of 10 minutes to the expected time: The timer starts at 03:20 when widget A is added, triggers an update for widget A at 03:50, and triggers another update for widget B at 04:20 (instead of 04:10 as expected).
> - Updates at the specified interval and updates at the scheduled time are triggered only when the screen is on. The update action is merely recorded when the screen is off and is performed once the screen is on.
>- If the [update-through-proxy](./arkts-ui-widget-update-by-proxy.md) feature is enabled, the settings for the update interval and next update time will not take effect.
