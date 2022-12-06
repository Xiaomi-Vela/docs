# Ability

Ability模块将二级模块API组织在一起方便开发者进行导出。

> **说明：**
> 
> 本模块首批接口从API version 9开始支持。后续版本的新增接口，采用上角标单独标记接口的起始版本。
> 本模块接口仅可在FA模型下使用

## 导入模块

```ts
import ability from '@ohos.ability.ability'
```

**系统能力**：以下各项对应的系统能力均为SystemCapability.Ability.AbilityBase

| 名称        | 可读    | 可写     | 类型                 | 必填 | 说明                                                         |
| ----------- | -------- |-------- | -------------------- | ---- | ------------------------------------------------------------ |
| DataAbilityHelper    | 是    | 否      | number               | 否   | DataAbilityHelper二级模块。                                |
| PacMap   | 是    | 否      | Want               | 否   | PacMap二级模块。 |
| DataAbilityOperation   | 是    | 否      | Want               | 否   | DataAbilityOperation二级模块。 |
| DataAbilityResult   | 是    | 否      | Want               | 否   | DataAbilityResult二级模块。 |
| AbilityResult   | 是    | 否      | Want               | 否   | AbilityResult二级模块。 |
| ConnectOptions   | 是    | 否      | Want               | 否   | ConnectOptions二级模块。 |
| StartAbilityParameter   | 是    | 否      | Want               | 否   | StartAbilityParameter二级模块。 |

**示例：**

  ```ts
  let dataAbilityHelper: ability.DataAbilityHelper;
  let pacMap: ability.PacMap;
  let dataAbilityOperation: ability.DataAbilityOperation;
  let dataAbilityResult: ability.DataAbilityResult;
  let abilityResult: ability.AbilityResult;
  let connectOptions: ability.ConnectOptions;  
  let startAbilityParameter: ability.StartAbilityParameter;
  ```