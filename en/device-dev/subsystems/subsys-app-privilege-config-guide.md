# Application Privilege Configuration

Application privileges are high-level capabilities of an application, for example, restricting an application from being uninstalled or restricting application data from being deleted.

OpenHarmony provides both general and device-specific application privileges. The latter can be configured by device vendors for applications on different devices. The privileges configured in the **install_list_capability.json** file take precedence over the privileges configured in the signature certificate.

> **NOTE**
> - To avoid user dissatisfaction or even infringement, do not abuse application privileges.
> - The method of changing the application's APL in its profile applies only to the applications or services in debug mode. For a commercial application, apply for a release certificate and profile in the corresponding application market.

## General Application Privileges

### Introduction

General application privileges are privileges available to applications on all types of devices. The general application privileges include the following:

| Privilege| Description                                                      |
| ---------------- | ------------------------------------------------------------ |
| AllowAppDataNotCleared | Allows application data not to be deleted.|
| AllowAppDesktopIconHide | Allows the application icon to be hidden from the home screen.|
| AllowAbilityPriorityQueried | Allows an ability to configure and query the priority.   |
| AllowAbilityExcludeFromMissions | Allows an ability to be hidden in the mission stack.|
| AllowAppShareLibrary | Allows an application to provide the inter-application HSP capability for other applications.|
| AllowMissionNotCleared | Allows an ability not to be cleared from the task list.|

### How to Configure

1. Add the **app-privilege-capabilities** field to the [**HarmonyAppProvision** file](../../application-dev/security/app-provision-structure.md) to configure general privilege capabilities as required.
2. Use the hapsigner tool to sign the [**HarmonyAppProvision** file](../../application-dev/security/app-provision-structure.md) to generate a .p7b file.
3. Use the .p7b file to sign the HAP.

