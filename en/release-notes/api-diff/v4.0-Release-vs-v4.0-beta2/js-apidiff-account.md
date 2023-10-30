| Change Type | Old Version | New Version | d.ts File |
| ---- | ------ | ------ | -------- |
|Deleted|Class name: AuthorizationExtensionAbility;<br>Method or attribute name: onStartAuthorization(request: AuthorizationRequest, callback: AuthorizationCallback): void;|NA|@ohos.account.appAccount.AuthorizationExtensionAbility.d.ts|
|Deleted|Class name: AuthorizationRequest;<br>Method or attribute name: readonly callerUid: number;|NA|@ohos.account.appAccount.AuthorizationExtensionAbility.d.ts|
|Deleted|Class name: AuthorizationRequest;<br>Method or attribute name: readonly parameters: appAccount.AccountCapabilityRequest;|NA|@ohos.account.appAccount.AuthorizationExtensionAbility.d.ts|
|Deleted|Class name: AuthorizationCallback;<br>Method or attribute name: onResult: AsyncCallback\<appAccount.AccountCapabilityResponse, { [key: string]: object }>;|NA|@ohos.account.appAccount.AuthorizationExtensionAbility.d.ts|
|Deleted|Class name: AccountCapabilityType;<br>Method or attribute name: AUTHORIZATION = 1|NA|@ohos.account.appAccount.d.ts|
|Deleted|Class name: AccountCapabilityProvider;<br>Method or attribute name: readonly capabilityType: AccountCapabilityType;|NA|@ohos.account.appAccount.d.ts|
|Deleted|Class name: AccountCapabilityProvider;<br>Method or attribute name: constructor(capabilityType: AccountCapabilityType);|NA|@ohos.account.appAccount.d.ts|
|Deleted|Class name: AuthorizationProvider;<br>Method or attribute name: constructor(info: AuthorizationProviderInfo);|NA|@ohos.account.appAccount.d.ts|
|Deleted|Class name: AuthorizationProviderInfo;<br>Method or attribute name: readonly bundleName: string;|NA|@ohos.account.appAccount.d.ts|
|Deleted|Class name: AuthorizationProviderInfo;<br>Method or attribute name: readonly abilityName: string;|NA|@ohos.account.appAccount.d.ts|
|Deleted|Class name: AccountCapabilityRequest;<br>Method or attribute name: constructor(provider: AccountCapabilityProvider);|NA|@ohos.account.appAccount.d.ts|
|Deleted|Class name: AccountCapabilityResponse;<br>Method or attribute name: readonly request: AccountCapabilityRequest;|NA|@ohos.account.appAccount.d.ts|
|Deleted|Class name: AccountCapabilityResponse;<br>Method or attribute name: constructor(request: AccountCapabilityRequest);|NA|@ohos.account.appAccount.d.ts|
|Deleted|Class name: AccountCapabilityScheduler;<br>Method or attribute name: executeRequest(<br>      request: AccountCapabilityRequest,<br>      callback: AsyncCallback\<AccountCapabilityResponse, { [key: string]: object }><br>    ): void;|NA|@ohos.account.appAccount.d.ts|
|Deleted|Class name: AccountCapabilityScheduler;<br>Method or attribute name: executeRequest(request: AccountCapabilityRequest): Promise\<AccountCapabilityResponse>;|NA|@ohos.account.appAccount.d.ts|
|Added|NA|Class name: AccountManager;<br>Method or attribute name: getOsAccountLocalIdForUidSync(uid: number): number;|@ohos.account.osAccount.d.ts|
|Added|NA|Class name: AccountManager;<br>Method or attribute name: getBundleIdForUidSync(uid: number): number;|@ohos.account.osAccount.d.ts|
|Added|NA|Class name: GetDomainAccountInfoOptions;<br>Method or attribute name: accountName: string;|@ohos.account.osAccount.d.ts|
|Added|NA|Class name: GetDomainAccountInfoOptions;<br>Method or attribute name: domain?: string;|@ohos.account.osAccount.d.ts|
|Added|NA|Class name: GetDomainAccountInfoPluginOptions;<br>Method or attribute name: callerUid: number;|@ohos.account.osAccount.d.ts|
|Added|NA|Class name: DomainAccountManager;<br>Method or attribute name: static getAccountInfo(options: GetDomainAccountInfoOptions, callback: AsyncCallback\<DomainAccountInfo>): void;|@ohos.account.osAccount.d.ts|
|Added|NA|Class name: DomainAccountManager;<br>Method or attribute name: static getAccountInfo(options: GetDomainAccountInfoOptions): Promise\<DomainAccountInfo>;|@ohos.account.osAccount.d.ts|
|Error code changed|Class name: UserAuth;<br>Method or attribute name: auth(<br>      challenge: Uint8Array,<br>      authType: AuthType,<br>      authTrustLevel: AuthTrustLevel,<br>      callback: IUserAuthCallback<br>    ): Uint8Array;<br>Old version information: 201,202,401, 12300001, 12300002, 12300101, 12300105, 12300106, 12300110, 12300111, 12300112|Class name: UserAuth;<br>Method or attribute name: auth(<br>      challenge: Uint8Array,<br>      authType: AuthType,<br>      authTrustLevel: AuthTrustLevel,<br>      callback: IUserAuthCallback<br>    ): Uint8Array;<br>New version information: 201,202,401, 12300001, 12300002, 12300101, 12300102, 12300105, 12300106, 12300109, 12300110, 12300111, 12300112|@ohos.account.osAccount.d.ts|
|Error code changed|Class name: UserAuth;<br>Method or attribute name: authUser(<br>      userId: number,<br>      challenge: Uint8Array,<br>      authType: AuthType,<br>      authTrustLevel: AuthTrustLevel,<br>      callback: IUserAuthCallback<br>    ): Uint8Array;<br>Old version information: 201,202,401, 12300001, 12300002, 12300101, 12300105, 12300106, 12300110, 12300111, 12300112|Class name: UserAuth;<br>Method or attribute name: authUser(<br>      userId: number,<br>      challenge: Uint8Array,<br>      authType: AuthType,<br>      authTrustLevel: AuthTrustLevel,<br>      callback: IUserAuthCallback<br>    ): Uint8Array;<br>New version information: 201,202,401, 12300001, 12300002, 12300101, 12300102, 12300105, 12300106, 12300109, 12300110, 12300111, 12300112|@ohos.account.osAccount.d.ts|
|Error code changed|Class name: DomainAccountManager;<br>Method or attribute name: static auth(domainAccountInfo: DomainAccountInfo, credential: Uint8Array, callback: IUserAuthCallback): void;<br>Old version information: 201,202,401, 12300001, 12300002, 12300003,12300013,12300101, 12300109, 12300110, 12300111, 12300112, 12300113,12300114|Class name: DomainAccountManager;<br>Method or attribute name: static auth(domainAccountInfo: DomainAccountInfo, credential: Uint8Array, callback: IUserAuthCallback): void;<br>New version information: 201,202,401,801, 12300001, 12300002, 12300003,12300013,12300101, 12300109, 12300110, 12300111, 12300112, 12300113,12300114|@ohos.account.osAccount.d.ts|
|Error code changed|Class name: DomainAccountManager;<br>Method or attribute name: static authWithPopup(callback: IUserAuthCallback): void;<br>Old version information: 201,202,401, 12300001, 12300003,12300013,12300101, 12300109, 12300110, 12300111, 12300112, 12300113,12300114|Class name: DomainAccountManager;<br>Method or attribute name: static authWithPopup(callback: IUserAuthCallback): void;<br>New version information: 201,202,401,801, 12300001, 12300003,12300013,12300101, 12300109, 12300110, 12300111, 12300112, 12300113,12300114|@ohos.account.osAccount.d.ts|
|Error code changed|Class name: DomainAccountManager;<br>Method or attribute name: static authWithPopup(localId: number, callback: IUserAuthCallback): void;<br>Old version information: 201,202,401, 12300001, 12300002, 12300003,12300013,12300101, 12300109, 12300110, 12300111, 12300112, 12300113,12300114|Class name: DomainAccountManager;<br>Method or attribute name: static authWithPopup(localId: number, callback: IUserAuthCallback): void;<br>New version information: 201,202,401,801, 12300001, 12300002, 12300003,12300013,12300101, 12300109, 12300110, 12300111, 12300112, 12300113,12300114|@ohos.account.osAccount.d.ts|
|Error code changed|Class name: DomainAccountManager;<br>Method or attribute name: static hasAccount(domainAccountInfo: DomainAccountInfo, callback: AsyncCallback\<boolean>): void;<br>Old version information: 201,202,401, 12300001, 12300002, 12300013|Class name: DomainAccountManager;<br>Method or attribute name: static hasAccount(domainAccountInfo: DomainAccountInfo, callback: AsyncCallback\<boolean>): void;<br>New version information: 201,202,401,801, 12300001, 12300002, 12300013,12300111|@ohos.account.osAccount.d.ts|
|Error code changed|Class name: DomainAccountManager;<br>Method or attribute name: static hasAccount(domainAccountInfo: DomainAccountInfo): Promise\<boolean>;<br>Old version information: 201,202,401, 12300001, 12300002, 12300013|Class name: DomainAccountManager;<br>Method or attribute name: static hasAccount(domainAccountInfo: DomainAccountInfo): Promise\<boolean>;<br>New version information: 201,202,401,801, 12300001, 12300002, 12300013,12300111|@ohos.account.osAccount.d.ts|
|Error code changed|Class name: UserIdentityManager;<br>Method or attribute name: addCredential(credentialInfo: CredentialInfo, callback: IIdmCallback): void;<br>Old version information: 201,202,401, 12300001, 12300002, 12300101, 12300106|Class name: UserIdentityManager;<br>Method or attribute name: addCredential(credentialInfo: CredentialInfo, callback: IIdmCallback): void;<br>New version information: 201,202,401, 12300001, 12300002, 12300101, 12300106, 12300109, 12300111, 12300115|@ohos.account.osAccount.d.ts|
|Error code changed|Class name: UserIdentityManager;<br>Method or attribute name: updateCredential(credentialInfo: CredentialInfo, callback: IIdmCallback): void;<br>Old version information: 201,202,401, 12300001, 12300002, 12300101, 12300106|Class name: UserIdentityManager;<br>Method or attribute name: updateCredential(credentialInfo: CredentialInfo, callback: IIdmCallback): void;<br>New version information: 201,202,401, 12300001, 12300002, 12300101, 12300102, 12300106, 12300109, 12300111|@ohos.account.osAccount.d.ts|
|Error code changed|Class name: UserIdentityManager;<br>Method or attribute name: getAuthInfo(callback: AsyncCallback\<Array\<EnrolledCredInfo>>): void;<br>Old version information: 201,202,401, 12300001|Class name: UserIdentityManager;<br>Method or attribute name: getAuthInfo(callback: AsyncCallback\<Array\<EnrolledCredInfo>>): void;<br>New version information: 201,202,401, 12300001, 12300102|@ohos.account.osAccount.d.ts|
|Error code changed|Class name: UserIdentityManager;<br>Method or attribute name: getAuthInfo(authType: AuthType, callback: AsyncCallback\<Array\<EnrolledCredInfo>>): void;<br>Old version information: 201,202,401, 12300001, 12300002|Class name: UserIdentityManager;<br>Method or attribute name: getAuthInfo(authType: AuthType, callback: AsyncCallback\<Array\<EnrolledCredInfo>>): void;<br>New version information: 201,202,401, 12300001, 12300002, 12300102|@ohos.account.osAccount.d.ts|
|Error code changed|Class name: UserIdentityManager;<br>Method or attribute name: getAuthInfo(authType?: AuthType): Promise\<Array\<EnrolledCredInfo>>;<br>Old version information: 201,202,401, 12300001, 12300002|Class name: UserIdentityManager;<br>Method or attribute name: getAuthInfo(authType?: AuthType): Promise\<Array\<EnrolledCredInfo>>;<br>New version information: 201,202,401, 12300001, 12300002, 12300102|@ohos.account.osAccount.d.ts|
|Permission changed|Class name: AccountManager;<br>Method or attribute name: getCurrentOsAccount(callback: AsyncCallback\<OsAccountInfo>): void;<br>Old version information: ohos.permission.MANAGE_LOCAL_ACCOUNTS|Class name: AccountManager;<br>Method or attribute name: getCurrentOsAccount(callback: AsyncCallback\<OsAccountInfo>): void;<br>New version information: ohos.permission.MANAGE_LOCAL_ACCOUNTS,ohos.permission.GET_LOCAL_ACCOUNTS|@ohos.account.osAccount.d.ts|
|Permission changed|Class name: AccountManager;<br>Method or attribute name: getCurrentOsAccount(): Promise\<OsAccountInfo>;<br>Old version information: ohos.permission.MANAGE_LOCAL_ACCOUNTS|Class name: AccountManager;<br>Method or attribute name: getCurrentOsAccount(): Promise\<OsAccountInfo>;<br>New version information: ohos.permission.MANAGE_LOCAL_ACCOUNTS,ohos.permission.GET_LOCAL_ACCOUNTS|@ohos.account.osAccount.d.ts|
|Function changed|Class name: DomainPlugin;<br>Method or attribute name: getAccountInfo(domain: string, accountName: string, callback: AsyncCallback\<DomainAccountInfo>): void;|Class name: DomainPlugin;<br>Method or attribute name: getAccountInfo(options: GetDomainAccountInfoPluginOptions, callback: AsyncCallback\<DomainAccountInfo>): void;|@ohos.account.osAccount.d.ts|