# @ohos.userIAM.faceAuth    
提供人脸录入相关接口。  
> **说明**   
>本模块首批接口从API version 9开始支持。后续版本的新增接口，采用上角标单独标记接口的起始版本  
  
## 导入模块  
  
```js    
import faceAuth from '@ohos.userIAM.faceAuth'    
```  
    
## FaceAuthManager    
人脸认证管理器对象。  
 **系统API:**  此接口为系统接口。  
 **系统能力:**  SystemCapability.UserIAM.UserAuth.FaceAuth    
### setSurfaceId    
该接口仅用于在录入人脸时，设置人脸预览界面 [XComponent](../arkui-ts/ts-basic-components-xcomponent.md#getxcomponentsurfaceid) 持有 Surface 的 ID，需要配合[人脸录入接口](./js-apis-osAccount.md#addcredential8)来使用。  
 **调用形式：**     
- setSurfaceId(surfaceId: string): void  
  
 **系统API:**  此接口为系统接口。  
 **系统能力:**  SystemCapability.UserIAM.UserAuth.FaceAuth  
 **需要权限：** ohos.permission.MANAGE_USER_IDM    
 **参数：**     
| 参数名 | 类型 | 必填 | 说明 |  
| --------| --------| --------| --------|  
| surfaceId | string | true | [XComponent](../arkui-ts/ts-basic-components-xcomponent.md#getxcomponentsurfaceid) 持有 Surface 的 ID。 |  
    
    
 **错误码：**     
| 错误码ID | 错误信息 |  
| --------| --------|  
| 201 | Permission verification failed. |  
| 202 | The caller is not a system application. |  
| 12700001 | The operation is failed. |  
    
 **示例代码：**   
```ts    
import userIAM_faceAuth from '@ohos.userIAM.faceAuth';  
  
// 该surfaceId应该从XComponent控件获取，此处仅用作示例。  
let surfaceId = '123456';  
let manager = new userIAM_faceAuth.FaceAuthManager();  
try {  
  manager.setSurfaceId(surfaceId);  
  console.info('set surface id success');  
} catch (e) {  
  console.error('set surface id failed, error = ' + e);  
}  
    
```    
  