Reference: [hapsigner](https://gitee.com/openharmony/developtools_hapsigner#README.md)

### Example

```json
{
    "version-name": "1.0.0",
    ...
    "bundle-info": {
        "developer-id": "OpenHarmony",
        ...
    },
    "issuer": "pki_internal",
    "app-privilege-capabilities": ["AllowAppDataNotCleared", "AllowAppDesktopIconHide"] // The application data cannot be deleted, and the application icon can be hidden on the home screen.
}
```

## Device-specific Application Privileges

### Introduction

In addition to general application privileges, device vendors can define device-specific privileges for an application. The table below describes the device-specific privileges.

| Privilege                 | Type    | Default Value| Description                                             |
| --------------------- | -------- | ------ | ------------------------------------------------- |
| removable             | bool     | true   | Allows an application to be uninstalled. This privilege takes effect only for preset applications.              |
| keepAlive             | bool     | false  | Allows an application to keep running in the background.                                |
| singleton             | bool     | false  | Allows an application to be installed for a single user (User 0).                  |
| allowCommonEvent      | string[] | -      | Allows an application to be started by a static broadcast.                            |
| associatedWakeUp      | bool     | false  | Allows an application in the FA model to be woken up by an associated application.                    |
| runningResourcesApply | bool     | false  | Allows an application to request running resources, such as the CPU, event notifications, and Bluetooth.|
| allowAppDataNotCleared | bool | false|Allows application data not to be deleted.|
| allowAppMultiProcess | bool | false| Allows an application to run on multiple processes.|
| allowAppDesktopIconHide | bool | false| Allows the application icon to be hidden from the home screen.|
| allowAbilityPriorityQueried | bool | false| Allows an ability to configure and query the priority.   |
| allowAbilityExcludeFromMissions | bool | false| Allows an ability to be hidden in the mission stack.|
| allowAppUsePrivilegeExtension | bool | false|Allows an application to use ServiceExtension and DataExtension abilities.|
| allowFormVisibleNotify | bool | false| Allows a widget to be visible on the home screen.|
| allowAppShareLibrary | bool | false | Allows an application to provide the inter-application HSP capability for other applications.|
| allowMissionNotCleared | bool | false | Allows an ability not to be cleared from the task list.|

### How to Configure

Configure the required privileges in the [configuration file](https://gitee.com/openharmony/vendor_hihope/tree/master/rk3568/preinstall-config).

### Example

#### Configuration in install_list_capability.json

```json
{
    "install_list": [
        {
            "bundleName": "com.example.kikakeyboard",
            "singleton": true, // The application is installed for a single user.
            "keepAlive": true, // The application can be running in the background.
            "runningResourcesApply": true, // The application can apply for running resources such as the CPU, event notifications, and Bluetooth.
            "associatedWakeUp": true, // The application in the FA model can be woken up by an associated application.
            "app_signature": ["****"], // The setting takes effect only when the configured certificate fingerprint is the same as the HAP certificate fingerprint.
            "allowCommonEvent": ["usual.event.SCREEN_ON", "usual.event.THERMAL_LEVEL_CHANGED"]
            "allowAppDataNotCleared": true, // The application data cannot be deleted.
            "allowAppMultiProcess": true, // Allow the application to run on multiple processes.
            "allowAppDesktopIconHide": true, // Allow the application icon to be hidden from the home screen.
            "allowAbilityPriorityQueried": true, // Allow the ability to configure the query priority.
            "allowAbilityExcludeFromMissions": true, // Allow the ability to be hidden in the mission stack.
            "allowAppUsePrivilegeExtension": true, // Allow the application to use ServiceExtension and DataExtension abilities.
            "allowFormVisibleNotify": true // Allow a widget to be visible on the home screen.
            "allowAppShareLibrary": true // Allow the application to provide the inter-application HSP capability.
            "allowMissionNotCleared": true // Allow an ability not to be cleared from the task list.
        },
}
```

**Obtaining the Certificate Fingerprint**

1. Create the **profile.cer** file, and copy the certificate content under the **distribution-certificate** field of the [**HarmonyAppProvision** file](../../application-dev/security/app-provision-structure.md) to the **profile.cer** file.

   ```json
   {
       ...
       "bundle-info": {
           "distribution-certificate": "-----BEGIN CERTIFICATE----\nMIICMzCCAbegAwIBAgIEaOC/zDAMBggqhkjOPQQDAwUAMk..." / Certificate content.
           ...
       }
       ...
   }
   ```

2. Apply line breaks in the **profile.cer** content and remove the newline characters.
   ```
   -----BEGIN CERTIFICATE-----
   MIICMzCCAbegAwIBAgIEaOC/zDAMBggqhkjOPQQDAwUAMGMxCzAJBgNVBAYTAkNO
   MRQwEgYDVQQKEwtPcGVuSGFybW9ueTEZMBcGA1UECxMQT3Blbkhhcm1vbnkgVGVh
   bTEjMCEGA1UEAxMaT3Blbkhhcm1vbnkgQXBwbGljYXRpb24gQ0EwHhcNMjEwMjAy
   MTIxOTMxWhcNNDkxMjMxMTIxOTMxWjBoMQswCQYDVQQGEwJDTjEUMBIGA1UEChML
   T3Blbkhhcm1vbnkxGTAXBgNVBAsTEE9wZW5IYXJtb255IFRlYW0xKDAmBgNVBAMT
   H09wZW5IYXJtb255IEFwcGxpY2F0aW9uIFJlbGVhc2UwWTATBgcqhkjOPQIBBggq
   hkjOPQMBBwNCAATbYOCQQpW5fdkYHN45v0X3AHax12jPBdEDosFRIZ1eXmxOYzSG
   JwMfsHhUU90E8lI0TXYZnNmgM1sovubeQqATo1IwUDAfBgNVHSMEGDAWgBTbhrci
   FtULoUu33SV7ufEFfaItRzAOBgNVHQ8BAf8EBAMCB4AwHQYDVR0OBBYEFPtxruhl
   cRBQsJdwcZqLu9oNUVgaMAwGCCqGSM49BAMDBQADaAAwZQIxAJta0PQ2p4DIu/ps
   LMdLCDgQ5UH1l0B4PGhBlMgdi2zf8nk9spazEQI/0XNwpft8QAIwHSuA2WelVi/o
   zAlF08DnbJrOOtOnQq5wHOPlDYB4OtUzOYJk9scotrEnJxJzGsh/
   -----END CERTIFICATE-----
   ```

3. Use keytool to run the following command to obtain the certificate fingerprint.

   > **NOTE**
   >
   > You can obtain keytool from the **\tools\openjdk\bin** directory after DevEco Studio is installed.
   ```shell
   keytool -printcert -file profile.cer
   
   # Example
   # result:
   # Issued To: CN=OpenHarmony Application Release, OU=OpenHarmony Team, O=OpenHarmony, C=CN
   # Issued By: CN=OpenHarmony Application CA, OU=OpenHarmony Team, O=OpenHarmony, C=CN
   # SN: 68e0bfcc
   # Valid From: Tue Feb 02 20:19:31 CST 2021, Valid To: Fri Dec 31 20:19:31 CST 2049
   # Fingerprints:
   #          SHA1 fingerprint: E3:E8:7C:65:B8:1D:02:52:24:6A:06:A4:3C:4A:02:39:19:92:D1:F5
   #          SHA256 fingerprint: 8E:93:86:3F:C3:2E:E2:38:06:0B:F6:9A:9B:37:E2:60:8F:FF:B2:1F:93:C8:62:DD:51:1C:BA:C9:F3:00:24:B5 // After the colons are removed, the fingerprint is 8E93863FC32EE238060BF69A9B37E2608FFFB21F93C862DD511CBAC9F30024B5.
   # ...
   ```

#### Configuration in install_list.json

```json
{
     "install_list" : [
        {
            "app_dir" : "/system/app/com.ohos.launcher",
            "removable": true // The application can be uninstalled.
        }
     ]
}
```
