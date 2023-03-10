#  	访问控制管理

> ![icon-note.gif](public_sys-resources/icon-note.gif) **说明：**
> 本模块首批接口从API version 8开始支持。后续版本的新增接口，采用上角标单独标记接口的起始版本。

## 导入模块

```js
import abilityAccessCtrl from '@ohos.abilityAccessCtrl'
```

## abilityAccessCtrl.createAtManager

createAtManager(): AtManager

访问控制管理：获取访问控制模块对象。

**系统能力：** SystemCapability.Security.AccessToken


**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| [AtManager](#atmanager) | 获取访问控制模块的实例。 |

**示例：**

```
var AtManager = abilityAccessCtrl.createAtManager();
```

## AtManager

管理访问控制模块的实例。

### verifyAccessToken

verifyAccessToken(tokenID: number, permissionName: string): Promise&lt;GrantStatus&gt;

校验应用是否授予权限，使用Promise方式异步返回结果。

**系统能力：** SystemCapability.Security.AccessToken

**参数：**

| 参数名   | 类型                 | 必填 | 说明                                       |
| -------- | -------------------  | ---- | ------------------------------------------ |
| tokenID   |  number   | 是   | 要校验的目标应用的身份标识。              |
| permissionName | string | 是   | 需要校验的权限名称。 |

**返回值：**

| 类型          | 说明                                |
| :------------ | :---------------------------------- |
| Promise&lt;GrantStatus&gt; | Promise实例，用于获取异步返回的授权状态结果。 |

**示例：**

```
var AtManager = abilityAccessCtrl.createAtManager();
let tokenID = 0;
let promise = AtManager.verifyAccessToken(tokenID, "ohos.permission.GRANT_SENSITIVE_PERMISSIONS");
promise.then(data => {
    console.log(`promise: data->${JSON.stringify(data)}`);
});
```

### grantUserGrantedPermission

grantUserGrantedPermission(tokenID: number, permissionName: string, permissionFlags: number): Promise&lt;number&gt;

授予应用user grant权限，使用Promise方式异步返回结果。

此接口为系统接口。

**需要权限：** ohos.permission.GRANT_SENSITIVE_PERMISSIONS

**系统能力：** SystemCapability.Security.AccessToken

**参数：**

| 参数名    | 类型                | 必填 | 说明                                                         |
| --------- | ------------------- | ---- | ------------------------------------------------------------ |
| tokenID      | number              | 是   | 目标应用的身份标识。            |
| permissionName | string              | 是   | 被授予的权限名称。 |
| permissionFlags  | number | 是   | 授权选项<br>- 0表示权限未经过用户主动设置。<br>- 1表示当次用户若选择禁止该权限，下次权限弹窗仍可以弹出申请用户授权。<br>- 2表示当次用户若选择禁止该权限，下次不会再弹出权限弹窗，需要用户在setting的权限管理中进行授权。<br>- 4表示当次权限设置为系统授权，用户不可更改这个权限授权状态。 |

**返回值：**

| 类型          | 说明                                |
| :------------ | :---------------------------------- |
| Promise&lt;number&gt; | Promise实例，用于获取异步返回的授权操作结果。 |

**示例：**

```
var AtManager = abilityAccessCtrl.createAtManager();
let tokenID = 0;
let permissionFlags = 1;
let promise = AtManager.grantUserGrantedPermission(tokenID, "ohos.permission.GRANT_SENSITIVE_PERMISSIONS", permissionFlags);
promise.then(data => {
    console.log(`promise: data->${JSON.stringify(data)}`);
});
```



### grantUserGrantedPermission

grantUserGrantedPermission(tokenID: number, permissionName: string, permissionFlags: number, callback: AsyncCallback&lt;number&gt;): void

授予应用user grant权限，使用callback回调异步返回结果。

此接口为系统接口。

**需要权限：** ohos.permission.GRANT_SENSITIVE_PERMISSIONS

**系统能力：** SystemCapability.Security.AccessToken

**参数：**

| 参数名    | 类型                | 必填 | 说明                          |
| --------- | ------------------- | ---- | ------------------------------------------------------------ |
| tokenID      | number              | 是   | 目标应用的身份标识。           |
| permissionName | string              | 是   | 被授予的权限名称。 |
| permissionFlags  | number | 是   | 授权选项<br>- 0表示权限未经过用户主动设置。<br>- 1表示当次用户若选择禁止该权限，下次权限弹窗仍可以弹出申请用户授权。<br>- 2表示当次用户若选择禁止该权限，下次不会再弹出权限弹窗，需要用户在setting的权限管理中进行授权。<br>- 4表示当次权限设置为系统授权，用户不可更改这个权限授权状态。 |
| callback | AsyncCallback&lt;number&gt; | 是 | 检查授予应用user grant权限的操作结果同步的回调。 |

**示例：**

```
var AtManager = abilityAccessCtrl.createAtManager();
let tokenID = 0;
let permissionFlags = 1;
AtManager.grantUserGrantedPermission(tokenID, "ohos.permission.GRANT_SENSITIVE_PERMISSIONS",permissionFlags, data => {
    console.log(`callback: data->${JSON.stringify(data)}`);
});
```

### revokeUserGrantedPermission

revokeUserGrantedPermission(tokenID: number, permissionName: string, permissionFlags: number): Promise&lt;number&gt;

撤销应用user grant权限，使用Promise方式异步返回结果。

此接口为系统接口。

**需要权限：** ohos.permission.REVOKE_SENSITIVE_PERMISSIONS

**系统能力：** SystemCapability.Security.AccessToken

**参数：**

| 参数名    | 类型                | 必填 | 说明                                                         |
| --------- | ------------------- | ---- | ------------------------------------------------------------ |
| tokenID      | number              | 是   | 目标应用的身份标识。            |
| permissionName | string              | 是   | 被撤销的权限名称。 |
| permissionFlags  | number | 是   | 授权选项<br>- 0表示权限未经过用户主动设置。<br>- 1表示当次用户若选择禁止该权限，下次权限弹窗仍可以弹出申请用户授权。<br>- 2表示当次用户若选择禁止该权限，下次不会再弹出权限弹窗，需要用户在setting的权限管理中进行授权。<br>- 4表示当次权限设置为系统授权，用户不可更改这个权限授权状态。 |

**返回值：**

| 类型          | 说明                                |
| :------------ | :---------------------------------- |
| Promise&lt;number&gt; | Promise实例，用于获取异步返回的授权操作结果。 |

**示例：**

```
var AtManager = abilityAccessCtrl.createAtManager();
let tokenID = 0;
let permissionFlags = 1;
let promise = AtManager.revokeUserGrantedPermission(tokenID, "ohos.permission.GRANT_SENSITIVE_PERMISSIONS", permissionFlags);
promise.then(data => {
    console.log(`promise: data->${JSON.stringify(data)}`);
});
```

### revokeUserGrantedPermission

revokeUserGrantedPermission(tokenID: number, permissionName: string, permissionFlags: number, callback: AsyncCallback&lt;number&gt;): void

撤销应用user grant权限，使用callback回调异步返回结果。

此接口为系统接口。

**需要权限：** ohos.permission.REVOKE_SENSITIVE_PERMISSIONS

**系统能力：** SystemCapability.Security.AccessToken

**参数：**

| 参数名    | 类型                | 必填 | 说明                          |
| --------- | ------------------- | ---- | ------------------------------------------------------------ |
| tokenID      | number              | 是   | 目标应用的身份标识。            |
| permissionName | string              | 是   | 被撤销的权限名称。 |
| permissionFlags  | number | 是   | 授权选项<br>- 0表示权限未经过用户主动设置。<br>- 1表示当次用户若选择禁止该权限，下次权限弹窗仍可以弹出申请用户授权。<br>- 2表示当次用户若选择禁止该权限，下次不会再弹出权限弹窗，需要用户在setting的权限管理中进行授权。<br>- 4表示当次权限设置为系统授权，用户不可更改这个权限授权状态。 |
| callback | AsyncCallback&lt;number&gt; | 是 | 检查撤销应用user grant权限的操作结果同步的回调。 |

**示例：**

```
var AtManager = abilityAccessCtrl.createAtManager();
let tokenID = 0;
let permissionFlags = 1;
AtManager.revokeUserGrantedPermission(tokenID, "ohos.permission.GRANT_SENSITIVE_PERMISSIONS",permissionFlags, data => {
    console.log(`callback: data->${JSON.stringify(data)}`);
});
```

### getPermissionFlags

getPermissionFlags(tokenID: number, permissionName: string): Promise&lt;number&gt;

获取指定应用的指定权限的flag，使用Promise方式异步返回结果。

此接口为系统接口。

**需要权限：** ohos.permission.GET_SENSITIVE_PERMISSIONS or GRANT_SENSITIVE_PERMISSIONS or REVOKE_SENSITIVE_PERMISSIONS

**系统能力：** SystemCapability.Security.AccessToken

**参数：**

| 参数名    | 类型                | 必填 | 说明                          |
| --------- | ------------------- | ---- | ------------------------------------------------------------ |
| tokenID      | number              | 是   | 目标应用的身份标识。            |
| permissionName | string              | 是   | 查询的权限名称。 |

**返回值：**

| 类型          | 说明                                |
| :------------ | :---------------------------------- |
| Promise&lt;number&gt; | Promise实例，用于获取异步返回的查询结果。 |

**示例：**

```
var AtManager = abilityAccessCtrl.createAtManager();
let tokenID = 0;
let promise = AtManager.getPermissionFlags(tokenID, "ohos.permission.GRANT_SENSITIVE_PERMISSIONS");
promise.then(data => {
    console.log(`promise: data->${JSON.stringify(data)}`);
});
```

### GrantStatus

表示授权状态的枚举。

**系统能力：** 以下各项对应的系统能力均为SystemCapability.Security.AccessToken

| 名称                          | 默认值                  | 描述                    |
| ----------------------------- | ---------------------- | -----------------------  |
| PERMISSION_DENIED             | -1                     | 表示未授权。             |
| PERMISSION_GRANTED            | 0                      | 表示已授权。             |