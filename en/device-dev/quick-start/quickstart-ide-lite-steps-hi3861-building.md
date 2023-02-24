# Building
> ![icon-note.gif](public_sys-resources/icon-note.gif) **NOTE**
> 
> In this document, the DevEco Device Tool 3.0 Release version is used as an example. The UI and usage of DevEco Device Tool vary by version. If you are using the latest version of DevEco Device Tool, perform instructions in [Building Source Code](https://gitee.com/openharmony/docs/blob/master/en/device-dev/quick-start/quickstart-ide-3861-build.md).

1. In **Projects**, click **Settings**. The Hi3861 configuration page is displayed.

   ![en-us_image_0000001265785209](figures/en-us_image_0000001265785209.png)

2. On the **toolchain** tab page, DevEco Device Tool automatically checks whether the dependent compilation toolchain is complete. If a message is displayed indicating that some tools are missing, click **SetUp** to automatically install the required tools.

   > ![icon-note.gif](public_sys-resources/icon-note.gif) **NOTE**
   >
   > If the pip component fails to be installed, [change the Python](https://device.harmonyos.com/en/docs/documentation/guide/ide-set-python-source-0000001227639986) source and try again.

   ![en-us_image_0000001221025048](figures/en-us_image_0000001221025048.png)

   After the toolchain is automatically installed, the figure below is displayed.

   ![en-us_image_0000001221344980](figures/en-us_image_0000001221344980.png)

3. On the **hi3861** tab page, set **build_type**. The default value is **debug**. Click **Save** to save the settings.

   ![en-us_image_0000001265945173](figures/en-us_image_0000001265945173.png)

4. Choose **PROJECT TASKS** > **hi3861** > **Build** to start building.

   ![en-us_image_0000001265505181](figures/en-us_image_0000001265505181.png)

5. Wait until **SUCCESS** is displayed in the **TERMINAL** window, indicating that the compilation is complete.

   ![en-us_image_0000001265665157](figures/en-us_image_0000001265665157.png)

   After the building is complete, go to the out directory of the project to view the generated files, which are needed in [burning](https://device.harmonyos.com/en/docs/documentation/guide/ide-hi3861-upload-0000001051668683).
