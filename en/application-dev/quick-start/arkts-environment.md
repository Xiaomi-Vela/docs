# Environment: Device Environment Query


You may want your application to behave differently based on the device environment where the application is running, for example, switching to dark mode or a specific language. In this case, you need Environment for device environment query.


Environment is a singleton object created by the ArkUI framework at application start. It provides a range of application state attributes to AppStorage that describe the device environment in which the application is running. Environment and its attributes are immutable. All property values are of simple type only.


## Application Scenarios


### Accessing Environment Parameters from UI

- Use **Environment.envProp** to save the environment variables of the device to AppStorage.

  ```ts
  // Save languageCode to AppStorage. The default value is en.
  Environment.envProp('languageCode', 'en');
  ```

- Decorate the variables with \@StorageProp to link them with components.

  ```ts
  @StorageProp('languageCode') lang : string = 'en';
  ```

The chain of updates is as follows: Environment > AppStorage > Component.

> **NOTE**
>
> An \@StorageProp decorated variable can be locally modified, but the change will not be updated to AppStorage. This is because the environment variable parameters are read-only to the application.


```ts
// Save the device language code to AppStorage.
Environment.envProp('languageCode', 'en');
let enable: undefined = AppStorage.get<undefined>('languageCode');

@Entry
@Component
struct Index {
  @StorageProp('languageCode') languageCode: string = 'en';

  build() {
    Row() {
      Column() {
        // Output the current device language code.
        Text(this.languageCode)
      }
    }
  }
}
```


### Using Environment in Application Logic


```ts
// Use Environment.EnvProp to save the device language code to AppStorage.
Environment.envProp('languageCode', 'en');
// Obtain the one-way bound languageCode variable from AppStorage.
const lang: SubscribedAbstractProperty<string> = AppStorage.prop('languageCode');

if (lang.get() === 'en') {
  console.info('Hi');
} else {
  console.info('Hello!');
}
```


## Restrictions


Environment can be called only when the [UIContext](../reference/apis/js-apis-arkui-UIContext.md#uicontext), which can be obtained through [runScopedTask](../reference/apis/js-apis-arkui-UIContext.md#runscopedtask), is specified. If Environment is called otherwise, no device environment data can be obtained.


```ts
// EntryAbility.ts
import UIAbility from '@ohos.app.ability.UIAbility';
import window from '@ohos.window';

export default class EntryAbility extends UIAbility {
  onWindowStageCreate(windowStage: window.WindowStage) {
    windowStage.loadContent('pages/Index');
    let window = windowStage.getMainWindow()
    window.then(window => {
      let uicontext = window.getUIContext()
      uicontext.runScopedTask(() => {
        Environment.envProp('languageCode', 'en');
      })
    })
  }
}
```
