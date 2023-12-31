# 接口 

- [开发说明](development-intro.md)

- Ability框架
  - Stage模型能力的接口(推荐)
    - [@ohos.app.ability.Ability (Ability基类)](js-apis-app-ability-ability.md)
    - [@ohos.app.ability.AbilityConstant (AbilityConstant)](js-apis-app-ability-abilityConstant.md)
    - [@ohos.app.ability.abilityLifecycleCallback (AbilityLifecycleCallback)](js-apis-app-ability-abilityLifecycleCallback.md)
    - [@ohos.app.ability.AbilityStage (AbilityStage)](js-apis-app-ability-abilityStage.md)
    - [@ohos.app.ability.ActionExtensionAbility (自定义服务扩展能力)](js-apis-app-ability-actionExtensionAbility.md)
    - [@ohos.app.ability.ApplicationStateChangeCallback (ApplicationStateChangeCallback)](js-apis-app-ability-applicationStateChangeCallback.md)
    - [@ohos.app.ability.AutoFillExtensionAbility (AutoFillExtensionAbility)](js-apis-app-ability-autoFillExtensionAbility.md)
    - [@ohos.app.ability.AutoFillManager (AutoFillManager)](js-apis-app-ability-autoFillManager.md)
    - [@ohos.app.ability.ChildProcess](js-apis-app-ability-childProcess.md)
    - [@ohos.app.ability.childProcessManager (childProcessManager)](js-apis-app-ability-childProcessManager.md)
    - [@ohos.app.ability.common (应用上下文Context)](js-apis-app-ability-common.md)
    - [@ohos.app.ability.contextConstant (ContextConstant)](js-apis-app-ability-contextConstant.md)
    - [@ohos.app.ability.EnvironmentCallback (EnvironmentCallback)](js-apis-app-ability-environmentCallback.md)
    - [@ohos.app.ability.ExtensionAbility (扩展能力基类)](js-apis-app-ability-extensionAbility.md)
    - [@ohos.app.ability.insightIntent (insightIntent)](js-apis-app-ability-insightIntent.md)
    - [@ohos.app.ability.InsightIntentContext (意图调用执行上下文)](js-apis-app-ability-insightIntentContext.md)
    - [@ohos.app.ability.insightIntentDriver (执行意图调用)](js-apis-app-ability-insightIntentDriver.md)
    - [@ohos.app.ability.InsightIntentExecutor (意图调用执行基类)](js-apis-app-ability-insightIntentExecutor.md)
    - [@ohos.app.ability.PrintExtensionAbility (打印扩展能力)](js-apis-app-ability-PrintExtensionAbility.md)
    - [@ohos.app.ability.ServiceExtensionAbility (ServiceExtensionAbility)](js-apis-app-ability-serviceExtensionAbility.md)
    - [@ohos.app.ability.ShareExtensionAbility (分享模板服务扩展能力)](js-apis-app-ability-shareExtensionAbility.md)
    - [@ohos.app.ability.StartOptions (StartOptions)](js-apis-app-ability-startOptions.md)
    - [@ohos.app.ability.autoStartupManager(autoStartupManager)](js-apis-app-ability-autoStartupManager.md)
    - [@ohos.app.ability.UIAbility (UIAbility)](js-apis-app-ability-uiAbility.md)
    - [@ohos.app.ability.UIExtensionAbility (带界面扩展能力基类)](js-apis-app-ability-uiExtensionAbility.md)
    - [@ohos.app.ability.UIExtensionContentSession (带界面扩展能力界面操作类)](js-apis-app-ability-uiExtensionContentSession.md)
    - [@ohos.app.form.FormExtensionAbility (FormExtensionAbility)](js-apis-app-form-formExtensionAbility.md)
    - [@ohos.application.DataShareExtensionAbility (数据共享扩展能力)](js-apis-application-dataShareExtensionAbility.md)
    - [@ohos.application.StaticSubscriberExtensionAbility (StaticSubscriberExtensionAbility)](js-apis-application-staticSubscriberExtensionAbility.md)
  - FA模型能力的接口
    - [@ohos.ability.ability (Ability)](js-apis-ability-ability.md)
    - [@ohos.ability.featureAbility (FeatureAbility模块)](js-apis-ability-featureAbility.md)
    - [@ohos.ability.particleAbility (ParticleAbility模块)](js-apis-ability-particleAbility.md)
  - 通用能力的接口(推荐)
    - [@ohos.app.ability.abilityDelegatorRegistry (AbilityDelegatorRegistry)](js-apis-app-ability-abilityDelegatorRegistry.md)
    - [@ohos.app.ability.abilityManager (AbilityManager)](js-apis-app-ability-abilityManager.md)
    - [@ohos.app.ability.appManager (appManager)](js-apis-app-ability-appManager.md)
    - [@ohos.app.ability.appRecovery (appRecovery)](js-apis-app-ability-appRecovery.md)
    - [@ohos.app.ability.Configuration (Configuration)](js-apis-app-ability-configuration.md)
    - [@ohos.app.ability.ConfigurationConstant (ConfigurationConstant)](js-apis-app-ability-configurationConstant.md)
    - [@ohos.app.ability.dataUriUtils (DataUriUtils模块)](js-apis-app-ability-dataUriUtils.md)
    - [@ohos.app.ability.dialogRequest (dialogRequest模块)](js-apis-app-ability-dialogRequest.md)
    - [@ohos.app.ability.errorManager (ErrorManager)](js-apis-app-ability-errorManager.md)
    - [@ohos.app.ability.missionManager (missionManager)](js-apis-app-ability-missionManager.md)
    - [@ohos.app.ability.quickFixManager (quickFixManager)](js-apis-app-ability-quickFixManager.md)
    - [@ohos.app.ability.Want (Want)](js-apis-app-ability-want.md)
    - [@ohos.app.ability.wantAgent (WantAgent模块)](js-apis-app-ability-wantAgent.md)
    - [@ohos.app.ability.wantConstant (wantConstant)](js-apis-app-ability-wantConstant.md)
    - [@ohos.app.businessAbilityRouter (业务路由模块)](js-apis-businessAbilityRouter.md)
    - [@ohos.app.form.formAgent (FormAgent)](js-apis-app-form-formAgent.md)
    - [@ohos.app.form.formBindingData (卡片数据绑定类)](js-apis-app-form-formBindingData.md)
    - [@ohos.app.form.formHost (FormHost)](js-apis-app-form-formHost.md)
    - [@ohos.app.form.formInfo (FormInfo)](js-apis-app-form-formInfo.md)
    - [@ohos.application.formError (FormError)](js-apis-application-formError.md)
    - [@ohos.app.form.formObserver (formObserver)](js-apis-app-form-formObserver.md)
    - [@ohos.app.form.formProvider (FormProvider)](js-apis-app-form-formProvider.md)
    - [@ohos.application.uriPermissionManager (URI权限管理)](js-apis-uripermissionmanager.md)
  - 通用能力的接口(待停用)
    - [@ohos.ability.dataUriUtils (DataUriUtils模块)](js-apis-ability-dataUriUtils.md)
    - [@ohos.ability.errorCode (ErrorCode)](js-apis-ability-errorCode.md)
    - [@ohos.ability.wantConstant (wantConstant)](js-apis-ability-wantConstant.md)
    - [@ohos.application.abilityDelegatorRegistry (AbilityDelegatorRegistry)](js-apis-application-abilityDelegatorRegistry.md)
    - [@ohos.application.abilityManager (AbilityManager)](js-apis-application-abilityManager.md)
    - [@ohos.application.appManager (appManager)](js-apis-application-appManager.md)
    - [@ohos.application.Configuration (Configuration)](js-apis-application-configuration.md)
    - [@ohos.application.ConfigurationConstant (ConfigurationConstant)](js-apis-application-configurationConstant.md)
    - [@ohos.application.formBindingData (卡片数据绑定类)](js-apis-application-formBindingData.md)
    - [@ohos.application.formHost (FormHost)](js-apis-application-formHost.md)
    - [@ohos.application.formInfo (FormInfo)](js-apis-application-formInfo.md)
    - [@ohos.application.formProvider (FormProvider)](js-apis-application-formProvider.md)
    - [@ohos.application.missionManager (missionManager)](js-apis-application-missionManager.md)
    - [@ohos.application.Want (Want)](js-apis-application-want.md)
    - [@ohos.wantAgent (WantAgent模块)](js-apis-wantAgent.md)
  - 接口依赖的元素及定义
    - ability
      - [abilityResult](js-apis-inner-ability-abilityResult.md)
      - [connectOptions](js-apis-inner-ability-connectOptions.md)
      - [dataAbilityHelper](js-apis-inner-ability-dataAbilityHelper.md)
      - [dataAbilityOperation](js-apis-inner-ability-dataAbilityOperation.md)
      - [dataAbilityResult](js-apis-inner-ability-dataAbilityResult.md)
      - [startAbilityParameter](js-apis-inner-ability-startAbilityParameter.md)
      - [want](js-apis-inner-ability-want.md)
    - app
      - [appVersionInfo](js-apis-inner-app-appVersionInfo.md)
      - [context](js-apis-inner-app-context.md)
      - [processInfo](js-apis-inner-app-processInfo.md)
    - application
      - [abilityDelegator](js-apis-inner-application-abilityDelegator.md)
      - [abilityDelegatorArgs](js-apis-inner-application-abilityDelegatorArgs.md)
      - [abilityMonitor](js-apis-inner-application-abilityMonitor.md)
      - [AbilityRunningInfo](js-apis-inner-application-abilityRunningInfo.md)
      - [AbilityStageContext](js-apis-inner-application-abilityStageContext.md)
      - [AbilityStartCallback](js-apis-inner-application-abilityStartCallback.md)
      - [AbilityStateData](js-apis-inner-application-abilityStateData.md)
      - [abilityStageMonitor](js-apis-inner-application-abilityStageMonitor.md)
      - [ApplicationContext](js-apis-inner-application-applicationContext.md)
      - [ApplicationStateObserver](js-apis-inner-application-applicationStateObserver.md)
      - [AppStateData](js-apis-inner-application-appStateData.md)
      - [AutoFillExtensionContext](js-apis-inner-application-autoFillExtensionContext.md)
      - [AutoFillRequest](js-apis-inner-application-autoFillRequest.md)
      - [AutoFillType](js-apis-inner-application-autoFillType.md)
      - [AutoStartupCallback](js-apis-inner-application-autoStartupCallback.md)
      - [AutoStartupInfo](js-apis-inner-application-autoStartupInfo.md)
      - [BaseContext](js-apis-inner-application-baseContext.md)
      - [Context](js-apis-inner-application-context.md)
      - [ContinuableInfo](js-apis-inner-application-continuableInfo.md)
      - [ContinueCallback](js-apis-inner-application-continueCallback.md)
      - [ContinueDeviceInfo](js-apis-inner-application-continueDeviceInfo.md)
      - [ContinueMissionInfo](js-apis-inner-application-continueMissionInfo.md)
      - [ErrorObserver](js-apis-inner-application-errorObserver.md)
      - [ExtensionContext](js-apis-inner-application-extensionContext.md)
      - [ExtensionRunningInfo](js-apis-inner-application-extensionRunningInfo.md)
      - [FormExtensionContext](js-apis-inner-application-formExtensionContext.md)
      - [MissionCallbacks](js-apis-inner-application-missionCallbacks.md)
      - [MissionDeviceInfo](js-apis-inner-application-missionDeviceInfo.md)
      - [MissionInfo](js-apis-inner-application-missionInfo.md)
      - [MissionListener](js-apis-inner-application-missionListener.md)
      - [MissionParameter](js-apis-inner-application-missionParameter.md)
      - [MissionSnapshot](js-apis-inner-application-missionSnapshot.md)
      - [PageNodeInfo](js-apis-inner-application-pageNodeInfo.md)
      - [ProcessData](js-apis-inner-application-processData.md)
      - [ProcessRunningInfo](js-apis-inner-application-processRunningInfo.md)
      - [ProcessInformation](js-apis-inner-application-processInformation.md)
      - [ServiceExtensionContext](js-apis-inner-application-serviceExtensionContext.md)
      - [UIAbilityContext](js-apis-inner-application-uiAbilityContext.md)
      - [UIExtensionContext](js-apis-inner-application-uiExtensionContext.md)
      - [shellCmdResult](js-apis-inner-application-shellCmdResult.md)
      - [ViewData](js-apis-inner-application-viewData.md)
      - [WindowExtensionContext](js-apis-inner-application-windowExtensionContext.md)
    - wantAgent
      - [triggerInfo](js-apis-inner-wantAgent-triggerInfo.md)
      - [wantAgentInfo](js-apis-inner-wantAgent-wantAgentInfo.md)
  - 流转
    - [@ohos.continuation.continuationManager (continuationManager)](js-apis-continuation-continuationManager.md)
    - continuation
      - [continuationExtraParams](js-apis-continuation-continuationExtraParams.md)
      - [continuationResult](js-apis-continuation-continuationResult.md)

