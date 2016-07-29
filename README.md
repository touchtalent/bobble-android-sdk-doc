# bobble-android-sdk

## Overview

Bobble SDK for Android enables you to create bobble heads, on the fly stickers, from within your application. 

Bobble SDK offers an array of features to you:

- Create bobblified heads
- Select preferred head
- Fetch all stickers categories(packs)
- Fetch all stickers for a given sticker category
- Create OTF Stickers
and many more.

This guide is intended to assist Android developers who want to embed Bobble SDK into their Android Applications. The guide explains step-by-step process to integrate SDK in your application.

Note -	Minimum version of supported Android platform is SDK level 15

## Concepts

#### Bobblified head
 The bobble head created after processing an image

#### Sticker category
Sticker Pack, Collection of stickers.

#### OTF Stickers
Stickers created with on the fly text



## Integrating Bobble SDK in your App

Add this in your build.gradle`

```groovy
compile 'com.bobble.android:bobble-android-sdk:0.3.0'
```

Then you are ready to use bobbleSDK


##### 
Then initialize it in onCreate() Method of application class, :

```java
BobbleSDK.initialize(getApplicationContext(), CLIENT_ID);

// If you do not have CLIENT_ID , email us to get it at : android@bobbleapp.me
```

If you are using proguard, then add this rule in proguard-project.txt

```
-dontwarn okio.**

-keep class me.bobbleapp.sdk.model.** { *; }

-keepclassmembers class * extends de.greenrobot.dao.AbstractDao {
    public static java.lang.String TABLENAME;
}

-keep class **$Properties
```


 Initialize the SDK before executing any other operations,
 
 Now you call BobbleSDK methods:
 
 call BobbleSDK.isReady to check if SDK is ready to do
something or not

```java
 boolean isBobbleReady = BobbleSDK.isReady();
