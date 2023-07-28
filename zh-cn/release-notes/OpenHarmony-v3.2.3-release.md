# OpenHarmony 3.2.3 Release


## 版本概述

当前版本在OpenHarmony 3.2.2 Release的基础上，修复了内存泄漏及linux kernel等开源组件的安全漏洞，增强了系统安全性。修复了部分系统稳定性的issue，增强了系统稳定性。更新配套的SDK版本。


## 配套关系

  **表1** 版本软件和工具配套关系

| 软件                              | 版本                                             | 备注                                                         |
| --------------------------------- | ------------------------------------------------ | ------------------------------------------------------------ |
| OpenHarmony                       | 3.2.3 Release                                    | NA                                                           |
| Public SDK                        | Ohos_sdk_public 3.2.14.5 (API Version 9 Release) | 面向应用开发者提供，不包含需要使用系统权限的系统接口。通过DevEco Studio默认获取的SDK为Public SDK。 |
| HUAWEI DevEco Studio（可选）      | 3.1 Release                                      | OpenHarmony应用开发推荐使用。<br />[点击此处获取](https://developer.harmonyos.com/cn/develop/deveco-studio#download) |
| HUAWEI DevEco Device Tool（可选） | 3.1 Release                                      | OpenHarmony智能设备集成开发环境推荐使用。<br />[点击此处获取](https://device.harmonyos.com/cn/develop/ide/) |

## 源码获取


### 前提条件

1. 注册码云gitee帐号。

2. 注册码云SSH公钥，请参考[码云帮助中心](https://gitee.com/help/articles/4191)。

3. 安装[git客户端](https://gitee.com/link?target=https%3A%2F%2Fgit-scm.com%2Fbook%2Fzh%2Fv2%2F%25E8%25B5%25B7%25E6%25AD%25A5-%25E5%25AE%2589%25E8%25A3%2585-Git)和[git-lfs](https://gitee.com/vcs-all-in-one/git-lfs?_from=gitee_search#downloading)并配置用户信息。
  
   ```
   git config --global user.name "yourname"
   git config --global user.email "your-email-address"
   git config --global credential.helper store
   ```

4. 安装码云repo工具，可以执行如下命令。
  
   ```
   curl -s https://gitee.com/oschina/repo/raw/fork_flow/repo-py3 > /usr/local/bin/repo  #如果没有权限，可下载至其他目录，并将其配置到环境变量中chmod a+x /usr/local/bin/repo
   pip3 install -i https://repo.huaweicloud.com/repository/pypi/simple requests
   ```


### 通过repo获取

**方式一（推荐）**

通过repo + ssh 下载（需注册公钥，请参考[码云帮助中心](https://gitee.com/help/articles/4191)）。

 ```
 repo init -u git@gitee.com:openharmony/manifest.git -b refs/tags/OpenHarmony-v3.2.3-Release --no-repo-verify
 repo sync -c
 repo forall -c 'git lfs pull'
 ```

**方式二**

通过repo + https 下载。

从版本发布Tag节点获取源码。可获取与版本发布时完全一致的源码。
 ```
 repo init -u https://gitee.com/openharmony/manifest -b refs/tags/OpenHarmony-v3.2.3-Release --no-repo-verify
 repo sync -c
 repo forall -c 'git lfs pull'
 ```

### 从镜像站点获取

  **表2** 获取源码路径

| 版本源码                              | **版本信息**  | **下载站点**                                                 | **SHA256校验码**                                             |
| ------------------------------------- | ------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| 全量代码（标准、轻量和小型系统）      | 3.2.3 Release | [站点](https://repo.huaweicloud.com/openharmony/os/3.2.3/code-v3.2.3-Release.tar.gz) | [SHA256校验码](https://repo.huaweicloud.com/openharmony/os/3.2.3/code-v3.2.3-Release.tar.gz.sha256) |
| Hi3861解决方案（二进制）              | 3.2.3 Release | [站点](https://repo.huaweicloud.com/openharmony/os/3.2.3/hispark_pegasus.tar.gz) | [SHA256校验码](https://repo.huaweicloud.com/openharmony/os/3.2.3/hispark_pegasus.tar.gz.sha256) |
| Hi3516解决方案-LiteOS（二进制）       | 3.2.3 Release | [站点](https://repo.huaweicloud.com/openharmony/os/3.2.3/hispark_taurus_LiteOS.tar.gz) | [SHA256校验码](https://repo.huaweicloud.com/openharmony/os/3.2.3/hispark_taurus_LiteOS.tar.gz.sha256) |
| Hi3516解决方案-Linux（二进制）        | 3.2.3 Release | [站点](https://repo.huaweicloud.com/openharmony/os/3.2.3/hispark_taurus_Linux.tar.gz) | [SHA256校验码](https://repo.huaweicloud.com/openharmony/os/3.2.3/hispark_taurus_Linux.tar.gz.sha256) |
| RK3568标准系统解决方案（二进制）      | 3.2.3 Release | [站点](https://repo.huaweicloud.com/openharmony/os/3.2.3/dayu200_standard_arm32.tar.gz) | [SHA256校验码](https://repo.huaweicloud.com/openharmony/os/3.2.3/dayu200_standard_arm32.tar.gz.sha256) |
| 标准系统Public SDK包（Mac）           | 3.2.14.5      | [站点](https://repo.huaweicloud.com/openharmony/os/3.2.3/ohos-sdk-mac-public.tar.gz) | [SHA256校验码](https://repo.huaweicloud.com/openharmony/os/3.2.3/ohos-sdk-mac-public.tar.gz.sha256) |
| 标准系统Public SDK包（Mac-M1）        | 3.2.14.5      | [站点](https://repo.huaweicloud.com/openharmony/os/3.2.3/L2-SDK-MAC-M1-PUBLIC.tar.gz) | [SHA256校验码](https://repo.huaweicloud.com/openharmony/os/3.2.3/L2-SDK-MAC-M1-PUBLIC.tar.gz.sha256) |
| 标准系统Public SDK包（Windows/Linux） | 3.2.14.5      | [站点](https://repo.huaweicloud.com/openharmony/os/3.2.3/ohos-sdk-windows_linux-public.tar.gz) | [SHA256校验码](https://repo.huaweicloud.com/openharmony/os/3.2.3/ohos-sdk-windows_linux-public.tar.gz.sha256) |

## 更新说明

### API 

3.2.3 Release对比3.2.2 Release API接口无变更。

### 芯片及开发板适配

芯片及开发板适配状态请参考[SIG-Devboard](https://gitee.com/openharmony/community/blob/master/sig/sig_devboard/sig_devboard_cn.md)信息。

## 修复缺陷issue列表

  **表3** 修复缺陷issue列表

| ISSUE                                                        | 问题描述                                                     |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [I73TPR](https://gitee.com/openharmony/ability_form_fwk/issues/I73TPR) | 【OpenHarmony  3.2.12.3】【RK3568】【压力测试】【ToC】【低概率1/10】【wukong】出现1次，由进程com.ohos.note下的com.ohos.note线程导致libace.z.so出现cppcrash |
| [I76UCD](https://gitee.com/openharmony/ability_form_fwk/issues/I76UCD) | 【OpenHarmony_3.2.12.5】【3.2Release】【多媒体子系统】【ToC】【RK3568】【必现-10/10】录像文件在图库播放最后2秒画面卡住未播放 |
| [I7B07F](https://gitee.com/openharmony/ability_form_fwk/issues/I7B07F) | 【OpenHarmony_3.2.12.5】【软总线】【发现】【Toc】【rk3568】【必现-3/3】蓝牙发现失败 |
| [I7BZ4F](https://gitee.com/openharmony/ability_form_fwk/issues/I7BZ4F) | 【OpenHarmony_3.2.13.1】【RK3568】【发现】【Toc】【概率 3/42】coap发现概率失败 |
| [I7C2B1](https://gitee.com/openharmony/ability_form_fwk/issues/I7C2B1) | 【OpenHarmony 3.2.13.1】【RK3568】【xts压力测试】【高概率20/30】出现20次  由进程com.amsst.stserviceabilityclient下的IPC_2_8347线程导致libabilitykit_native.z.so出现cppcrash |
| [I7C98S](https://gitee.com/openharmony/ability_form_fwk/issues/I7C98S) | 【OpenHarmony 3.2.13.1】【RK3568】【压力测试】【ToC】【低概率2/10】【wukong】出现2次，  com.ohos.photos下出现jscrash问题，栈名：initializeConsume |
| [I7D48T](https://gitee.com/openharmony/ability_form_fwk/issues/I7D48T) | 【OpenHarmony】【体验测试】【版本号：3.2.13.1】【rk3568】【ToC】【概率：必现】web浏览器打开天猫网页从上往下滑54帧，实际值50.9fps，差基线3.1fps |
| [I7D4KX](https://gitee.com/openharmony/ability_form_fwk/issues/I7D4KX) | 【OpenHarmony】【体验测试】【版本号：3.2.13.1】【rk3568】【ToC】【概率：必现】拨号盘按键响应时延88ms，实际值120.8ms，超基线32.8ms |
| [I7EZJK](https://gitee.com/openharmony/ability_form_fwk/issues/I7EZJK) | 【OpenHarmony 3.2.13.5】【媒体子系统】【RK3568】【必现】在图库中新建相册后，无法重命名相册 |
| [I7FO8I](https://gitee.com/openharmony/ability_form_fwk/issues/I7FO8I) | [Bug]: 【OpenHarmony 3.2  0620daily】【RK3568】【压力测试】【ToC】【低概率1/10】【wukong】出现1次  进com.ohos.adminprovisioning下的IPC_3_14056线程导致libabilitykit_native.z.so出现cppcrash |
| [I7FR03](https://gitee.com/openharmony/ability_form_fwk/issues/I7FR03) | [Bug]: 【OpenHarmony 3.2  0620daily】【RK3568】【压力测试】【ToC】【低概率1/10】【wukong】出现1次  由进程com.ohos.note下的RSRenderThread线程出现Rosenweb on  consumer导致libmali-bifrost-g52-g2p0-ohos.so出现cppcrash |
| [I7GA51](https://gitee.com/openharmony/ability_form_fwk/issues/I7GA51) | [Bug]: 【OpenHarmony 3.2.13.5】【应用子系统】【RK3568】【必现_5/5】桌面大文件夹展开后导航点与第四行图标重叠 |
| [I7GAJQ](https://gitee.com/openharmony/ability_form_fwk/issues/I7GAJQ) | [Bug]: 【OpenHarmony  3.2.13.5】【应用子系统】【RK3568】【必现_5/5】进入图库服务卡片界面后，再进入相机服务卡片界面显示异常 |

## 修复安全issue列表

  **表4** 修复安全issue列表

| ISSUE  | 问题描述                                            |
| ------ | --------------------------------------------------- |
| I6QYW7 | 【漏洞】 【OpenHarmony-3.2-Release】 CVE-2022-4095  |
| I6RZV9 | 【漏洞】 【OpenHarmony-3.2-Release】 CVE-2022-4744  |
| I6TCVF | 【漏洞】 【OpenHarmony-3.2-Release】 CVE-2023-1838  |
| I6TCVR | 【漏洞】 【OpenHarmony-3.2-Release】 CVE-2023-1855  |
| I6TCW0 | 【漏洞】 【OpenHarmony-3.2-Release】 CVE-2023-1582  |
| I6U82D | 【漏洞】 【OpenHarmony-3.2-Release】 CVE-2023-30456 |
| I6UW4X | 【漏洞】 【OpenHarmony-3.2-Release】 CVE-2022-29581 |
| I6UW4Y | 【漏洞】 【OpenHarmony-3.2-Release】 CVE-2022-1158  |
| I6VHE0 | 【漏洞】 【OpenHarmony-3.2-Release】 CVE-2023-1990  |
| I6VVQJ | 【漏洞】 【OpenHarmony-3.2-Release】 CVE-2023-1859  |
| I6W9EQ | 【漏洞】 【OpenHarmony-3.2-Release】 CVE-2023-30772 |
| I6YK8O | 【漏洞】 【OpenHarmony-3.2-Release】 CVE-2023-2008  |
| I6ZH6E | 【漏洞】 【OpenHarmony-3.2-Release】 CVE-2023-0458  |
| I6ZJDL | 【漏洞】 【OpenHarmony-3.2-Release】 CVE-2023-31436 |
| I6ZK8X | 【漏洞】 【OpenHarmony-3.2-Release】 CVE-2023-2177  |
| I6ZK92 | 【漏洞】 【OpenHarmony-3.2-Release】 CVE-2023-2194  |
| I6ZQRA | 【漏洞】 【OpenHarmony-3.2-Release】 CVE-2023-28328 |
| I6ZQRH | 【漏洞】 【OpenHarmony-3.2-Release】 CVE-2023-2166  |
| I6ZQRM | 【漏洞】 【OpenHarmony-3.2-Release】 CVE-2023-28327 |
| I6ZUT4 | 【漏洞】 【OpenHarmony-3.2-Release】 CVE-2023-2248  |
| I6ZZDJ | 【漏洞】 【OpenHarmony-3.2-Release】 CVE-2023-1998  |
| I70B1G | 【漏洞】 【OpenHarmony-3.2-Release】 CVE-2023-2483  |
| I72GRH | 【漏洞】 【OpenHarmony-3.2-Release】 CVE-2023-32269 |
| I73Z2O | 【漏洞】 【OpenHarmony-3.2-Release】 CVE-2023-2124  |
| I76VW0 | 【漏洞】 【OpenHarmony-3.2-Release】 CVE-2023-0459  |
| I78R44 | 【漏洞】 【OpenHarmony-3.2-Release】 CVE-2023-33203 |
| I79YE0 | 【漏洞】 【OpenHarmony-3.2-Release】 CVE-2023-34256 |

## 遗留缺陷列表

  **表5** 遗留缺陷列表

| ISSUE | 问题描述 | 影响 | 计划解决日期 |
| ----- | -------- | ---- | ------------ |
|       |          |      |              |
|       |          |      |              |
