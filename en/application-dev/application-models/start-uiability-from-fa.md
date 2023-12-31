# Starting a UIAbility from the FA Model


This topic describes how the three application components of the FA model start the UIAbility component of the stage model.


## PageAbility Starting a UIAbility

A PageAbility starts a UIAbility in the same way as it starts another PageAbility.

```ts
import featureAbility from '@ohos.ability.featureAbility';
import { BusinessError } from '@ohos.base';

featureAbility.startAbility(
    {
        want: {
            bundleName: "com.ohos.stage",
            abilityName: "EntryAbility"
        }
    }
).then((code) => {
    console.info('Ability verify code: ' + JSON.stringify(code));
}).catch((error: BusinessError) => {
    console.error("Ability failed: " + JSON.stringify(error));
});
```


## PageAbility Accessing a UIAbility (startAbilityForResult)

Different from **startAbility()**, **startAbilityForResult()** obtains the execution result when the UIAbility is destroyed.

A PageAbility starts a UIAbility through **startAbilityForResult()** in the same way as it starts another PageAbility through **startAbilityForResult()**.


```ts
import featureAbility from '@ohos.ability.featureAbility';
import { BusinessError } from '@ohos.base';

featureAbility.startAbilityForResult(
    {
        want: {
            bundleName: "com.ohos.stage",
            abilityName: "com.ohos.stage.EntryAbility"
        }
    }).then((result) => {
    console.info('Ability verify result: ' + JSON.stringify(result));
}).catch((error: BusinessError) => {
    console.error("Ability failed: " + JSON.stringify(error));
});
```


## ServiceAbility or DataAbility Starting a UIAbility

A ServiceAbility or DataAbility starts a UIAbility in the same way as it starts a PageAbility.


```ts
import particleAbility from '@ohos.ability.particleAbility';
import { BusinessError } from '@ohos.base';

particleAbility.startAbility(
    {
        want: {
            bundleName: "com.ohos.stage",
            abilityName: "com.ohos.stage.EntryAbility"
        }
    }
).then(() => {
    console.info('Start Ability successfully.');
}).catch((error: BusinessError) => {
    console.error("Ability failed: " + JSON.stringify(error));
});
```
