# URI String Parsing

> **NOTE**<br>
> The initial APIs of this module are supported since API version 8. Newly added APIs will be marked with a superscript to indicate their earliest API version.


## Modules to Import

```
import uri from '@ohos.uri'  
```

## System Capabilities

SystemCapability.Utils.Lang

## URI


### Attributes

| Name| Type| Readable| Writable| Description|
| -------- | -------- | -------- | -------- | -------- |
| scheme | string | Yes| No| Scheme in the URI.|
| userInfo | string | Yes| No| User information in the URI.|
| host | string | Yes| No| Host name (without the port number) in the URI.|
| port | string | Yes| No| Port number in the URI.|
| path | string | Yes| No| Path in the URI.|
| query | string | Yes| No| Query part in the URI.|
| fragment | string | Yes| No| Fragment part in the URI.|
| authority | string | Yes| No| Authority part in the URI.|
| ssp | string | Yes| No| Scheme-specific part in the URI.|


### constructor

constructor(uri: string)

A constructor used to create a URI instance.

**Parameters**

| Name| Type.| Readable| Writable| Description|
| -------- | -------- | -------- | -------- | -------- |
| uri | string | Yes| Yes| Input object.|

**Example**

```js
var mm = 'http://username:password@host:8080/directory/file?foo=1&bar=2#fragment';
new uri.URI(mm); // Output 'http://username:password@host:8080/directory/file?foo=1&bar=2#fragment';
```
```js
new uri.URI('http://username:password@host:8080'); // Output 'http://username:password@host:8080';
```


### toString

toString(): string

Obtains the query string applicable to this URI.

**Return value**

| Type.| Description|
| -------- | -------- |
| string | Website address in a serialized string.|

**Example**

```js
const uri = new uri.URI('http://username:password@host:8080/directory/file?query=pppppp#qwer=da');
uri.toString()
```


### equals

equals(other: URI): boolean

Checks whether this URI is the same as another URI object.

**Parameters**

| Name| Type.| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| other | [URI](#uri) | Yes| URI object to compare.|

**Return value**

| Type.| Description|
| -------- | -------- |
| boolean | Returns **true** if the two URIs are the same; returns **false** otherwise.|

**Example**

```js
const uriInstance = new uri.URI('http://username:password@host:8080/directory/file?query=pppppp#qwer=da');
const uriInstance1 = new uri.URI('http://username:password@host:8080/directory/file?query=pppppp#qwer=da#fragment');
uriInstance.equals(uriInstance1);
```

### checkIsAbsolute

checkIsAbsolute(): boolean

Checks whether this URI is an absolute URI (whether the scheme component is defined).

**Return value**

| Type.| Description|
| -------- | -------- |
| boolean | Returns **true** if the URI is an absolute URI; returns **false** otherwise.|

**Example**

```js
const uriInstance = new uri.URI('http://username:password@www.qwer.com:8080?query=pppppp');
uriInstance.checkIsAbsolute();
```


### normalize

normalize(): URI

Normalizes the path of this URI.

**Return value**

| Type.| Description|
| -------- | -------- |
| URI | URI with the normalized path.|

**Example**
```js
const uriInstance = new uri.URI('http://username:password@www.qwer.com:8080/path/path1/../path2/./path3?query=pppppp');
let uriInstance1 = uriInstance.normalize();
uriInstance1.path;
```