- 公共事件与通知
  - [系统公共事件定义](commonEventManager-definitions.md)
  - [@ohos.commonEventManager (公共事件模块)(推荐)](js-apis-commonEventManager.md)
  - [@ohos.events.emitter (Emitter)](js-apis-emitter.md)
  - [@ohos.notificationManager (NotificationManager模块)(推荐)](js-apis-notificationManager.md)
  - [@ohos.notificationSubscribe (NotificationSubscribe模块)(推荐)](js-apis-notificationSubscribe.md)
  - [@ohos.application.StaticSubscriberExtensionContext (NotificationSubscribe模块)(推荐)](js-apis-application-StaticSubscriberExtensionContext.md)
  - [系统公共事件定义 (待停用)](commonEvent-definitions.md)
  - [@ohos.commonEvent (公共事件模块)(待停用)](js-apis-commonEvent.md)
  - [@ohos.notification (Notification模块)(待停用)](js-apis-notification.md)
  - application
    - [EventHub](js-apis-inner-application-eventHub.md)
  - commonEvent
    - [CommonEventData](js-apis-inner-commonEvent-commonEventData.md)
    - [CommonEventPublishData](js-apis-inner-commonEvent-commonEventPublishData.md)
    - [CommonEventSubscriber](js-apis-inner-commonEvent-commonEventSubscriber.md)
    - [CommonEventSubscribeInfo](js-apis-inner-commonEvent-commonEventSubscribeInfo.md)
  - notification
    - [NotificationActionButton](js-apis-inner-notification-notificationActionButton.md)
    - [NotificationCommonDef](js-apis-inner-notification-notificationCommonDef.md)
    - [NotificationContent](js-apis-inner-notification-notificationContent.md)
    - [NotificationFlags](js-apis-inner-notification-notificationFlags.md)
    - [NotificationRequest](js-apis-inner-notification-notificationRequest.md)
    - [NotificationSlot](js-apis-inner-notification-notificationSlot.md)
    - [NotificationSorting](js-apis-inner-notification-notificationSorting.md)
    - [NotificationSortingMap](js-apis-inner-notification-notificationSortingMap.md)
    - [NotificationSubscribeInfo](js-apis-inner-notification-notificationSubscribeInfo.md)
    - [NotificationSubscriber](js-apis-inner-notification-notificationSubscriber.md)
    - [NotificationTemplate](js-apis-inner-notification-notificationTemplate.md)
    - [NotificationUserInput](js-apis-inner-notification-notificationUserInput.md)
  - 公共事件定义
    - [元能力子系统公共事件定义](common_event/commonEvent-ability.md)
    - [包管理子系统公共事件定义](common_event/commonEvent-bundleManager.md)
    - [通知服务公共事件定义](common_event/commonEvent-ans.md)
    - [资源调度子系统公共事件定义](common_event/commonEvent-resourceschedule.md)
    - [窗口管理子系统公共事件定义](common_event/commonEvent-window.md)
    - [网络管理子系统公共事件定义](common_event/commonEvent-netmanager.md)
    - [短信应用公共事件定义](common_event/commonEvent-mms.md)
    - [电话服务子系统公共事件定义](common_event/commonEvent-telephony.md)
    - [电源管理子系统公共事件定义](common_event/commonEvent-powermgr.md)
    - [NFC子系统公共事件定义](common_event/commonEvent-nfc.md)
    - [Wifi子系统公共事件定义](common_event/commonEvent-wifi.md)
    - [USB子系统公共事件定义](common_event/commonEvent-usb.md)
    - [文件管理子系统公共事件定义](common_event/commonEvent-filemanagement.md)
    - [主题框架子系统-锁屏管理公共事件定义](common_event/commonEvent-screenlock.md)
    - [时间时区子系统公共事件定义](common_event/commonEvent-time.md)
    - [帐号子系统公共事件定义](common_event/commonEvent-account.md)