```

 for checking image pass either bitmap or path of bitmap and
listerner for faceDetection:

```java
 BobbleSDK.checkImage(bitmap, new FaceDetectionListener() {
 
  @Override
   public void onSingleFaceDetection(RectF faceRectF) {
   Log.d(Constants.TAG, " onSingleFaceDetection with
   bitmap parameter :" + faceRectF.toString());
  }
 
  @Override
   public void onMultipleFaceDetection(List<RectF>
   facesRectFList) {
   Log.d(Constants.TAG, " onMultipleFaceDetection with
   bitmap parameter :" + facesRectFList.toString());
  }
 
  @Override
   public void onNoFaceDetection() {
   Log.d(Constants.TAG, " onNoFaceDetection with bitmap
   parameter ");
  }
 
  @Override
   public void onError(String error) {
   Log.d(Constants.TAG, " onError : " + error);
  }
  
 });
```

 To get BobbleImage : pass path or bitmap, gender and
listerner

```java
 BobbleSDK.bobblify(path, "female", new
  BobblificationListener() {
  
  @Override
  public void onBobblificationComplete(long faceId) {

  }
  
  @Override
  public void onError(String error) {

  }
  
 });
 ```
 
 To get all faces:
 ```java
 BobbleSDK.getAllFaces();
 ```
 
 To get all bobbleHeads
 
 ```java
 BobbleSDK.getAllBobbleHead();
 ```
 
 To get the list of downloaded sticker category
 ```java
 BobbleSDK.getAllStickerCategory();
 ```
 
 To get the list of downloaded sticker category
 
 ```java
 BobbleSDK.getPreferredBobbleHeadForFaceId(faceId);
 ```
 
 To get the list of sticker of a sticker category

 ```java
BobbleSDK.getStickerListForStickerCategoryId(stickerCategoryId,bobbl
eHead);
 ```
 
 To get the list of stickerCategory : pass limit , page and
a listener

 ```java
 BobbleSDK.getApiStickerCategoryList(10, 1, new
  ApiStickerCategoryListListener() {
  
  @Override
  public void onSuccess(List<ApiStickerCategory>
  apiStickerCategoryList) {
  Log.d(TAG, "apiStickerCategoryList size " +
  apiStickerCategoryList.size());
  }
  
  @Override
  public void onError(String error) {
   Log.d(TAG, "onError");
  }
 });
  ```
  
 To download a stickerCategory
  ```
 BobbleSDK.downloadStickerCategoryForId(stickerCategoryId);
  ```
  
 To get sticker : pass the bobbleHead , sticker and
listener
 ```java
 BobbleSDK.createSticker(bobbleHead, sticker, new
  StickerCreationListener() {
  
 @Override
  public void onStickerCreationComplete(Bitmap bitmap){

  }
  
 @Override
  public void onError(String error) {

  }
 });
  ```
  
 To get OnTheFly sticker : pass the bobbleHead , sticker,
text and listener
 ```java
 BobbleSDK.createStickerOnTheFly(bobbleHead, sticker, "This
    is a test message", new StickerCreationListener() {
    
 @Override
  public void onStickerCreationComplete(Bitmap bitmap) {
  
  }
  
 @Override
  public void onError(String error) {

  }
 });
 ```
 Call BobbleSDK.shutDown() to shutDown BobbleSDK
 
# APIs

## 1. initialize

 ```java
public static void initialize(Context context, String clientId) 
 ```
 
You should invoke initialize API from your landing activity.
This API accepts two arguments, context and client id,  context for application context and client id is used to authenticate and authorize your application with Bobble server. Both of the arguments cannot be Null.


## 2. isReady
 ```java
 public static boolean isReady()
  ```
Method to check if SDK is ready to do something.


## 3. shutDown
 ```java
public static void shutDown() 
 ```
Method to close bobble SDK instance.


Precondition:- SDK should be enabled

## 4. checkImage
 ```java
public static void checkImage(Bitmap bitmap, final FaceDetectionListener faceDetectionListener)
 ```
 ```java

public static void checkImage(String path, final FaceDetectionListener faceDetectionListener)
 ```

This is to test Face detection - Single Face,  Multiple faces or No face detected scenarios

First argument can be image or image path.(Path cannot be Null)

Preconditions - SDK should be enabled and Bobble should be ready.


## 5. bobblify
 ```java
public static void bobblify(String path, String gender, BobblificationListener bobblificationListener)
 ```
  ```java
public static void bobblify(Bitmap bitmap, String gender, BobblificationListener bobblificationListener)
 ```
 
This method is to create boblified heads. 

First argument is image or image path. Second argument “gender” can have 2 values - male or female. 

Preconditions - SDK should be enabled. Bobble should be ready. Image/Path and Gender cannot be null.

## 6. createSticker
 ```java
public static void createSticker(final BobbleHead bobbleHead, final Sticker sticker, final StickerCreationListener stickerCreationListener)
 ```
 
This method is for creating stickers. The first argument is for bobblified head and second is for selected sticker.

Precondition - SDK should be enabled

## 7. createStickerOnTheFly
 ```java
public static void createStickerOnTheFly(final BobbleHead bobbleHead, final Sticker sticker, String text, final StickerCreationListener stickerCreationListener) 
 ```
 
To create stickers with OTF text.
First argument accepts bobblified head, second argument is for selected sticker, third argument is for OTF text (this value should not be Null). 

Precondition - SDK should be enabled

## 8.  getAllFaces
 ```java
public static List<Face> getAllFaces()
 ```
 
To get all faces. This will return a list of faces. 

## 9. getAllBobbleHeads
 ```java
public static List<BobbleHead> getAllBobbleHeads()
 ```
 
To get a list of all bobblified heads for all faces

## 10. getBobbleHeadForFaceId
 ```java
public static List<BobbleHead> getBobbleHeadForFaceId(final long faceId)
 ```
To get list of all bobblified heads for a particular faceId


## 11.  getPreferredBobbleHeadForFaceId
 ```java
public static BobbleHead getPreferredBobbleHeadForFaceId(final long faceId) 
 ```
This will return the preferred head for a particular faceId, the priority is set by server.

Note:  SDK must be enabled and headList should not be null or zero


## 12. getAllStickerCategory
 ```java
public static List<StickerCategory> getAllStickerCategory()
 ```
 
To get list of all the sticker packs


## 13. getStickerListForStickerCategoryId
 ```java
public static List<Sticker> getStickerListForStickerCategoryId(final long stickerCategoryId, final BobbleHead bobbleHead)
 ```
To fetch all sticker for a particular stickercategory id. It accepts two arguments, first is stickercategoryid which is unique id for each stickercategory, second is bobblified head.

## 14. getStickerList
 ```java
public static List<Sticker> getStickerList(final BobbleHead bobbleHead)
 ```
To fetch all sticker corresponding to a bobbleHead.


## 15.  getApiStickerCategoryList
```java
public static void getApiStickerCategoryList(int limit, int page, final ApiStickerCategoryListListener apiStickerCategoryListListener) 
 ```
 
To get pagewise sticker categories list. Arguments are :- 

1. limit numeric value to set limit, this should not be changed in a session

2. page to set no. of pages

## 16. downloadStickerCategoryForId
 ```java
public static void downloadStickerCategoryForId(long id, final DownloadListener downloadListener) 
 ```

It accepts sticker category id as an argument to download the pack.

## 17. deleteSticker
 ```java
public static void deleteSticker(long stickerId, final DeleteListener deleteListener) 
 ```

It accepts sticker id as an argument to delete the sticker.

## 18. deleteStickerCategory
 ```java
public static void deleteStickerCategory(long stickerCategoryId, final DeleteListener deleteListener) 
 ```

It accepts sticker category id as an argument to delete the sticker category.

## 19. deleteFace
 ```java
public static void deleteFace(long faceId, final DeleteListener deleteListener) 
 ```

It accepts face id as an argument to delete the face and the associated bobble heads.

## 20. deleteBobbleHead
 ```java
public static void deleteBobbleHead(long bobbleHeadId, final DeleteListener deleteListener) 
 ```

It accepts bobble head id as an argument to delete the bobble head.

## 21. seed
 ```java
public static void seed(int rawResId, final SeedListener seedListener) 
 ```

It accepts raw resource id as an argument.

 ```java
public static void seed(String zipPath, final SeedListener seedListener) 
 ```

It accepts zip path as an argument.


