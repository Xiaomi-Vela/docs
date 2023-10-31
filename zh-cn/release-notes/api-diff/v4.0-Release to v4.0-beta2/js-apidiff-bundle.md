| 操作 | 旧版本 | 新版本 | d.ts文件 |
| ---- | ------ | ------ | -------- |
|删除|类名：ExtensionAbilityType;<br>方法or属性：APP_ACCOUNT_AUTHORIZATION = 19|NA|@ohos.bundle.bundleManager.d.ts|
|新增|NA|类名：appControl;<br>方法or属性：function setDisposedStatusSync(appId: string, disposedWant: Want): void;|@ohos.bundle.appControl.d.ts|
|新增|NA|类名：appControl;<br>方法or属性：function getDisposedStatusSync(appId: string): Want;|@ohos.bundle.appControl.d.ts|
|新增|NA|类名：appControl;<br>方法or属性：function deleteDisposedStatusSync(appId: string): void;|@ohos.bundle.appControl.d.ts|
|新增|NA|类名：bundleManager;<br>方法or属性：function queryAbilityInfoSync(want: Want, abilityFlags: number, userId?: number): Array\<AbilityInfo>;|@ohos.bundle.bundleManager.d.ts|
|新增|NA|类名：bundleManager;<br>方法or属性：function queryExtensionAbilityInfoSync(want: Want, extensionAbilityType: ExtensionAbilityType,<br><br>    extensionAbilityFlags: number, userId?: number): Array\<ExtensionAbilityInfo>;|@ohos.bundle.bundleManager.d.ts|
|新增|NA|类名：bundleManager;<br>方法or属性：function getBundleNameByUidSync(uid: number): string;|@ohos.bundle.bundleManager.d.ts|
|新增|NA|类名：bundleManager;<br>方法or属性：function getBundleArchiveInfoSync(hapFilePath: string, bundleFlags: number): BundleInfo;|@ohos.bundle.bundleManager.d.ts|
|新增|NA|类名：bundleManager;<br>方法or属性：function setApplicationEnabledSync(bundleName: string, isEnabled: boolean): void;|@ohos.bundle.bundleManager.d.ts|
|新增|NA|类名：bundleManager;<br>方法or属性：function setAbilityEnabledSync(info: AbilityInfo, isEnabled: boolean): void;|@ohos.bundle.bundleManager.d.ts|
|新增|NA|类名：bundleManager;<br>方法or属性：function isApplicationEnabledSync(bundleName: string): boolean;|@ohos.bundle.bundleManager.d.ts|
|新增|NA|类名：bundleManager;<br>方法or属性：function isAbilityEnabledSync(info: AbilityInfo): boolean;|@ohos.bundle.bundleManager.d.ts|
|新增|NA|类名：bundleManager;<br>方法or属性：function getLaunchWantForBundleSync(bundleName: string, userId?: number): Want;|@ohos.bundle.bundleManager.d.ts|
|新增|NA|类名：bundleManager;<br>方法or属性：function getProfileByAbilitySync(moduleName: string, abilityName: string, metadataName?: string): Array\<string>;|@ohos.bundle.bundleManager.d.ts|
|新增|NA|类名：bundleManager;<br>方法or属性：function getProfileByExtensionAbilitySync(moduleName: string, extensionAbilityName: string, metadataName?: string): Array\<string>;|@ohos.bundle.bundleManager.d.ts|
|新增|NA|类名：bundleManager;<br>方法or属性：function getPermissionDefSync(permissionName: string): PermissionDef;|@ohos.bundle.bundleManager.d.ts|
|新增|NA|类名：bundleManager;<br>方法or属性：function getAbilityLabelSync(bundleName: string, moduleName: string, abilityName: string): string;|@ohos.bundle.bundleManager.d.ts|
|新增|NA|类名：bundleManager;<br>方法or属性：function getAppProvisionInfoSync(bundleName: string, userId?: number): AppProvisionInfo;|@ohos.bundle.bundleManager.d.ts|
|新增|NA|类名：bundleManager;<br>方法or属性：export type ModuleMetadata = _ModuleMetadata;|@ohos.bundle.bundleManager.d.ts|
|新增|NA|类名：ExtensionAbilityType;<br>方法or属性：SHARE = 16|@ohos.bundle.bundleManager.d.ts|
|新增|NA|类名：ExtensionAbilityType;<br>方法or属性：ACTION = 19|@ohos.bundle.bundleManager.d.ts|
|新增|NA|类名：defaultAppManager;<br>方法or属性：function isDefaultApplicationSync(type: string): boolean;|@ohos.bundle.defaultAppManager.d.ts|
|新增|NA|类名：defaultAppManager;<br>方法or属性：function getDefaultApplicationSync(type: string, userId?: number): BundleInfo;|@ohos.bundle.defaultAppManager.d.ts|
|新增|NA|类名：defaultAppManager;<br>方法or属性：function setDefaultApplicationSync(type: string, elementName: ElementName, userId?: number): void;|@ohos.bundle.defaultAppManager.d.ts|
|新增|NA|类名：defaultAppManager;<br>方法or属性：function resetDefaultApplicationSync(type: string, userId?: number): void;|@ohos.bundle.defaultAppManager.d.ts|
|新增|NA|类名：sourcefile;<br>方法or属性：export type BundleStatusCallback = _BundleStatusCallback;|@ohos.bundle.innerBundleManager.d.ts|
|新增|NA|类名：installer;<br>方法or属性：function getBundleInstallerSync(): BundleInstaller;|@ohos.bundle.installer.d.ts|
|新增|NA|类名：BundleInstaller;<br>方法or属性：updateBundleForSelf(hapFilePaths: Array\<string>, installParam: InstallParam, callback: AsyncCallback\<void>): void;|@ohos.bundle.installer.d.ts|
|新增|NA|类名：BundleInstaller;<br>方法or属性：updateBundleForSelf(hapFilePaths: Array\<string>, callback: AsyncCallback\<void>): void;|@ohos.bundle.installer.d.ts|
|新增|NA|类名：BundleInstaller;<br>方法or属性：updateBundleForSelf(hapFilePaths: Array\<string>, installParam?: InstallParam): Promise\<void>;|@ohos.bundle.installer.d.ts|
|新增|NA|类名：launcherBundleManager;<br>方法or属性：function getLauncherAbilityInfoSync(bundleName: string, userId: number): Array\<LauncherAbilityInfo>;|@ohos.bundle.launcherBundleManager.d.ts|
|新增|NA|类名：launcherBundleManager;<br>方法or属性：function getShortcutInfoSync(bundleName: string): Array\<ShortcutInfo>;|@ohos.bundle.launcherBundleManager.d.ts|
|新增|NA|类名：zlib;<br>方法or属性：function decompressFile(inFile: string, outFile: string, callback: AsyncCallback\<void>): void;|@ohos.zlib.d.ts|
|新增|NA|类名：ApplicationInfo;<br>方法or属性：readonly metadataArray: Array\<ModuleMetadata>;|ApplicationInfo.d.ts|
|新增|NA|类名：ModuleMetadata;<br>方法or属性：readonly moduleName: string;|ApplicationInfo.d.ts|
|新增|NA|类名：ModuleMetadata;<br>方法or属性：readonly metadata: Array\<Metadata>;|ApplicationInfo.d.ts|
|废弃版本有变化|类名：ApplicationInfo;<br>方法or属性：readonly metadata: Map\<string, Array\<Metadata>>;<br>旧版本信息：|类名：ApplicationInfo;<br>方法or属性：readonly metadata: Map\<string, Array\<Metadata>>;<br>新版本信息：10<br>代替接口： ApplicationInfo#metadataArray|ApplicationInfo.d.ts|
|错误码有变化|类名：BundleInstaller;<br>方法or属性：install(hapFilePaths: Array\<string>, installParam: InstallParam, callback: AsyncCallback\<void>): void;<br>旧版本信息：201,202,401,17700004,17700010,17700011,17700012,17700015,17700016,17700017,17700018,17700031,17700036,17700039,17700041,17700042,17700043,17700044,17700047,17700048|类名：BundleInstaller;<br>方法or属性：install(hapFilePaths: Array\<string>, installParam: InstallParam, callback: AsyncCallback\<void>): void;<br>新版本信息：201,202,401,17700004,17700010,17700011,17700012,17700015,17700016,17700017,17700018,17700031,17700036,17700039,17700041,17700042,17700043,17700044,17700047,17700048,17700050|@ohos.bundle.installer.d.ts|
|错误码有变化|类名：BundleInstaller;<br>方法or属性：install(hapFilePaths: Array\<string>, callback: AsyncCallback\<void>): void;<br>旧版本信息：201,202,401,17700010,17700011,17700012,17700015,17700016,17700017,17700018,17700031,17700036,17700039,17700041,17700042,17700043,17700044,17700047,17700048|类名：BundleInstaller;<br>方法or属性：install(hapFilePaths: Array\<string>, callback: AsyncCallback\<void>): void;<br>新版本信息：201,202,401,17700010,17700011,17700012,17700015,17700016,17700017,17700018,17700031,17700036,17700039,17700041,17700042,17700043,17700044,17700047,17700048,17700050|@ohos.bundle.installer.d.ts|
|错误码有变化|类名：BundleInstaller;<br>方法or属性：install(hapFilePaths: Array\<string>, installParam?: InstallParam): Promise\<void>;<br>旧版本信息：201,202,401,17700004,17700010,17700011,17700012,17700015,17700016,17700017,17700018,17700031,17700036,17700039,17700041,17700042,17700043,17700044,17700047,17700048|类名：BundleInstaller;<br>方法or属性：install(hapFilePaths: Array\<string>, installParam?: InstallParam): Promise\<void>;<br>新版本信息：201,202,401,17700004,17700010,17700011,17700012,17700015,17700016,17700017,17700018,17700031,17700036,17700039,17700041,17700042,17700043,17700044,17700047,17700048,17700050|@ohos.bundle.installer.d.ts|
|错误码有变化|类名：BundleInstaller;<br>方法or属性：uninstall(uninstallParam: UninstallParam, callback: AsyncCallback\<void>): void;<br>旧版本信息：201,401,17700020,17700037,17700038|类名：BundleInstaller;<br>方法or属性：uninstall(uninstallParam: UninstallParam, callback: AsyncCallback\<void>): void;<br>新版本信息：201,202,401,17700020,17700037,17700038|@ohos.bundle.installer.d.ts|
|错误码有变化|类名：BundleInstaller;<br>方法or属性：uninstall(uninstallParam: UninstallParam): Promise\<void>;<br>旧版本信息：201,401,17700020,17700037,17700038|类名：BundleInstaller;<br>方法or属性：uninstall(uninstallParam: UninstallParam): Promise\<void>;<br>新版本信息：201,202,401,17700020,17700037,17700038|@ohos.bundle.installer.d.ts|
|权限有变化|类名：BundleInstaller;<br>方法or属性：install(hapFilePaths: Array\<string>, installParam: InstallParam, callback: AsyncCallback\<void>): void;<br>旧版本信息：ohos.permission.INSTALL_BUNDLE,ohos.permission.INSTALL_ENTERPRISE_BUNDLE|类名：BundleInstaller;<br>方法or属性：install(hapFilePaths: Array\<string>, installParam: InstallParam, callback: AsyncCallback\<void>): void;<br>新版本信息：ohos.permission.INSTALL_BUNDLE,ohos.permission.INSTALL_ENTERPRISE_BUNDLE,ohos.permission.INSTALL_ENTERPRISE_MDM_BUNDLE,ohos.permission.INSTALL_ENTERPRISE_NORMAL_BUNDLE|@ohos.bundle.installer.d.ts|
|权限有变化|类名：BundleInstaller;<br>方法or属性：install(hapFilePaths: Array\<string>, callback: AsyncCallback\<void>): void;<br>旧版本信息：ohos.permission.INSTALL_BUNDLE,ohos.permission.INSTALL_ENTERPRISE_BUNDLE|类名：BundleInstaller;<br>方法or属性：install(hapFilePaths: Array\<string>, callback: AsyncCallback\<void>): void;<br>新版本信息：ohos.permission.INSTALL_BUNDLE,ohos.permission.INSTALL_ENTERPRISE_BUNDLE,ohos.permission.INSTALL_ENTERPRISE_MDM_BUNDLE,ohos.permission.INSTALL_ENTERPRISE_NORMAL_BUNDLE|@ohos.bundle.installer.d.ts|
|权限有变化|类名：BundleInstaller;<br>方法or属性：install(hapFilePaths: Array\<string>, installParam?: InstallParam): Promise\<void>;<br>旧版本信息：ohos.permission.INSTALL_BUNDLE,ohos.permission.INSTALL_ENTERPRISE_BUNDLE|类名：BundleInstaller;<br>方法or属性：install(hapFilePaths: Array\<string>, installParam?: InstallParam): Promise\<void>;<br>新版本信息：ohos.permission.INSTALL_BUNDLE,ohos.permission.INSTALL_ENTERPRISE_BUNDLE,ohos.permission.INSTALL_ENTERPRISE_MDM_BUNDLE,ohos.permission.INSTALL_ENTERPRISE_NORMAL_BUNDLE|@ohos.bundle.installer.d.ts|
|权限有变化|类名：BundleInstaller;<br>方法or属性：uninstall(bundleName: string, installParam: InstallParam, callback: AsyncCallback\<void>): void;<br>旧版本信息：ohos.permission.INSTALL_BUNDLE|类名：BundleInstaller;<br>方法or属性：uninstall(bundleName: string, installParam: InstallParam, callback: AsyncCallback\<void>): void;<br>新版本信息：ohos.permission.INSTALL_BUNDLE,ohos.permission.UNINSTALL_BUNDLE|@ohos.bundle.installer.d.ts|
|权限有变化|类名：BundleInstaller;<br>方法or属性：uninstall(bundleName: string, callback: AsyncCallback\<void>): void;<br>旧版本信息：ohos.permission.INSTALL_BUNDLE|类名：BundleInstaller;<br>方法or属性：uninstall(bundleName: string, callback: AsyncCallback\<void>): void;<br>新版本信息：ohos.permission.INSTALL_BUNDLE,ohos.permission.UNINSTALL_BUNDLE|@ohos.bundle.installer.d.ts|
|权限有变化|类名：BundleInstaller;<br>方法or属性：uninstall(bundleName: string, installParam?: InstallParam): Promise\<void>;<br>旧版本信息：ohos.permission.INSTALL_BUNDLE|类名：BundleInstaller;<br>方法or属性：uninstall(bundleName: string, installParam?: InstallParam): Promise\<void>;<br>新版本信息：ohos.permission.INSTALL_BUNDLE,ohos.permission.UNINSTALL_BUNDLE|@ohos.bundle.installer.d.ts|
|权限有变化|类名：BundleInstaller;<br>方法or属性：uninstall(uninstallParam: UninstallParam, callback: AsyncCallback\<void>): void;<br>旧版本信息：ohos.permission.INSTALL_BUNDLE|类名：BundleInstaller;<br>方法or属性：uninstall(uninstallParam: UninstallParam, callback: AsyncCallback\<void>): void;<br>新版本信息：ohos.permission.INSTALL_BUNDLE,ohos.permission.UNINSTALL_BUNDLE|@ohos.bundle.installer.d.ts|
|权限有变化|类名：BundleInstaller;<br>方法or属性：uninstall(uninstallParam: UninstallParam): Promise\<void>;<br>旧版本信息：ohos.permission.INSTALL_BUNDLE|类名：BundleInstaller;<br>方法or属性：uninstall(uninstallParam: UninstallParam): Promise\<void>;<br>新版本信息：ohos.permission.INSTALL_BUNDLE,ohos.permission.UNINSTALL_BUNDLE|@ohos.bundle.installer.d.ts|
|权限有变化|类名：BundleInstaller;<br>方法or属性：recover(bundleName: string, installParam: InstallParam, callback: AsyncCallback\<void>): void;<br>旧版本信息：ohos.permission.INSTALL_BUNDLE|类名：BundleInstaller;<br>方法or属性：recover(bundleName: string, installParam: InstallParam, callback: AsyncCallback\<void>): void;<br>新版本信息：ohos.permission.INSTALL_BUNDLE,ohos.permission.RECOVER_BUNDLE|@ohos.bundle.installer.d.ts|
|权限有变化|类名：BundleInstaller;<br>方法or属性：recover(bundleName: string, callback: AsyncCallback\<void>): void;<br>旧版本信息：ohos.permission.INSTALL_BUNDLE|类名：BundleInstaller;<br>方法or属性：recover(bundleName: string, callback: AsyncCallback\<void>): void;<br>新版本信息：ohos.permission.INSTALL_BUNDLE,ohos.permission.RECOVER_BUNDLE|@ohos.bundle.installer.d.ts|
|权限有变化|类名：BundleInstaller;<br>方法or属性：recover(bundleName: string, installParam?: InstallParam): Promise\<void>;<br>旧版本信息：ohos.permission.INSTALL_BUNDLE|类名：BundleInstaller;<br>方法or属性：recover(bundleName: string, installParam?: InstallParam): Promise\<void>;<br>新版本信息：ohos.permission.INSTALL_BUNDLE,ohos.permission.RECOVER_BUNDLE|@ohos.bundle.installer.d.ts|
|函数有变化|类名：zlib;<br>方法or属性：function decompressFile(inFile: string, outFile: string, options: Options): Promise\<void>;|类名：zlib;<br>方法or属性：function decompressFile(inFile: string, outFile: string, options?: Options): Promise\<void>;|@ohos.zlib.d.ts|