- 包管理
  - [@ohos.bundle.appControl (appControl模块)](js-apis-appControl.md)
  - [@ohos.bundle.bundleManager (bundleManager模块)](js-apis-bundleManager.md)
  - [@ohos.bundle.bundleResourceManager (bundleResourceManager模块)](js-apis-bundleResourceManager.md)
  - [@ohos.bundle.bundleMonitor (bundleMonitor模块)](js-apis-bundleMonitor.md)
  - [@ohos.bundle.defaultAppManager (默认应用管理)](js-apis-defaultAppManager.md)
  - [@ohos.bundle.distributedBundleManager (distributedBundleManager模块)](js-apis-distributedBundleManager.md)
  - [@ohos.bundle.freeInstall (freeInstall模块)](js-apis-freeInstall.md)
  - [@ohos.bundle.installer (installer模块)](js-apis-installer.md)
  - [@ohos.bundle.launcherBundleManager (launcherBundleManager模块)](js-apis-launcherBundleManager.md)
  - [@ohos.bundle.overlay (overlay模块)](js-apis-overlay.md)
  - [@ohos.zlib (Zip模块)](js-apis-zlib.md)
  - bundleManager
    - [abilityInfo](js-apis-bundleManager-abilityInfo.md)
    - [applicationInfo](js-apis-bundleManager-applicationInfo.md)
    - [AppProvisionInfo](js-apis-bundleManager-AppProvisionInfo.md)
    - [bundleInfo](js-apis-bundleManager-bundleInfo.md)
    - [BundlePackInfo](js-apis-bundleManager-BundlePackInfo.md)
    - [BusinessAbilityInfo](js-apis-bundleManager-businessAbilityInfo.md)
    - [dispatchInfo](js-apis-bundleManager-dispatchInfo.md)
    - [elementName](js-apis-bundleManager-elementName.md)
    - [extensionAbilityInfo](js-apis-bundleManager-extensionAbilityInfo.md)
    - [hapModuleInfo](js-apis-bundleManager-hapModuleInfo.md)
    - [launcherAbilityInfo](js-apis-bundleManager-launcherAbilityInfo.md)
    - [LauncherAbilityResourceInfo](js-apis-bundleManager-LauncherAbilityResourceInfo.md)
    - [metadata](js-apis-bundleManager-metadata.md)
    - [OverlayModuleInfo](js-apis-bundleManager-overlayModuleInfo.md)
    - [permissionDef](js-apis-bundleManager-permissionDef.md)
    - [remoteAbilityInfo](js-apis-bundleManager-remoteAbilityInfo.md)
    - [BundleResourceInfo](js-apis-bundleManager-BundleResourceInfo.md)
    - [SharedBundleInfo](js-apis-bundleManager-sharedBundleInfo.md)
    - [shortcutInfo](js-apis-bundleManager-shortcutInfo.md)

