# Common Events of the Account Subsystem
This document lists the common system events provided by the account subsystem to applications. Applications can use [APIs](../js-apis-commonEventManager.md) to subscribe to common system events.

## COMMON_EVENT_USER_ADDED
Indicates that a user has been added to the system.

- Value: usual.event.USER_ADDED
- Required subscriber permissions: ohos.permission.MANAGE_LOCAL_ACCOUNTS

When a system account is created, the event notification service is triggered to publish this event carrying the system account ID.

APIs related to this event: **createOsAccount** and **createOsAccountForDomain**. These APIs are system APIs. For details, see [@ohos.account.osAccount (OS Account Management)](../js-apis-osAccount.md).

## COMMON_EVENT_USER_REMOVED
Indicates that a user has been removed from the system.

- Value: usual.event.USER_REMOVED
- Required subscriber permissions: ohos.permission.MANAGE_LOCAL_ACCOUNTS

When a system account is removed, the event notification service is triggered to publish this event carrying the system account ID.

APIs related to this event: **removeOsAccount**. This API is a system API. For details, see [@ohos.account.osAccount (OS Account Management)](../js-apis-osAccount.md).

## COMMON_EVENT_DOMAIN_ACCOUNT_STATUS_CHANGED<sup>10+<sup>
Indicates that the status of the domain account status changes.

- Value: usual.event.DOMAIN_ACCOUNT_STATUS_CHANGED
- Required subscriber permissions: ohos.permission.GET_LOCAL_ACCOUNTS

When a domain user account is authenticated, deleted, or has the token updated, the event notification service is triggered to publish this event carrying the system account ID, domain name, and account status.

APIs related to this event: **removeOsAccount**, **DomainAccountManager.auth**, and **updateAccountToken**. These APIs are system APIs. For details, see [@ohos.account.osAccount (OS Account Management)](../js-apis-osAccount.md).

## COMMON_EVENT_USER_SWITCHED
Indicates that user switching is in progress.

- Value: usual.event.USER_SWITCHED
- Required subscriber permissions: ohos.permission.MANAGE_LOCAL_ACCOUNTS

When the system account is switched, the event notification service is triggered to publish this event carrying the system account ID.

APIs related to this event: **activateOsAccount**. This API is a system API. For details, see [@ohos.account.osAccount (OS Account Management)](../js-apis-osAccount.md).

## COMMON_EVENT_USER_INFO_UPDATED<sup>9+<sup>
Indicates that the user information has been updated.

- Value: **usual.event.USER_INFO_UPDATED**
- Required subscriber permissions: none

When the distributed account information, system account profile picture, or system account name is changed, the event notification service is triggered to publish this event carrying the system account ID.

APIs related to this event: **setOsAccountName**, **setOsAccountProfilePhoto**, and **setOsAccountDistributedInfon**. The first two are system APIs, and the last is a public API. For details, see [@ohos.account.osAccount (OS Account Management)](../js-apis-osAccount.md).

## COMMON_EVENT_DISTRIBUTED_ACCOUNT_LOGIN
(Reserved, not supported yet) Indicates a successful login to a distributed account.

- Value: usual.event.DISTRIBUTED_ACCOUNT_LOGIN
- Required subscriber permissions: none

## COMMON_EVENT_DISTRIBUTED_ACCOUNT_LOGOUT
(Reserved, not supported yet) Indicates a successful logout of a distributed account.

- Value: usual.event.DISTRIBUTED_ACCOUNT_LOGOUT
- Required subscriber permissions: none

## COMMON_EVENT_DISTRIBUTED_ACCOUNT_TOKEN_INVALID
(Reserved, not supported yet) Indicates the token of a distributed account is invalid.

- Value: usual.event.DISTRIBUTED_ACCOUNT_TOKEN_INVALID
- Required subscriber permissions: none

## COMMON_EVENT_DISTRIBUTED_ACCOUNT_LOGOFF
(Reserved, not supported yet) Indicates that a distributed account is deregistered.

- Value: usual.event.DISTRIBUTED_ACCOUNT_LOGOFF
- Required subscriber permissions: none
