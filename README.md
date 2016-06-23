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

```
compile 'com.bobble.android:bobble-android-sdk:0.2.0'
```

Then you are ready to use bobbleSDK


##### 
Then initialize it in onCreate() Method of application class, :

```
BobbleSDK.initialize(getApplicationContext(), CLIENT_ID);

// If you do not have CLIENT_ID , email us to get it at : android@bobbleapp.me

 ```
 
 Initialize the SDK before executing any other operations,
 
 Now you call BobbleSDK methods:
 
 call BobbleSDK.isReady to check if SDK is ready to do
something or not

```
 boolean isBobbleReady = BobbleSDK.isReady();
```

 for checking image pass either bitmap or path of bitmap and
listerner for faceDetection:

```
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

```
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
 ```
 BobbleSDK.getAllFaces();
 ```
 
 To get all bobbleHeads
 
 ```
 BobbleSDK.getAllBobbleHead();
 ```
 
 To get the list of downloaded sticker category
 ```
 BobbleSDK.getAllStickerCategory();
 ```
 
 To get the list of downloaded sticker category
 
 ```
 BobbleSDK.getPreferredBobbleHeadForFaceId(faceId);
 ```
 
 To get the list of sticker of a sticker category

 ```
BobbleSDK.getStickerListForStickerCategoryId(stickerCategoryId,bobbl
eHead);
 ```
 
 To get the list of stickerCategory : pass limit , page and
a listener

 ```
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
 ```
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
 ```
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

 ```
public static void initialize(Context context, String clientId) 
 ```
 
You should invoke initialize API from your landing activity.
This API accepts two arguments, context and client id,  context for application context and client id is used to authenticate and authorize your application with Bobble server. Both of the arguments cannot be Null.


## 2. isReady
 ```
 public static boolean isReady()
  ```
Method to check if SDK is ready to do something.


## 3. shutDown
 ```
public static void shutDown() 
 ```
Method to close bobble SDK instance.


## 4. generateAccessToken
 ```
public static void generateAccessToken()
 ```
method to generate access token for validation. 

Precondition:- SDK should be enabled

## 5. checkImage
 ```
public static void checkImage(Bitmap bitmap, final FaceDetectionListener faceDetectionListener)
 ```
 ```

public static void checkImage(String path, final FaceDetectionListener faceDetectionListener)
 ```

This is to test Face detection - Single Face,  Multiple faces or No face detected scenarios

First argument can be image or image path.(Path cannot be Null)

Preconditions - SDK should be enabled and Bobble should be ready.


## 6. bobblify
 ```
public static void bobblify(String path, String gender, BobblificationListener bobblificationListener)
 ```
  ```
public static void bobblify(Bitmap bitmap, String gender, BobblificationListener bobblificationListener)
 ```
 
This method is to create boblified heads. 

First argument is image or image path. Second argument “gender” can have 2 values - male or female. 

Preconditions - SDK should be enabled. Bobble should be ready. Image/Path and Gender cannot be null.

## 7. createSticker
 ```
public static void createSticker(final BobbleHead bobbleHead, final Sticker sticker, final StickerCreationListener stickerCreationListener)
 ```
 
This method is for creating stickers. The first argument is for bobblified head and second is for selected sticker.

Precondition - SDK should be enabled

## 8. createStickerOnTheFly
 ```
public static void createStickerOnTheFly(final BobbleHead bobbleHead, final Sticker sticker, String text, final StickerCreationListener stickerCreationListener) 
 ```
 
To create stickers with OTF text.
First argument accepts bobblified head, second argument is for selected sticker, third argument is for OTF text (this value should not be Null). 

Precondition - SDK should be enabled

## 9.  getAllFaces
 ```
public static List<Face> getAllFaces()
 ```
 
To get all faces. This will return a list of faces. 

## 10. getAllBobbleHeads
 ```
public static List<BobbleHead> getAllBobbleHeads()
 ```
 
To get a list of all bobblified heads for all faces

## 11. getBobbleHeadForFaceId
 ```
public static List<BobbleHead> getBobbleHeadForFaceId(final long faceId)
 ```
To get list of all bobblified heads for a particular faceId


## 12.  getPreferredBobbleHeadForFaceId
 ```
public static BobbleHead getPreferredBobbleHeadForFaceId(final long faceId) 
 ```
This will return the preferred head for a particular faceId, the priority is set by server.

Note:  SDK must be enabled and headList should not be null or zero


## 13. getAllStickerCategory
 ```
public static List<StickerCategory> getAllStickerCategory()
 ```
 
To get list of all the sticker packs


## 14. getStickerListForStickerCategoryId
 ```
public static List<Sticker> getStickerListForStickerCategoryId(final long stickerCategoryId, final BobbleHead bobbleHead)
 ```
To fetch all sticker for a particular stickercategory id. It accepts two arguments, first is stickercategoryid which is unique id for each stickercategory, second is bobblified head.


## 15.  getApiStickerCategoryList
```
public static void getApiStickerCategoryList(int limit, int page, final ApiStickerCategoryListListener apiStickerCategoryListListener) 
 ```
 
To get pagewise sticker categories list. Arguments are :- 

1. limit numeric value to set limit, this should not be changed in a session

2. page to set no. of pages

## 16. downloadStickerCategoryForId
 ```
public static void downloadStickerCategoryForId(long id, final DownloadListener downloadListener) 
 ```

It accepts sticker category id as an argument to download the pack.

## 17. deleteSticker
 ```
public static void deleteSticker(long stickerId, final DeleteListener deleteListener) 
 ```

It accepts sticker id as an argument to delete the sticker.

## 18. deleteStickerCategory
 ```
public static void deleteStickerCategory(long stickerCategoryId, final DeleteListener deleteListener) 
 ```

It accepts sticker category id as an argument to delete the sticker category.

## 19. deleteFace
 ```
public static void deleteFace(long faceId, final DeleteListener deleteListener) 
 ```

It accepts face id as an argument to delete the face and the associated bobble heads.

## 20. deleteBobbleHead
 ```
public static void deleteBobbleHead(long bobbleHeadId, final DeleteListener deleteListener) 
 ```

It accepts bobble head id as an argument to delete the bobble head.