- UI界面
  - [@ohos.animator (动画)](js-apis-animator.md)
  - [@ohos.arkui.componentSnapshot (组件截图)](js-apis-arkui-componentSnapshot.md)
  - [@ohos.arkui.componentUtils (componentUtils)](js-apis-arkui-componentUtils.md)
  - [@ohos.arkui.dragController (DragController)](js-apis-arkui-dragController.md)
  - [@ohos.arkui.drawableDescriptor (DrawableDescriptor)](js-apis-arkui-drawableDescriptor.md)
  - [@ohos.arkui.inspector (布局回调)](js-apis-arkui-inspector.md)
  - [@ohos.arkui.observer (无感监听)](js-apis-arkui-observer.md)
  - [@ohos.arkui.performanceMonitor (性能监测)](js-apis-arkui-performancemonitor.md)
  - [@ohos.arkui.UIContext (UIContext)](js-apis-arkui-UIContext.md)
  - [@ohos.curves (插值计算)](js-apis-curve.md)
  - [@ohos.font (注册自定义字体)](js-apis-font.md)
  - [@ohos.matrix4 (矩阵变换)](js-apis-matrix4.md)
  - [@ohos.measure (文本计算)](js-apis-measure.md)
  - [@ohos.mediaquery (媒体查询)](js-apis-mediaquery.md)
  - [@ohos.pluginComponent (PluginComponentManager)](js-apis-plugincomponent.md)
  - [@ohos.promptAction (弹窗)](js-apis-promptAction.md)
  - [@ohos.router (页面路由)](js-apis-router.md)
  - [@ohos.uiAppearance (用户界面外观)](js-apis-uiappearance.md)

- 图形图像
  - [@ohos.animation.windowAnimationManager (窗口动画管理)](js-apis-windowAnimationManager.md)
  - [@ohos.application.WindowExtensionAbility (窗口扩展能力)](js-apis-application-windowExtensionAbility.md)
  - [@ohos.display (屏幕属性)](js-apis-display.md)
  - [@ohos.effectKit (图像效果)](js-apis-effectKit.md)
  - [@ohos.graphics.colorSpaceManager (色彩管理)](js-apis-colorSpaceManager.md)
  - [@ohos.PiPWindow (画中画窗口)](js-apis-pipWindow.md)
  - [@ohos.screen (屏幕)](js-apis-screen.md)
  - [@ohos.screenshot (屏幕截图)](js-apis-screenshot.md)
  - [@ohos.window (窗口)](js-apis-window.md)

- 媒体
  - [@ohos.app.ability.MediaControlExtensionAbility (播控扩展能力)](js-apis-app-ability-MediaControlExtensionAbility.md)
  - [@ohos.multimedia.audio (音频管理)](js-apis-audio.md)
  - [@ohos.multimedia.avsession (媒体会话管理)](js-apis-avsession.md)
  - [@ohos.multimedia.camera (相机管理)](js-apis-camera.md)
  - [@ohos.multimedia.image (图片处理)](js-apis-image.md)
  - [@ohos.multimedia.media (媒体服务)](js-apis-media.md)
  - [@ohos.multimedia.systemSoundManager (系统声音管理)](js-apis-systemSoundManager.md)
  - application
    - [MediaControlExtensionContext (播控扩展能力上下文)](js-apis-inner-application-MediaControlExtensionContext.md)
  - multimedia
    - [ringtonePlayer (铃声播放器)](js-apis-inner-multimedia-ringtonePlayer.md)
    - [soundPool (音频池)](js-apis-inner-multimedia-soundPool.md)

- 资源管理
  - [@ohos.i18n (国际化-I18n)](js-apis-i18n.md)
  - [@ohos.intl (国际化-Intl)](js-apis-intl.md)
  - [@ohos.resourceManager (资源管理)](js-apis-resource-manager.md)

- 后台任务(Background Task)
  - [@ohos.distributedMissionManager (分布式任务管理)](js-apis-distributedMissionManager.md)
  - [@ohos.reminderAgentManager (后台代理提醒)](js-apis-reminderAgentManager.md)
  - [@ohos.resourceschedule.backgroundTaskManager (后台任务管理)](js-apis-resourceschedule-backgroundTaskManager.md)
  - [@ohos.resourceschedule.workScheduler (延迟任务调度)](js-apis-resourceschedule-workScheduler.md)
  - [@ohos.resourceschedule.usageStatistics (设备使用信息统计)](js-apis-resourceschedule-deviceUsageStatistics.md)
  - [@ohos.WorkSchedulerExtensionAbility (延迟任务调度回调)](js-apis-WorkSchedulerExtensionAbility.md)
  - application
    - [WorkSchedulerExtensionContext](js-apis-inner-application-WorkSchedulerExtensionContext.md)

