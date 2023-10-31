| Change Type | Old Version | New Version | d.ts File |
| ---- | ------ | ------ | -------- |
|Deleted|Class name: ExtensionAbilityType;<br>Method or attribute name: APP_ACCOUNT_AUTHORIZATION = 19|NA|@ohos.bundle.bundleManager.d.ts|
|Added|NA|Class name: appControl;<br>Method or attribute name: function setDisposedStatusSync(appId: string, disposedWant: Want): void;|@ohos.bundle.appControl.d.ts|
|Added|NA|Class name: appControl;<br>Method or attribute name: function getDisposedStatusSync(appId: string): Want;|@ohos.bundle.appControl.d.ts|
|Added|NA|Class name: appControl;<br>Method or attribute name: function deleteDisposedStatusSync(appId: string): void;|@ohos.bundle.appControl.d.ts|
|Added|NA|Class name: bundleManager;<br>Method or attribute name: function queryAbilityInfoSync(want: Want, abilityFlags: number, userId?: number): Array\<AbilityInfo>;|@ohos.bundle.bundleManager.d.ts|
|Added|NA|Class name: bundleManager;<br>Method or attribute name: function queryExtensionAbilityInfoSync(want: Want, extensionAbilityType: ExtensionAbilityType,<br><br>    extensionAbilityFlags: number, userId?: number): Array\<ExtensionAbilityInfo>;|@ohos.bundle.bundleManager.d.ts|
|Added|NA|Class name: bundleManager;<br>Method or attribute name: function getBundleNameByUidSync(uid: number): string;|@ohos.bundle.bundleManager.d.ts|
|Added|NA|Class name: bundleManager;<br>Method or attribute name: function getBundleArchiveInfoSync(hapFilePath: string, bundleFlags: number): BundleInfo;|@ohos.bundle.bundleManager.d.ts|
|Added|NA|Class name: bundleManager;<br>Method or attribute name: function setApplicationEnabledSync(bundleName: string, isEnabled: boolean): void;|@ohos.bundle.bundleManager.d.ts|
|Added|NA|Class name: bundleManager;<br>Method or attribute name: function setAbilityEnabledSync(info: AbilityInfo, isEnabled: boolean): void;|@ohos.bundle.bundleManager.d.ts|
|Added|NA|Class name: bundleManager;<br>Method or attribute name: function isApplicationEnabledSync(bundleName: string): boolean;|@ohos.bundle.bundleManager.d.ts|
|Added|NA|Class name: bundleManager;<br>Method or attribute name: function isAbilityEnabledSync(info: AbilityInfo): boolean;|@ohos.bundle.bundleManager.d.ts|
|Added|NA|Class name: bundleManager;<br>Method or attribute name: function getLaunchWantForBundleSync(bundleName: string, userId?: number): Want;|@ohos.bundle.bundleManager.d.ts|
|Added|NA|Class name: bundleManager;<br>Method or attribute name: function getProfileByAbilitySync(moduleName: string, abilityName: string, metadataName?: string): Array\<string>;|@ohos.bundle.bundleManager.d.ts|
|Added|NA|Class name: bundleManager;<br>Method or attribute name: function getProfileByExtensionAbilitySync(moduleName: string, extensionAbilityName: string, metadataName?: string): Array\<string>;|@ohos.bundle.bundleManager.d.ts|
|Added|NA|Class name: bundleManager;<br>Method or attribute name: function getPermissionDefSync(permissionName: string): PermissionDef;|@ohos.bundle.bundleManager.d.ts|
|Added|NA|Class name: bundleManager;<br>Method or attribute name: function getAbilityLabelSync(bundleName: string, moduleName: string, abilityName: string): string;|@ohos.bundle.bundleManager.d.ts|
|Added|NA|Class name: bundleManager;<br>Method or attribute name: function getAppProvisionInfoSync(bundleName: string, userId?: number): AppProvisionInfo;|@ohos.bundle.bundleManager.d.ts|
|Added|NA|Class name: bundleManager;<br>Method or attribute name: export type ModuleMetadata = _ModuleMetadata;|@ohos.bundle.bundleManager.d.ts|
|Added|NA|Class name: ExtensionAbilityType;<br>Method or attribute name: SHARE = 16|@ohos.bundle.bundleManager.d.ts|
|Added|NA|Class name: ExtensionAbilityType;<br>Method or attribute name: ACTION = 19|@ohos.bundle.bundleManager.d.ts|
|Added|NA|Class name: defaultAppManager;<br>Method or attribute name: function isDefaultApplicationSync(type: string): boolean;|@ohos.bundle.defaultAppManager.d.ts|
|Added|NA|Class name: defaultAppManager;<br>Method or attribute name: function getDefaultApplicationSync(type: string, userId?: number): BundleInfo;|@ohos.bundle.defaultAppManager.d.ts|
|Added|NA|Class name: defaultAppManager;<br>Method or attribute name: function setDefaultApplicationSync(type: string, elementName: ElementName, userId?: number): void;|@ohos.bundle.defaultAppManager.d.ts|
|Added|NA|Class name: defaultAppManager;<br>Method or attribute name: function resetDefaultApplicationSync(type: string, userId?: number): void;|@ohos.bundle.defaultAppManager.d.ts|
|Added|NA|Class name: sourcefile;<br>Method or attribute name: export type BundleStatusCallback = _BundleStatusCallback;|@ohos.bundle.innerBundleManager.d.ts|
|Added|NA|Class name: installer;<br>Method or attribute name: function getBundleInstallerSync(): BundleInstaller;|@ohos.bundle.installer.d.ts|
|Added|NA|Class name: BundleInstaller;<br>Method or attribute name: updateBundleForSelf(hapFilePaths: Array\<string>, installParam: InstallParam, callback: AsyncCallback\<void>): void;|@ohos.bundle.installer.d.ts|
|Added|NA|Class name: BundleInstaller;<br>Method or attribute name: updateBundleForSelf(hapFilePaths: Array\<string>, callback: AsyncCallback\<void>): void;|@ohos.bundle.installer.d.ts|
|Added|NA|Class name: BundleInstaller;<br>Method or attribute name: updateBundleForSelf(hapFilePaths: Array\<string>, installParam?: InstallParam): Promise\<void>;|@ohos.bundle.installer.d.ts|
|Added|NA|Class name: launcherBundleManager;<br>Method or attribute name: function getLauncherAbilityInfoSync(bundleName: string, userId: number): Array\<LauncherAbilityInfo>;|@ohos.bundle.launcherBundleManager.d.ts|
|Added|NA|Class name: launcherBundleManager;<br>Method or attribute name: function getShortcutInfoSync(bundleName: string): Array\<ShortcutInfo>;|@ohos.bundle.launcherBundleManager.d.ts|
|Added|NA|Class name: zlib;<br>Method or attribute name: function decompressFile(inFile: string, outFile: string, callback: AsyncCallback\<void>): void;|@ohos.zlib.d.ts|
|Added|NA|Class name: ApplicationInfo;<br>Method or attribute name: readonly metadataArray: Array\<ModuleMetadata>;|ApplicationInfo.d.ts|
|Added|NA|Class name: ModuleMetadata;<br>Method or attribute name: readonly moduleName: string;|ApplicationInfo.d.ts|
|Added|NA|Class name: ModuleMetadata;<br>Method or attribute name: readonly metadata: Array\<Metadata>;|ApplicationInfo.d.ts|
|Deprecated version changed|Class name: ApplicationInfo;<br>Method or attribute name: readonly metadata: Map\<string, Array\<Metadata>>;<br>Old version information: |Class name: ApplicationInfo;<br>Method or attribute name: readonly metadata: Map\<string, Array\<Metadata>>;<br>New version information: 10<br>Substitute API: ApplicationInfo#metadataArray|ApplicationInfo.d.ts|
|Error code changed|Class name: BundleInstaller;<br>Method or attribute name: install(hapFilePaths: Array\<string>, installParam: InstallParam, callback: AsyncCallback\<void>): void;<br>Old version information: 201,202,401, 17700004, 17700010, 17700011, 17700012, 17700015, 17700016, 17700017, 17700018, 17700031, 17700036, 17700039, 17700041, 17700042, 17700043,17700044, 17700047, 17700048|Class name: BundleInstaller;<br>Method or attribute name: install(hapFilePaths: Array\<string>, installParam: InstallParam, callback: AsyncCallback\<void>): void;<br>New version information: 201,202,401, 17700004, 17700010, 17700011, 17700012, 17700015, 17700016, 17700017, 17700018, 17700031, 17700036, 17700039, 17700041, 17700042, 17700043,17700044, 17700047, 17700048, 17700050|@ohos.bundle.installer.d.ts|
|Error code changed|Class name: BundleInstaller;<br>Method or attribute name: install(hapFilePaths: Array\<string>, callback: AsyncCallback\<void>): void;<br>Old version information: 201,202,401, 17700010, 17700011, 17700012, 17700015, 17700016, 17700017, 17700018, 17700031, 17700036, 17700039, 17700041, 17700042, 17700043,17700044, 17700047, 17700048|Class name: BundleInstaller;<br>Method or attribute name: install(hapFilePaths: Array\<string>, callback: AsyncCallback\<void>): void;<br>New version information: 201,202,401, 17700010, 17700011, 17700012, 17700015, 17700016, 17700017, 17700018, 17700031, 17700036, 17700039, 17700041, 17700042, 17700043,17700044, 17700047, 17700048, 17700050|@ohos.bundle.installer.d.ts|
|Error code changed|Class name: BundleInstaller;<br>Method or attribute name: install(hapFilePaths: Array\<string>, installParam?: InstallParam): Promise\<void>;<br>Old version information: 201,202,401, 17700004, 17700010, 17700011, 17700012, 17700015, 17700016, 17700017, 17700018, 17700031, 17700036, 17700039, 17700041, 17700042, 17700043,17700044, 17700047, 17700048|Class name: BundleInstaller;<br>Method or attribute name: install(hapFilePaths: Array\<string>, installParam?: InstallParam): Promise\<void>;<br>New version information: 201,202,401, 17700004, 17700010, 17700011, 17700012, 17700015, 17700016, 17700017, 17700018, 17700031, 17700036, 17700039, 17700041, 17700042, 17700043,17700044, 17700047, 17700048, 17700050|@ohos.bundle.installer.d.ts|
|Error code changed|Class name: BundleInstaller;<br>Method or attribute name: uninstall(uninstallParam: UninstallParam, callback: AsyncCallback\<void>): void;<br>Old version information: 201,401, 17700020, 17700037, 17700038|Class name: BundleInstaller;<br>Method or attribute name: uninstall(uninstallParam: UninstallParam, callback: AsyncCallback\<void>): void;<br>New version information: 201,202,401, 17700020, 17700037, 17700038|@ohos.bundle.installer.d.ts|
|Error code changed|Class name: BundleInstaller;<br>Method or attribute name: uninstall(uninstallParam: UninstallParam): Promise\<void>;<br>Old version information: 201,401, 17700020, 17700037, 17700038|Class name: BundleInstaller;<br>Method or attribute name: uninstall(uninstallParam: UninstallParam): Promise\<void>;<br>New version information: 201,202,401, 17700020, 17700037, 17700038|@ohos.bundle.installer.d.ts|
|Permission changed|Class name: BundleInstaller;<br>Method or attribute name: install(hapFilePaths: Array\<string>, installParam: InstallParam, callback: AsyncCallback\<void>): void;<br>Old version information: ohos.permission.INSTALL_BUNDLE,ohos.permission.INSTALL_ENTERPRISE_BUNDLE|Class name: BundleInstaller;<br>Method or attribute name: install(hapFilePaths: Array\<string>, installParam: InstallParam, callback: AsyncCallback\<void>): void;<br>New version information: ohos.permission.INSTALL_BUNDLE,ohos.permission.INSTALL_ENTERPRISE_BUNDLE,ohos.permission.INSTALL_ENTERPRISE_MDM_BUNDLE,ohos.permission.INSTALL_ENTERPRISE_NORMAL_BUNDLE|@ohos.bundle.installer.d.ts|
|Permission changed|Class name: BundleInstaller;<br>Method or attribute name: install(hapFilePaths: Array\<string>, callback: AsyncCallback\<void>): void;<br>Old version information: ohos.permission.INSTALL_BUNDLE,ohos.permission.INSTALL_ENTERPRISE_BUNDLE|Class name: BundleInstaller;<br>Method or attribute name: install(hapFilePaths: Array\<string>, callback: AsyncCallback\<void>): void;<br>New version information: ohos.permission.INSTALL_BUNDLE,ohos.permission.INSTALL_ENTERPRISE_BUNDLE,ohos.permission.INSTALL_ENTERPRISE_MDM_BUNDLE,ohos.permission.INSTALL_ENTERPRISE_NORMAL_BUNDLE|@ohos.bundle.installer.d.ts|
|Permission changed|Class name: BundleInstaller;<br>Method or attribute name: install(hapFilePaths: Array\<string>, installParam?: InstallParam): Promise\<void>;<br>Old version information: ohos.permission.INSTALL_BUNDLE,ohos.permission.INSTALL_ENTERPRISE_BUNDLE|Class name: BundleInstaller;<br>Method or attribute name: install(hapFilePaths: Array\<string>, installParam?: InstallParam): Promise\<void>;<br>New version information: ohos.permission.INSTALL_BUNDLE,ohos.permission.INSTALL_ENTERPRISE_BUNDLE,ohos.permission.INSTALL_ENTERPRISE_MDM_BUNDLE,ohos.permission.INSTALL_ENTERPRISE_NORMAL_BUNDLE|@ohos.bundle.installer.d.ts|
|Permission changed|Class name: BundleInstaller;<br>Method or attribute name: uninstall(bundleName: string, installParam: InstallParam, callback: AsyncCallback\<void>): void;<br>Old version information: ohos.permission.INSTALL_BUNDLE|Class name: BundleInstaller;<br>Method or attribute name: uninstall(bundleName: string, installParam: InstallParam, callback: AsyncCallback\<void>): void;<br>New version information: ohos.permission.INSTALL_BUNDLE,ohos.permission.UNINSTALL_BUNDLE|@ohos.bundle.installer.d.ts|
|Permission changed|Class name: BundleInstaller;<br>Method or attribute name: uninstall(bundleName: string, callback: AsyncCallback\<void>): void;<br>Old version information: ohos.permission.INSTALL_BUNDLE|Class name: BundleInstaller;<br>Method or attribute name: uninstall(bundleName: string, callback: AsyncCallback\<void>): void;<br>New version information: ohos.permission.INSTALL_BUNDLE,ohos.permission.UNINSTALL_BUNDLE|@ohos.bundle.installer.d.ts|
|Permission changed|Class name: BundleInstaller;<br>Method or attribute name: uninstall(bundleName: string, installParam?: InstallParam): Promise\<void>;<br>Old version information: ohos.permission.INSTALL_BUNDLE|Class name: BundleInstaller;<br>Method or attribute name: uninstall(bundleName: string, installParam?: InstallParam): Promise\<void>;<br>New version information: ohos.permission.INSTALL_BUNDLE,ohos.permission.UNINSTALL_BUNDLE|@ohos.bundle.installer.d.ts|
|Permission changed|Class name: BundleInstaller;<br>Method or attribute name: uninstall(uninstallParam: UninstallParam, callback: AsyncCallback\<void>): void;<br>Old version information: ohos.permission.INSTALL_BUNDLE|Class name: BundleInstaller;<br>Method or attribute name: uninstall(uninstallParam: UninstallParam, callback: AsyncCallback\<void>): void;<br>New version information: ohos.permission.INSTALL_BUNDLE,ohos.permission.UNINSTALL_BUNDLE|@ohos.bundle.installer.d.ts|
|Permission changed|Class name: BundleInstaller;<br>Method or attribute name: uninstall(uninstallParam: UninstallParam): Promise\<void>;<br>Old version information: ohos.permission.INSTALL_BUNDLE|Class name: BundleInstaller;<br>Method or attribute name: uninstall(uninstallParam: UninstallParam): Promise\<void>;<br>New version information: ohos.permission.INSTALL_BUNDLE,ohos.permission.UNINSTALL_BUNDLE|@ohos.bundle.installer.d.ts|
|Permission changed|Class name: BundleInstaller;<br>Method or attribute name: recover(bundleName: string, installParam: InstallParam, callback: AsyncCallback\<void>): void;<br>Old version information: ohos.permission.INSTALL_BUNDLE|Class name: BundleInstaller;<br>Method or attribute name: recover(bundleName: string, installParam: InstallParam, callback: AsyncCallback\<void>): void;<br>New version information: ohos.permission.INSTALL_BUNDLE,ohos.permission.RECOVER_BUNDLE|@ohos.bundle.installer.d.ts|
|Permission changed|Class name: BundleInstaller;<br>Method or attribute name: recover(bundleName: string, callback: AsyncCallback\<void>): void;<br>Old version information: ohos.permission.INSTALL_BUNDLE|Class name: BundleInstaller;<br>Method or attribute name: recover(bundleName: string, callback: AsyncCallback\<void>): void;<br>New version information: ohos.permission.INSTALL_BUNDLE,ohos.permission.RECOVER_BUNDLE|@ohos.bundle.installer.d.ts|
|Permission changed|Class name: BundleInstaller;<br>Method or attribute name: recover(bundleName: string, installParam?: InstallParam): Promise\<void>;<br>Old version information: ohos.permission.INSTALL_BUNDLE|Class name: BundleInstaller;<br>Method or attribute name: recover(bundleName: string, installParam?: InstallParam): Promise\<void>;<br>New version information: ohos.permission.INSTALL_BUNDLE,ohos.permission.RECOVER_BUNDLE|@ohos.bundle.installer.d.ts|
|Function changed|Class name: zlib;<br>Method or attribute name: function decompressFile(inFile: string, outFile: string, options: Options): Promise\<void>;|Class name: zlib;<br>Method or attribute name: function decompressFile(inFile: string, outFile: string, options?: Options): Promise\<void>;|@ohos.zlib.d.ts|