# Managing User Albums

The **photoAccessHelper** module provides APIs for user album management, including creating or deleting a user album, adding images and videos to a user album, and deleting image and videos from a user album.

> **NOTE**
>
> Before you start, you need to obtain a **PhotoAccessHelper** instance and apply for required permissions. For details, see [photoAccessHelper Overview](photoAccessHelper-overview.md).<br>
> By default, the **PhotoAccessHelper** instance obtained in [photoAccessHelper Overview](photoAccessHelper-overview.md) is used when **photoAccessHelper** APIs are used. If the code for obtaining the **PhotoAccessHelper** instance is not added, an error indicating that **photoAccessHelper** is not defined is reported.

To ensure application running efficiency, most **photoAccessHelper** APIs are asynchronously implemented in callback or promise mode. The following code samples use promise-based APIs. For details about the APIs, see [Album Management](../reference/apis/js-apis-photoAccessHelper.md).
Unless otherwise specified, all the media assets to be obtained in this document exist in the database. If no media asset is obtained when the sample code is executed, check whether the media assets exist in the database.

## Creating a User Album

Use [createAlbum](../reference/apis/js-apis-photoAccessHelper.md#createalbum) to create a user album.

The album name must meet the following requirements:

- The album name is a string of 1 to 255 characters.
- The album name cannot contain any of the following characters:<br>\ / : * ? " ' ` < > | { } [ ]
- The album name is case-insensitive.
- Duplicate album names are not allowed.

**Prerequisites**

- A **PhotoAccessHelper** instance is obtained.
- The application has the **ohos.permission.WRITE_IMAGEVIDEO** permission.

Example: Create a user album.

**How to Develop**

1. Set the name of the album.
2. Use **createAlbum** to create an album.

```ts
import photoAccessHelper from '@ohos.file.photoAccessHelper';

try {
  let albumName = 'albumName';
  let album: photoAccessHelper.Album = await phAccessHelper.createAlbum(albumName);
  console.info('createAlbum successfully, album: ' + album.albumName + ' album uri: ' + album.albumUri);
} catch (err) {
  console.error('createAlbum failed with err: ' + err);
}
```

## Obtaining a User Album

Use [getAlbums](../reference/apis/js-apis-photoAccessHelper.md#getalbums) to obtain a user album.

**Prerequisites**

- A **PhotoAccessHelper** instance is obtained.
- The application has the **ohos.permission.READ_IMAGEVIDEO** permission.

Example: Obtain the user album named **albumName**.

**How to Develop**

1. Set **fetchOptions** for obtaining the user album.
2. Call **getAlbums** to obtain user albums.
3. Call [FetchResult.getFirstObject](../reference/apis/js-apis-photoAccessHelper.md#getfirstobject) to obtain the first user album.

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';
import photoAccessHelper from '@ohos.file.photoAccessHelper';

let predicates: dataSharePredicates.DataSharePredicates = new dataSharePredicates.DataSharePredicates();
let albumName: photoAccessHelper.AlbumKeys.ALBUM_NAME  = photoAccessHelper.AlbumKey.ALBUM_NAME;
predicates.equalTo(albumName, 'albumName');
let fetchOptions: photoAccessHelper.FetchOptions = {
  fetchColumns: [],
  predicates: predicates
};

try {
  let fetchResult: photoAccessHelper.FetchResult<photoAccessHelper.Album> = await phAccessHelper.getAlbums(photoAccessHelper.AlbumType.USER, photoAccessHelper.AlbumSubtype.USER_GENERIC, fetchOptions);
  let album: photoAccessHelper.Album = await fetchResult.getFirstObject();
  console.info('getAlbums successfully, albumName: ' + album.albumName);
  fetchResult.close();
} catch (err) {
  console.error('getAlbums failed with err: ' + err);
}
```

## Renaming a User Album

Modify the **Albums.albumName** attribute of the album, and use [Album.commitModify](../reference/apis/js-apis-photoAccessHelper.md#commitmodify-2) to update the modification to the database.

Before renaming a user album, you need to obtain an album object. You can use the [FetchResult](../reference/apis/js-apis-photoAccessHelper.md#fetchresult) APIs to obtain the user album of the specified location.

The new user album names must also comply with the user name requirements in [Creating a User Album](#creating-a-user-album).

**Prerequisites**

- A **PhotoAccessHelper** instance is obtained.
- The application has the **ohos.permission.READ_IMAGEVIDEO** and **ohos.permission.WRITE_IMAGEVIDEO** permissions.

Example: Rename an album named **albumName**.

**How to Develop**

1. Set **fetchOptions** for obtaining the user album.
2. Call **getAlbums** to obtain user albums.
3. Call [FetchResult.getFirstObject](../reference/apis/js-apis-photoAccessHelper.md#getfirstobject) to obtain the first user album.
4. Set a new album name.
5. Call **Album.commitModify** to update the new album name to the database.

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';
import photoAccessHelper from '@ohos.file.photoAccessHelper';

let predicates: dataSharePredicates.DataSharePredicates = new dataSharePredicates.DataSharePredicates();
let albumName: photoAccessHelper..AlbumKeys.ALBUM_NAME = photoAccessHelper.AlbumKey.ALBUM_NAME;
predicates.equalTo(albumName, 'albumName');
let fetchOptions: photoAccessHelper.FetchOptions = {
  fetchColumns: [],
  predicates: predicates
};

try {
  let fetchResult: photoAccessHelper.FetchResult<photoAccessHelper.Album> = await phAccessHelper.getAlbums(photoAccessHelper.AlbumType.USER, photoAccessHelper.AlbumSubtype.USER_GENERIC, fetchOptions);
  let album: photoAccessHelper.Album = await fetchResult.getFirstObject();
  console.info('getAlbums successfully, albumName: ' + album.albumName);
  album.albumName = 'newAlbumName';
  await album.commitModify();
  fetchResult.close();
} catch (err) {
  console.error('commitModify failed with err: ' + err);
}
```

## Adding Images or Videos to a User Album

[Obtain the user album](#obtaining-a-user-album) and the images or videos to be added to the album, and then call [Album.addAssets](../reference/apis/js-apis-photoAccessHelper.md#addassets) to add the images or videos to the user album.

**Prerequisites**

- A **PhotoAccessHelper** instance is obtained.
- The application has the **ohos.permission.READ_IMAGEVIDEO** and **ohos.permission.WRITE_IMAGEVIDEO** permissions.

Example: Add an image to the album **albumName**.

**How to Develop**

1. Set **albumFetchOptions** for obtaining the user album.
2. Set **photoFetchOptions** for obtaining the image.
3. Call **getAlbums** to obtain user albums.
4. Call [FetchResult.getFirstObject](../reference/apis/js-apis-photoAccessHelper.md#getfirstobject) to obtain the first user album.
5. Call [PhotoAccessHelper.getAssets](../reference/apis/js-apis-photoAccessHelper.md#getassets) to obtain image assets.
6. Call [FetchResult.getFirstObject](../reference/apis/js-apis-photoAccessHelper.md#getfirstobject) to obtain the first image from the result set.
7. Call **Album.addAssets** to add the image to the user album.

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';
import photoAccessHelper from '@ohos.file.photoAccessHelper';

let albumPredicates: dataSharePredicates.DataSharePredicates = new dataSharePredicates.DataSharePredicates();
let albumName: photoAccessHelper..AlbumKeys.ALBUM_NAME = photoAccessHelper.AlbumKey.ALBUM_NAME;
albumPredicates.equalTo(albumName, 'albumName');
let albumFetchOptions: dataSharePredicates.FetchOptions = {
  fetchColumns: [],
  predicates: albumPredicates
};

let photoPredicates: dataSharePredicates.DataSharePredicates = new dataSharePredicates.DataSharePredicates();
let photoFetchOptions: photoAccessHelper.FetchOptions = {
  fetchColumns: [],
  predicates: photoPredicates
};

try {
  let albumFetchResult: photoAccessHelper.FetchResult<photoAccessHelper.Album> = await phAccessHelper.getAlbums(photoAccessHelper.AlbumType.USER, photoAccessHelper.AlbumSubtype.USER_GENERIC, albumFetchOptions);
  let album: photoAccessHelper.Album = await albumFetchResult.getFirstObject();
  console.info('getAlbums successfully, albumName: ' + album.albumName);
  let photoFetchResult: photoAccessHelper.FetchResult<photoAccessHelper.PhotoAsset> = await phAccessHelper.getAssets(photoFetchOptions);
  let fileAsset: photoAccessHelper.PhotoAsset = await photoFetchResult.getFirstObject();
  console.info('getAssets successfully, albumName: ' + fileAsset.displayName);
  await album.addAssets([fileAsset]);
  albumFetchResult.close();
  photoFetchResult.close();
} catch (err) {
  console.error('addAssets failed with err: ' + err);
}
```

## Obtaining Images and Videos in a User Album

[Obtain the user album](#obtaining-a-user-album), and call [Album.getAssets](../reference/apis/js-apis-photoAccessHelper.md#getassets-2) to obtain the media assets in the user album.

**Prerequisites**

- A **PhotoAccessHelper** instance is obtained.
- The application has the **ohos.permission.READ_IMAGEVIDEO** and **ohos.permission.WRITE_IMAGEVIDEO** permissions.

Example: Obtain an image in the user album **albumName**.

**How to Develop**

1. Set **albumFetchOptions** for obtaining the user album.
2. Set **photoFetchOptions** for obtaining the image.
3. Call **getAlbums** to obtain user albums.
4. Call [FetchResult.getFirstObject](../reference/apis/js-apis-photoAccessHelper.md#getfirstobject) to obtain the first user album.
5. Call **Album.getAssets** to obtain the image assets in the user album.
6. Call [FetchResult.getFirstObject](../reference/apis/js-apis-photoAccessHelper.md#getfirstobject) to obtain the first image from the result set.

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';
import photoAccessHelper from '@ohos.file.photoAccessHelper';

let albumPredicates: dataSharePredicates.DataSharePredicates = new dataSharePredicates.DataSharePredicates();
let albumName: photoAccessHelper.AlbumKeys = photoAccessHelper.AlbumKey.ALBUM_NAME;
albumPredicates.equalTo(albumName, 'albumName');
let albumFetchOptions: photoAccessHelper.FetchOptions = {
  fetchColumns: [],
  predicates: albumPredicates
};

let photoPredicates: dataSharePredicates.DataSharePredicates = new dataSharePredicates.DataSharePredicates();
let photoFetchOptions: photoAccessHelper.FetchOptions = {
  fetchColumns: [],
  predicates: photoPredicates
};

try {
  let albumFetchResult: photoAccessHelper.FetchResult<photoAccessHelper.Album> = await phAccessHelper.getAlbums(photoAccessHelper.AlbumType.USER, photoAccessHelper.AlbumSubtype.USER_GENERIC, albumFetchOptions);
  let album: photoAccessHelper.Album = await albumFetchResult.getFirstObject();
  console.info('getAlbums successfully, albumName: ' + album.albumName);
  let photoFetchResult: photoAccessHelper.FetchResult<photoAccessHelper.PhotoAsset> = await album.getAssets(photoFetchOptions);
  let fileAsset: photoAccessHelper.PhotoAsset = await photoFetchResult.getFirstObject();
  console.info('album getAssets successfully, albumName: ' + fileAsset.displayName);
  albumFetchResult.close();
  photoFetchResult.close();
} catch (err) {
  console.error('album getAssets failed with err: ' + err);
}
```

## Removing Images and Videos from a User Album

[Obtain the user album](#obtaining-a-user-album), and call [Album.getAssets](../reference/apis/js-apis-photoAccessHelper.md#getassets-2) to obtain the media assets in the user album.

Use [Album.removeAssets](../reference/apis/js-apis-photoAccessHelper.md#removeassets) to remove the specified media assets.

**Prerequisites**

- A **PhotoAccessHelper** instance is obtained.
- The application has the **ohos.permission.READ_IMAGEVIDEO** and **ohos.permission.WRITE_IMAGEVIDEO** permissions.

Example: Remove an image from the album named **albumName**.

**How to Develop**

1. Set **albumFetchOptions** for obtaining the user album.
2. Set **photoFetchOptions** for obtaining the image.
3. Call **getAlbums** to obtain user albums.
4. Call [FetchResult.getFirstObject](../reference/apis/js-apis-photoAccessHelper.md#getfirstobject) to obtain the first user album.
5. Call **Album.getAssets** to obtain the image assets.
6. Call [FetchResult.getFirstObject](../reference/apis/js-apis-photoAccessHelper.md#getfirstobject) to obtain the first image from the result set.
7. Call **Album.removeAssets** to remove the image from the user album.

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';
import photoAccessHelper from '@ohos.file.photoAccessHelper';

let albumPredicates: dataSharePredicates.DataSharePredicates = new dataSharePredicates.DataSharePredicates();
let albumName: photoAccessHelper.AlbumKeys.ALBUM_NAME = photoAccessHelper.AlbumKey.ALBUM_NAME;
albumPredicates.equalTo(albumName, 'albumName');
let albumFetchOptions: photoAccessHelper.FetchOptions = {
  fetchColumns: [],
  predicates: albumPredicates
};

let photoPredicates: dataSharePredicates.DataSharePredicates = new dataSharePredicates.DataSharePredicates();
let photoFetchOptions: photoAccessHelper.FetchOptions = {
  fetchColumns: [],
  predicates: photoPredicates
};

try {
  let albumFetchResult: photoAccessHelper.FetchResult<photoAccessHelper.Album> = await phAccessHelper.getAlbums(photoAccessHelper.AlbumType.USER, photoAccessHelper.AlbumSubtype.USER_GENERIC, albumFetchOptions);
  let album: photoAccessHelper.Album = await albumFetchResult.getFirstObject();
  console.info('getAlbums successfully, albumName: ' + album.albumName);
  let photoFetchResult: photoAccessHelper.FetchResult<photoAccessHelper.PhotoAsset> = await album.getAssets(photoFetchOptions);
  let fileAsset: photoAccessHelper.PhotoAsset = await photoFetchResult.getFirstObject();
  console.info('album getAssets successfully, albumName: ' + fileAsset.displayName);
  await album.removeAssets([fileAsset]);
  albumFetchResult.close();
  photoFetchResult.close();
} catch (err) {
  console.error('removeAssets failed with err: ' + err);
}
```

## Deleting a User Album

[Obtain the user album](##obtaining-a-user-album), and call [deleteAlbums](../reference/apis/js-apis-photoAccessHelper.md#deletealbums) to delete the user album.

**Prerequisites**

- A **PhotoAccessHelper** instance is obtained.
- The application has the **ohos.permission.READ_IMAGEVIDEO** and **ohos.permission.WRITE_IMAGEVIDEO** permissions.

Example: Delete a user album named **albumName**.

**How to Develop**

1. Set **fetchOptions** for obtaining the user album.
2. Call **getAlbums** to obtain user albums.
3. Call **FetchResult.getFirstObject** to obtain the first user album.
4. Call **deleteAlbums** to delete the user album.

```ts
import dataSharePredicates from '@ohos.data.dataSharePredicates';
import photoAccessHelper from '@ohos.file.photoAccessHelper';

let predicates: dataSharePredicates.DataSharePredicates = new dataSharePredicates.DataSharePredicates();
let albumName: photoAccessHelper.AlbumKeys..ALBUM_NAME = photoAccessHelper.AlbumKey.ALBUM_NAME;
predicates.equalTo(albumName, '%albumName%');
let fetchOptions: photoAccessHelper.FetchOptions = {
  fetchColumns: [],
  predicates: predicates
};

try {
  let fetchResult: photoAccessHelper.FetchResult<photoAccessHelper.Album> = await phAccessHelper.getAlbums(photoAccessHelper.AlbumType.USER, photoAccessHelper.AlbumSubtype.USER_GENERIC, fetchOptions);
  let album: photoAccessHelper.Album = await fetchResult.getFirstObject();
  console.info('getAlbums successfully, albumName: ' + album.albumName);
  phAccessHelper.deleteAlbums([album]);
  fetchResult.close();
} catch (err) {
  console.error('deleteAlbums failed with err: ' + err);
}
```