- 安全
  - [@ohos.abilityAccessCtrl (程序访问控制管理)](js-apis-abilityAccessCtrl.md)
  - [@ohos.dlpPermission (数据防泄漏)](js-apis-dlppermission.md)
  - [@ohos.privacyManager (隐私管理)](js-apis-privacyManager.md)
  - [@ohos.security.cert (证书模块)](js-apis-cert.md)
  - [@ohos.security.certManager (证书管理)](js-apis-certManager.md)
  - [@ohos.security.cryptoFramework (加解密算法库框架)](js-apis-cryptoFramework.md)
  - [@ohos.security.huks (通用密钥库系统)](js-apis-huks.md)
  - [@ohos.userIAM.faceAuth (人脸认证)](js-apis-useriam-faceauth.md)
  - [@ohos.userIAM.userAuth (用户认证)](js-apis-useriam-userauth.md)
  - security
    - [PermissionRequestResult](js-apis-permissionrequestresult.md)
- 数据管理
  - [@ohos.data.cloudData (端云协同)](js-apis-data-cloudData.md)
  - [@ohos.data.dataAbility (DataAbility谓词)](js-apis-data-ability.md)
  - [@ohos.data.dataShare (数据共享)](js-apis-data-dataShare.md)
  - [@ohos.data.dataSharePredicates (数据共享谓词)](js-apis-data-dataSharePredicates.md)
  - [@ohos.data.dataShareResultSet (数据共享结果集)](js-apis-data-DataShareResultSet.md)
  - [@ohos.data.distributedDataObject (分布式数据对象)](js-apis-data-distributedobject.md)
  - [@ohos.data.distributedKVStore (分布式键值数据库)](js-apis-distributedKVStore.md)
  - [@ohos.data.preferences (用户首选项)](js-apis-data-preferences.md)
  - [@ohos.data.relationalStore (关系型数据库)](js-apis-data-relationalStore.md)
  - [@ohos.data.unifiedDataChannel (标准化数据通路)](js-apis-data-unifiedDataChannel.md)
  - [@ohos.data.uniformTypeDescriptor (标准化数据定义与描述)](js-apis-data-uniformTypeDescriptor.md)
  - [@ohos.data.ValuesBucket (数据集)](js-apis-data-valuesBucket.md)

- 文件管理
  - [@ohos.application.BackupExtensionAbility (备份恢复扩展能力)](js-apis-application-backupExtensionAbility.md)
  - [@ohos.file.backup (备份恢复)](js-apis-file-backup.md)
  - [@ohos.file.cloudSync (端云同步能力)](js-apis-file-cloudsync.md)
  - [@ohos.file.cloudSyncManager (端云同步管理)](js-apis-file-cloudsyncmanager.md)
  - [@ohos.file.environment (目录环境能力)](js-apis-file-environment.md)
  - [@ohos.file.fileAccess (公共文件访问与管理)](js-apis-fileAccess.md)
  - [@ohos.file.fileExtensionInfo (公共文件访问与管理属性信息)](js-apis-fileExtensionInfo.md)
  - [@ohos.file.fileuri (文件URI)](js-apis-file-fileuri.md)
  - [@ohos.file.fs (文件管理)](js-apis-file-fs.md)
  - [@ohos.file.hash (文件哈希处理)](js-apis-file-hash.md)
  - [@ohos.file.photoAccessHelper (相册管理模块)](js-apis-photoAccessHelper.md)
  - [@ohos.file.picker (选择器)](js-apis-file-picker.md)
  - [@ohos.file.recent(最近访问列表)](js-apis-file-recent.md)
  - [@ohos.file.securityLabel (数据标签)](js-apis-file-securityLabel.md)
  - [@ohos.file.statvfs (文件系统空间统计)](js-apis-file-statvfs.md)
  - [@ohos.file.storageStatistics (应用空间统计)](js-apis-file-storage-statistics.md)
  - [@ohos.file.trash (回收站)](js-apis-file-trash.md)
  - [@ohos.file.volumeManager (卷管理)](js-apis-file-volumemanager.md)
  - [@ohos.filemanagement.userFileManager (用户数据管理)](js-apis-userFileManager.md)
  - [@ohos.fileshare (文件分享)](js-apis-fileShare.md)

- AI
  - [@ohos.ai.mindSporeLite (推理能力)](js-apis-mindSporeLite.md)
  - [@ohos.ai.intelligentVoice (智能语音)](js-apis-intelligentVoice.md)

- 电话服务
  - [@ohos.contact (联系人)](js-apis-contact.md)
  - [@ohos.telephony.call (拨打电话)](js-apis-call.md)
  - [@ohos.telephony.data (蜂窝数据)](js-apis-telephony-data.md)
  - [@ohos.telephony.observer (observer)](js-apis-observer.md)
  - [@ohos.telephony.radio (网络搜索)](js-apis-radio.md)
  - [@ohos.telephony.sim (SIM卡管理)](js-apis-sim.md)
  - [@ohos.telephony.sms (短信服务)](js-apis-sms.md)

- 网络管理
  - [@ohos.net.connection (网络连接管理)](js-apis-net-connection.md)
  - [@ohos.net.ethernet (以太网连接管理)](js-apis-net-ethernet.md)
  - [@ohos.net.http (数据请求)](js-apis-http.md)
  - [@ohos.net.policy (网络策略管理)](js-apis-net-policy.md)
  - [@ohos.net.mdns (MDNS管理)](js-apis-net-mdns.md)
  - [@ohos.net.sharing (网络共享管理)](js-apis-net-sharing.md)
  - [@ohos.net.socket (Socket连接)](js-apis-socket.md)
  - [@ohos.net.statistics (流量管理)](js-apis-net-statistics.md)
  - [@ohos.net.vpn (VPN管理)](js-apis-net-vpn.md)
  - [@ohos.net.webSocket (WebSocket连接)](js-apis-webSocket.md)
  - [@ohos.request (上传下载)](js-apis-request.md)

