# 数据共享错误码

> **说明：**
>
> 以下仅介绍本模块特有错误码，通用错误码请参考[通用错误码说明文档](errorcode-universal.md)。

## 15700010 创建DataShareHelper异常

**错误信息**

The DataShareHelper is not initialized successfully.

**错误描述**

创建DataShareHelper工具类异常时，系统会产生此错误码。

**可能原因**

1. 创建DataShareHelper时，接口createDataHelper的入参uri不正确。
2. 创建DataShareHelper时，接口createDataHelper的入参context不正确。
3. 创建DataShareHelper时，客户端从后台拉起DataShareExtension时，未配置后台拉起权限。

**处理步骤**

1. 咨询DataShare服务端提供者，获取正确的uri路径。
2. DataShare仅支持Stage模型，检查context是否为Stage模型的context。
3. 检查客户端是否有数据的读或者写权限，具体步骤如下：
    (1) 找到数据提供者包名，在uri的path里面找，例如：uri = "datashareproxy://com.acts.ohos.data.datasharetest/test"。
    (2) 根据包名找到配置，例如：bm dump --bundle-name com.acts.ohos.data.datasharetest，在里面找到DataShareExtension的配置，确认数据访问者是否有readPermission或writePermission中配置的权限.

## 15700011 添加/删除模板异常

**错误信息**

The uri is not exist.

**错误描述**

添加/删除模板异常时，系统会产生此错误码。

**可能原因**

1. 添加模板异常时，接口addTemplate的入参uri不正确。
2. 删除模板异常时，接口delTemplate的入参uri不正确。

**处理步骤**

咨询DataShare服务端提供者，获取正确的uri路径。

## 15700012 数据区不存在

**错误信息**

The data area is not exist.

**错误描述**

数据更新异常时，系统会产生此错误码。

**可能原因**

数据更新异常时，接口publish的入参bundleName不正确。

**处理步骤**

咨询DataShare服务端提供者，获取正确的bundleName。