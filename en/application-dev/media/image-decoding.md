# Image Decoding

Image decoding refers to the process of decoding an archived image in a supported format into a [pixel map](image-overview.md) for image display or [processing](image-transformation.md). Currently, the following image formats are supported: JPEG, PNG, GIF, RAW, WebP, BMP, and SVG.

## How to Develop

Read [Image](../reference/apis/js-apis-image.md#imagesource) for APIs related to image decoding.

1. Import the image module.
     
   ```ts
   import image from '@ohos.multimedia.image';
   ```

2. Obtain an image.
   - Method 1: Obtain the sandbox path. For details about how to obtain the sandbox path, see [Obtaining Application File Paths](../application-models/application-context-stage.md#obtaining-application-file-paths). For details about the application sandbox and how to push files to the application sandbox, see [File Management](../file-management/app-sandbox-directory.md).
        
      ```ts
      // Code on the stage model
      const context : Context = getContext(this);
      const filePath : string = context.cacheDir + '/test.jpg';
      ```

      ```ts
      // Code on the FA model
      import featureAbility from '@ohos.ability.featureAbility';
      
      const context = featureAbility.getContext();
      const filePath = context.getCacheDir() + "/test.jpg";
      ```
   - Method 2: Obtain the file descriptor of the image through the sandbox path. For details, see [file.fs API Reference] (../reference/apis/js-apis-file-fs.md).
      To use this method, you must import the \@ohos.file.fs module first.

      ```ts
      import fs from '@ohos.file.fs';
      ```

      Then call **fs.openSync()** to obtain the file descriptor.
  
      ```ts
      // Code on the stage model
      const context = getContext(this);
      const filePath = context.cacheDir + '/test.jpg';
      const file : fs.File = fs.openSync(filePath, fs.OpenMode.READ_WRITE);
      const fd : number = file?.fd;
      ```

      ```ts
      // Code on the FA model
      import featureAbility from '@ohos.ability.featureAbility';
      
      const context = featureAbility.getContext();
      const filePath = context.getCacheDir() + "/test.jpg";
      const file : fs.File = fs.openSync(filePath, fs.OpenMode.READ_WRITE);
      const fd : number = file?.fd;
      ```
   - Method 3: Obtain the array buffer of the resource file through the resource manager. For details, see [ResourceManager API Reference](../reference/apis/js-apis-resource-manager.md#getrawfilecontent9-1).
        
      ```ts
      // Code on the stage model
      const context : Context = getContext(this);
      // Obtain a resource manager.
      const resourceMgr : resourceManager.ResourceManager = context.resourceManager;
      ```

      ```ts
      // Code on the FA model
      // Import the resourceManager module.
      import resourceManager from '@ohos.resourceManager';
      const resourceMgr = await resourceManager.getResourceManager();
      ```

      The method of obtaining the resource manager varies according to the application model. After obtaining the resource manager, call **resourceMgr.getRawFileContent()** to obtain the array buffer of the resource file.

      ```ts
      const fileData : Uint8Array = await resourceMgr.getRawFileContent('test.jpg');
      // Obtain the array buffer of the image.
      const buffer = fileData.buffer;
      ```
   - Method 4: Obtain the raw file descriptor of the resource file through the resource manager. For details, see [ResourceManager API Reference](../reference/apis/js-apis-resource-manager.md#getrawfd9-1).
        
      ```ts
      // Code on the stage model
      const context : Context = getContext(this);
      // Obtain a resource manager.
      const resourceMgr : resourceManager.ResourceManager = context.resourceManager;
      ```

      ```ts
      // Code on the FA model
      // Import the resourceManager module.
      import resourceManager from '@ohos.resourceManager';
      const resourceMgr = await resourceManager.getResourceManager();
      ```

      The method of obtaining the resource manager varies according to the application model. After obtaining the resource manager, call **resourceMgr.getRawFd()** to obtain the raw file descriptor of the resource file.

      ```ts
      const rawFileDescriptor : resourceManager.RawFileDescriptor = await resourceMgr.getRawFd('test.jpg');
      ```


3. Create an **ImageSource** instance.
   - Method 1: Create an **ImageSource** instance using the sandbox path. The sandbox path can be obtained by using method 1 in step 2.
        
      ```ts
      // path indicates the obtained sandbox path.
      const imageSource : image.ImageSource = image.createImageSource(filePath);
      ```
   - Method 2: Create an **ImageSource** instance using the file descriptor. The file descriptor can be obtained by using method 2 in step 2.
        
      ```ts
      // fd is the obtained file descriptor.
      const imageSource : image.ImageSource = image.createImageSource(fd);
      ```
   - Method 3: Create an **ImageSource** instance using an array buffer. The array buffer can be obtained by using method 3 in step 2.
        
      ```ts
      const imageSource : image.ImageSource = image.createImageSource(buffer);
      ```
   - Method 4: Create an **ImageSource** instance using the raw file descriptor of the resource file. The raw file descriptor can be obtained by using method 4 in step 2.
        
      ```ts
      const imageSource : image.ImageSource = image.createImageSource(rawFileDescriptor);
      ```

4. Set **DecodingOptions** and decode the image to obtain a pixel map.
     
   ```ts
   let decodingOptions : image.DecodingOptions = {
       editable: true,
       desiredPixelFormat: 3,
   }
   // Create a pixel map and perform rotation and scaling on it.
   const pixelMap : image.PixelMap = await imageSource.createPixelMap(decodingOptions);
   ```

   After the decoding is complete and the pixel map is obtained, you can perform subsequent [image processing](image-transformation.md).

5. Release the **PixelMap** instance.
   ```ts
   pixelMap.release();
   ```

## Sample Code - Decoding an Image in Resource Files

1. Obtain a resource manager.
     
   ```ts
   const context : Context = getContext(this);
   // Obtain a resource manager.
   const resourceMgr : resourceManager.ResourceManager = context.resourceManager;
   ```

2. Create an **ImageSource** instance.
   - Create an **ImageSource** instance by using the array buffer of **test.jpg** in the **rawfile** folder.
     ```ts
     const fileData : Uint8Array = await resourceMgr.getRawFileContent('test.jpg');
     // Obtain the array buffer of the image.
     const buffer = fileData.buffer;

     const imageSource : image.ImageSource = image.createImageSource(buffer);
     ```

   - Create an **ImageSource** instance by using the raw file descriptor of **test.jpg** in the **rawfile** folder.
     ```ts
     const rawFileDescriptor : resourceManager.RawFileDescriptor = await resourceMgr.getRawFd('test.jpg');

     const imageSource : image.ImageSource = image.createImageSource(rawFileDescriptor);
     ```
3. Create a **PixelMap** instance.
     
   ```ts
   const pixelMap : image.PixelMap = await imageSource.createPixelMap();
   ```

4. Release the **PixelMap** instance.
   ```ts
   pixelMap.release();
   ```