- 通信与连接
  - [@ohos.bluetooth.a2dp(蓝牙a2dp模块)(推荐)](js-apis-bluetooth-a2dp.md)
  - [@ohos.bluetooth.access(蓝牙access模块)(推荐)](js-apis-bluetooth-access.md)
  - [@ohos.bluetooth.baseProfile(蓝牙baseProfile模块)(推荐)](js-apis-bluetooth-baseProfile.md)
  - [@ohos.bluetooth.ble(蓝牙ble模块)(推荐)](js-apis-bluetooth-ble.md)
  - [@ohos.bluetooth.connection(蓝牙connection模块)(推荐)](js-apis-bluetooth-connection.md)
  - [@ohos.bluetooth.constant(蓝牙constant模块)(推荐)](js-apis-bluetooth-constant.md)
  - [@ohos.bluetooth.hfp(蓝牙hfp模块)(推荐)](js-apis-bluetooth-hfp.md)
  - [@ohos.bluetooth.hid(蓝牙hid模块)(推荐)](js-apis-bluetooth-hid.md)
  - [@ohos.bluetooth.pan(蓝牙pan模块)(推荐)](js-apis-bluetooth-pan.md)
  - [@ohos.bluetooth.socket(蓝牙socket模块)(推荐)](js-apis-bluetooth-socket.md)
  - [@ohos.bluetooth (蓝牙)(待停用)](js-apis-bluetooth.md)
  - [@ohos.bluetoothManager (蓝牙)(待停用)](js-apis-bluetoothManager.md)
  - [@ohos.connectedTag (有源标签)](js-apis-connectedTag.md)
  - [@ohos.nfc.cardEmulation (标准NFC-cardEmulation)](js-apis-cardEmulation.md)
  - [@ohos.nfc.controller (标准NFC)](js-apis-nfcController.md)
  - [@ohos.nfc.tag (标准NFC-Tag)](js-apis-nfcTag.md)
  - [@ohos.rpc (RPC通信)](js-apis-rpc.md)
  - [@ohos.secureElement (安全单元的通道管理)](js-apis-secureElement.md)
  - [@ohos.wifiManager (WLAN)(推荐)](js-apis-wifiManager.md)
  - [@ohos.wifiManagerExt (WLAN扩展接口)(推荐)](js-apis-wifiManagerExt.md)
  - [@ohos.wifi (WLAN)(待停用)](js-apis-wifi.md)
  - [@ohos.wifiext (WLAN扩展接口)(待停用)](js-apis-wifiext.md)
  - tag
    - [nfctech (标准NFC-Tag Nfc 技术)](js-apis-nfctech.md)
    - [tagSession (标准NFC-Tag TagSession)](js-apis-tagSession.md)

- 系统基础能力
  - [@ohos.accessibility (辅助功能)](js-apis-accessibility.md)
  - [@ohos.accessibility.config (系统辅助功能配置)](js-apis-accessibility-config.md)
  - [@ohos.accessibility.GesturePath (手势路径)](js-apis-accessibility-GesturePath.md)
  - [@ohos.accessibility.GesturePoint (手势触摸点)](js-apis-accessibility-GesturePoint.md)
  - [@ohos.application.AccessibilityExtensionAbility (辅助功能扩展能力)](js-apis-application-accessibilityExtensionAbility.md)
  - [@ohos.base (公共回调信息)](js-apis-base.md)
  - [@ohos.faultLogger (故障日志获取)](js-apis-faultLogger.md)
  - [@ohos.hichecker (检测模式)](js-apis-hichecker.md)
  - [@ohos.hidebug (Debug调试)](js-apis-hidebug.md)
  - [@ohos.hilog (HiLog日志打印)](js-apis-hilog.md)
  - [@ohos.hiSysEvent (系统事件打点)](js-apis-hisysevent.md)
  - [@ohos.hiTraceChain (分布式跟踪)](js-apis-hitracechain.md)
  - [@ohos.hiTraceMeter (性能打点)](js-apis-hitracemeter.md)
  - [@ohos.hiviewdfx.hiAppEvent (应用事件打点)](js-apis-hiviewdfx-hiappevent.md)
  - [@ohos.inputMethod (输入法框架)](js-apis-inputmethod.md)
  - [@ohos.inputMethodEngine (输入法服务)](js-apis-inputmethodengine.md)
  - [@ohos.InputMethodExtensionAbility (InputMethodExtensionAbility)](js-apis-inputmethod-extension-ability.md)
  - [@ohos.InputMethodExtensionContext (InputMethodExtensionContext)](js-apis-inputmethod-extension-context.md)
  - [@ohos.inputMethod.Panel (输入法面板)](js-apis-inputmethod-panel.md)
  - [@ohos.inputMethodList (输入法切换列表控件）](js-apis-inputmethodlist.md)
  - [@ohos.InputMethodSubtype (输入法子类型)](js-apis-inputmethod-subtype.md)
  - [@ohos.logLibrary (维测日志获取)](js-apis-loglibrary.md)
  - [@ohos.pasteboard (剪贴板)](js-apis-pasteboard.md)
  - [@ohos.print (打印)](js-apis-print.md)
  - [@ohos.screenLock (锁屏管理)](js-apis-screen-lock.md)
  - [@ohos.systemDateTime (系统时间、时区)](js-apis-system-date-time.md)
  - [@ohos.systemTimer (系统定时器)](js-apis-system-timer.md)
  - [@ohos.wallpaper (壁纸)](js-apis-wallpaper.md)
  - [@ohos.WallpaperExtensionAbility (WallpaperExtensionAbility)](js-apis-WallpaperExtensionAbility.md)
  - [@ohos.web.webview (Webview)](js-apis-webview.md)
  - [@ohos.telephony.vcard (VCard)](js-apis-vcard.md)
  - [Console (控制台)](js-apis-logs.md)
  - [Timer (定时器)](js-apis-timer.md)
  - [syscap (系统能力)](js-apis-syscap.md)
  - application
    - [AccessibilityExtensionContext (辅助功能扩展上下文)](js-apis-inner-application-accessibilityExtensionContext.md)

- 设备管理
  - [@ohos.app.ability.DriverExtensionAbility (DriverExtensionAbility)](js-apis-app-ability-driverExtensionAbility.md)
  - [@ohos.batteryInfo (电量信息)](js-apis-battery-info.md)
  - [@ohos.batteryStatistics (耗电统计)](js-apis-batteryStatistics.md)
  - [@ohos.brightness (屏幕亮度)](js-apis-brightness.md)
  - [@ohos.calendarManager (日程管理)](js-apis-calendarManager.md)
  - [@ohos.charger (充电类型)](js-apis-charger.md)
  - [@ohos.cooperate (键鼠穿越)](js-apis-devicestatus-cooperate.md)
  - [@ohos.deviceAttest (设备证明)](js-apis-deviceAttest.md)
  - [@ohos.deviceStatus.dragInteraction（拖拽）](js-apis-devicestatus-draginteraction.md)
  - [@ohos.deviceInfo (设备信息)](js-apis-device-info.md)
  - [@ohos.distributedDeviceManager (设备管理)](js-apis-distributedDeviceManager.md)
  - [@ohos.distributedHardware.deviceManager (设备管理)](js-apis-device-manager.md)
  - [@ohos.distributedHardware.hardwareManager (分布式硬件管理)](js-apis-distributedHardwareManager.md)
  - [@ohos.driver.deviceManager (外设管理)](js-apis-driver-deviceManager.md)
  - [@ohos.geoLocationManager (位置服务)](js-apis-geoLocationManager.md)
  - [@ohos.multimodalInput.gestureEvent (手势事件)](js-apis-multimodalinput-gestureevent.md)
  - [@ohos.multimodalInput.inputConsumer (组合按键)](js-apis-inputconsumer.md)
  - [@ohos.multimodalInput.inputDevice (输入设备)](js-apis-inputdevice.md)
  - [@ohos.multimodalInput.inputDeviceCooperate (键鼠穿越)(待停用)](js-apis-cooperate.md)
  - [@ohos.multimodalInput.inputEvent (输入事件)](js-apis-inputevent.md)
  - [@ohos.multimodalInput.inputEventClient (按键注入)](js-apis-inputeventclient.md)
  - [@ohos.multimodalInput.inputMonitor (输入监听)](js-apis-inputmonitor.md)
  - [@ohos.multimodalInput.intentionCode (意图事件)](js-apis-intentioncode.md)
  - [@ohos.multimodalInput.keyCode (键值)](js-apis-keycode.md)
  - [@ohos.multimodalInput.keyEvent (按键输入事件)](js-apis-keyevent.md)
  - [@ohos.multimodalInput.mouseEvent (鼠标输入事件)](js-apis-mouseevent.md)
  - [@ohos.multimodalInput.pointer (鼠标指针)](js-apis-pointer.md)
  - [@ohos.multimodalInput.touchEvent (触摸输入事件)](js-apis-touchevent.md)
  - [@ohos.multimodalInput.shortKey(快捷键)](js-apis-shortKey.md)
  - [@ohos.power (系统电源管理)](js-apis-power.md)
  - [@ohos.resourceschedule.deviceStandby (设备待机模块)](js-apis-resourceschedule-deviceStandby.md)
  - [@ohos.runningLock (Runninglock锁)](js-apis-runninglock.md)
  - [@ohos.sensor (传感器)](js-apis-sensor.md)
  - [@ohos.settings (设置数据项名称)](js-apis-settings.md)
  - [@ohos.stationary (设备状态感知框架)](js-apis-stationary.md)
  - [@ohos.systemCapability (系统能力)](js-apis-system-capability.md)
  - [@ohos.systemParameterEnhance (系统参数)](js-apis-system-parameterEnhance.md)
  - [@ohos.thermal (热管理)](js-apis-thermal.md)
  - [@ohos.update (升级)](js-apis-update.md)
  - [@ohos.usbManager (USB管理)](js-apis-usbManager.md)
  - [@ohos.vibrator (振动)](js-apis-vibrator.md)
  - application
    - [DriverExtensionContext](js-apis-inner-application-driverExtensionContext.md)
  
- 帐号管理
  - [@ohos.account.appAccount (应用帐号管理)](js-apis-appAccount.md)
  - [@ohos.account.distributedAccount (分布式帐号管理)](js-apis-distributed-account.md)
  - [@ohos.account.osAccount (系统帐号管理)](js-apis-osAccount.md)

- 定制管理
  - [@ohos.configPolicy (配置策略)](js-apis-configPolicy.md)

- 企业设备管理
  - [企业设备管理概述 (仅对系统应用开放)](enterpriseDeviceManagement-overview.md)
  - [@ohos.enterprise.accountManager (帐户管理)](js-apis-enterprise-accountManager.md)
  - [@ohos.enterprise.adminManager (企业设备管理)](js-apis-enterprise-adminManager.md)
  - [@ohos.enterprise.applicationManager (应用管理)](js-apis-enterprise-applicationManager.md)
  - [@ohos.enterprise.browser (浏览器管理)](js-apis-enterprise-browser.md)
  - [@ohos.enterprise.bundleManager (包管理)](js-apis-enterprise-bundleManager.md)
  - [@ohos.enterprise.dateTimeManager (系统时间管理)](js-apis-enterprise-dateTimeManager.md)
  - [@ohos.enterprise.deviceControl (设备控制管理)](js-apis-enterprise-deviceControl.md)
  - [@ohos.enterprise.deviceInfo (设备信息管理)](js-apis-enterprise-deviceInfo.md)
  - [@ohos.enterprise.deviceSettings (设备设置管理)](js-apis-enterprise-deviceSettings.md)
  - [@ohos.enterprise.EnterpriseAdminExtensionAbility (企业设备管理扩展能力)](js-apis-EnterpriseAdminExtensionAbility.md)
  - [@ohos.enterprise.networkManager (网络管理)](js-apis-enterprise-networkManager.md)
  - [@ohos.enterprise.restrictions (限制类策略)](js-apis-enterprise-restrictions.md)
  - [@ohos.enterprise.securityManager (安全管理)](js-apis-enterprise-securityManager.md)
  - [@ohos.enterprise.bluetoothManager (蓝牙管理)](js-apis-enterprise-bluetoothManager.md)
  - [@ohos.enterprise.systemManager (系统管理)](js-apis-enterprise-systemManager.md)
  - [@ohos.enterprise.usbManager (USB管理)](js-apis-enterprise-usbManager.md)
  - [@ohos.enterprise.wifiManager (WiFi管理)](js-apis-enterprise-wifiManager.md)

- 语言基础类库
  - [@ohos.buffer (Buffer)](js-apis-buffer.md)
  - [@ohos.convertxml (xml转换JavaScript)](js-apis-convertxml.md)
  - [@ohos.process (获取进程相关的信息)](js-apis-process.md)
  - [@ohos.taskpool (启动任务池)](js-apis-taskpool.md)
  - [@ohos.uri (URI字符串解析)](js-apis-uri.md)
  - [@ohos.url (URL字符串解析)](js-apis-url.md)
  - [@ohos.util (util工具函数)](js-apis-util.md)
  - [@ohos.util.ArrayList (线性容器ArrayList)](js-apis-arraylist.md)
  - [@ohos.util.Deque (线性容器Deque)](js-apis-deque.md)
  - [@ohos.util.HashMap (非线性容器HashMap)](js-apis-hashmap.md)
  - [@ohos.util.HashSet (非线性容器HashSet)](js-apis-hashset.md)
  - [@ohos.util.LightWeightMap (非线性容器LightWeightMap)](js-apis-lightweightmap.md)
  - [@ohos.util.LightWeightSet (非线性容器LightWeightSet)](js-apis-lightweightset.md)
  - [@ohos.util.LinkedList (线性容器LinkedList)](js-apis-linkedlist.md)
  - [@ohos.util.List (线性容器List)](js-apis-list.md)
  - [@ohos.util.PlainArray (非线性容器PlainArray)](js-apis-plainarray.md)
  - [@ohos.util.Queue (线性容器Queue)](js-apis-queue.md)
  - [@ohos.util.Stack (线性容器Stack)](js-apis-stack.md)
  - [@ohos.util.TreeMap (非线性容器TreeMap)](js-apis-treemap.md)
  - [@ohos.util.TreeSet (非线性容器TreeSet)](js-apis-treeset.md)
  - [@ohos.worker (启动一个Worker)](js-apis-worker.md)
  - [@ohos.xml (xml解析与生成)](js-apis-xml.md)

- 应用服务
  - [@ohos.identifier.oaid (广告标识服务)](js-apis-oaid.md)

- 测试
  - [@ohos.application.testRunner (TestRunner)](js-apis-application-testRunner.md)
  - [@ohos.uitest (UiTest)](js-apis-uitest.md)

- 已停止维护的接口
  - [@ohos.backgroundTaskManager (后台任务管理)](js-apis-backgroundTaskManager.md)
  - [@ohos.bundle (Bundle模块)](js-apis-Bundle.md)
  - [@ohos.bundle.innerBundleManager (innerBundleManager模块)](js-apis-Bundle-InnerBundleManager.md)
  - [@ohos.bundleState (设备使用信息统计)](js-apis-deviceUsageStatistics.md)
  - [@ohos.bytrace (性能打点)](js-apis-bytrace.md)
  - [@ohos.data.distributedData (分布式数据管理)](js-apis-distributed-data.md)
  - [@ohos.data.storage (轻量级存储)](js-apis-data-storage.md)
  - [@ohos.data.rdb (关系型数据库)](js-apis-data-rdb.md)
  - [@ohos.distributedBundle (分布式包管理)](js-apis-Bundle-distributedBundle.md)
  - [@ohos.document (文件交互)](js-apis-document.md)
  - [@ohos.fileio (文件管理)](js-apis-fileio.md)
  - [@ohos.geolocation (位置服务)](js-apis-geolocation.md)
  - [@ohos.hiAppEvent (应用打点)](js-apis-hiappevent.md)
  - [@ohos.multimedia.medialibrary (媒体库管理)](js-apis-medialibrary.md)
  - [@ohos.prompt (弹窗)](js-apis-prompt.md)
  - [@ohos.reminderAgent (后台代理提醒)](js-apis-reminderAgent.md)
  - [@ohos.statfs (statfs)](js-apis-statfs.md)
  - [@ohos.systemParameter (系统属性)](js-apis-system-parameter.md)
  - [@ohos.systemTime (系统时间、时区)](js-apis-system-time.md)
  - [@ohos.usb (USB管理)](js-apis-usb-deprecated.md)
  - [@ohos.util.Vector (线性容器Vector)](js-apis-vector.md)
  - [@system.app (应用上下文)](js-apis-system-app.md)
  - [@system.battery (电量信息)](js-apis-system-battery.md)
  - [@system.bluetooth (蓝牙)](js-apis-system-bluetooth.md)
  - [@system.brightness (屏幕亮度)](js-apis-system-brightness.md)
  - [@system.cipher (加密算法)](js-apis-system-cipher.md)
  - [@system.configuration (应用配置)](js-apis-system-configuration.md)
  - [@system.device (设备信息)](js-apis-system-device.md)
  - [@system.fetch (数据请求)](js-apis-system-fetch.md)
  - [@system.file (文件存储)](js-apis-system-file.md)
  - [@system.geolocation (地理位置)](js-apis-system-location.md)
  - [@system.mediaquery (媒体查询)](js-apis-system-mediaquery.md)
  - [@system.network (网络状态)](js-apis-system-network.md)
  - [@system.notification (通知消息)](js-apis-system-notification.md)
  - [@system.package (应用管理)](js-apis-system-package.md)
  - [@system.prompt (弹窗)](js-apis-system-prompt.md)
  - [@system.request (上传下载)](js-apis-system-request.md)
  - [@system.router (页面路由)](js-apis-system-router.md)
  - [@system.sensor (传感器)](js-apis-system-sensor.md)
  - [@system.storage (数据存储)](js-apis-system-storage.md)
  - [@system.vibrator (振动)](js-apis-system-vibrate.md)
  - bundle
    - [abilityInfo](js-apis-bundle-AbilityInfo.md)
    - [applicationInfo](js-apis-bundle-ApplicationInfo.md)
    - [bundleInfo](js-apis-bundle-BundleInfo.md)
    - [bundleInstaller](js-apis-bundle-BundleInstaller.md)
    - [bundleStatusCallback](js-apis-Bundle-BundleStatusCallback.md)
    - [customizeData](js-apis-bundle-CustomizeData.md)
    - [elementName](js-apis-bundle-ElementName.md)
    - [hapModuleInfo](js-apis-bundle-HapModuleInfo.md)
    - [launcherAbilityInfo](js-apis-bundle-LauncherAbilityInfo.md)
    - [moduleInfo](js-apis-bundle-ModuleInfo.md)
    - [PermissionDef](js-apis-bundle-PermissionDef.md)
    - [remoteAbilityInfo](js-apis-bundle-remoteAbilityInfo.md)
    - [shortcutInfo](js-apis-bundle-ShortcutInfo.md)
  - data/rdb
    - [resultSet (结果集)](js-apis-data-resultset.md)
