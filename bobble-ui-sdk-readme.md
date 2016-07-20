# Bobble UI SDK Doc

### Integrating Bobble SDK in your App

Add this in your build.gradle
```groovy
compile 'com.bobble.android:bobble-android-sdk:x.y.z'
```

Then you are ready to use bobble-sdk

Then initialize it in onCreate() Method of application class, :
```java
BobbleSDK.initialize(getApplicationContext(), CLIENT_ID);

// If you do not have CLIENT_ID , email us to get it at : android@bobbleapp.me
```

If you are using proguard, then add this rule in proguard-project.txt
```
-dontwarn okio.**
-keep class me.bobbleapp.sdk.model.** { *; }
```

### Calling Bobble Onboarding UI:

You need to include bobble onboarding fragment in any of your activity.
```java
// Within the activity
Fragment fragment = BobbleSdk.getOnBoardingFragment();
fragment.init(this)
```

This fragment can be use in your application like this (depending on you use case) :
```java
// Within the activity
FragmentTransaction ft = getSupportFragmentManager().beginTransaction();
ft.replace(R.id.your_placeholder, fragment);
ft.commit();
```

You need to implement BobbleFragmentCallBack in your Activity 
```java
@Override
public void onBobbleOnBoardingSuccess(long bobbleHeadId, Uri uri){

}

@Override
public void onBobbleOnBoardingFailure(String error){

}
```

After OnBoarding completion,either it returns onBobbleOnBoardingSuccess(bobbleHeadID , URI) or onBobbleOnBoardingFailure to the activity.

### Adding BobbleButton in your UI:
```xml
<me.bobbleapp.sdk.widget.BobbleButton
android:id="@+id/bobbleButton"
android:layout_width="48dp"
android:layout_height="48dp"
/>
```          
In this way BobbleButton can be included in any UI

### Adding BobbleStickerView in your UI:
```xml
<me.bobbleapp.sdk.widget.BobbleStickerView
android:id="@+id/bobbleStickerView"
android:layout_width="match_parent"
android:layout_height="match_parent"
app:gif="true"
app:font="false"
app:expression="true"
/>
```
These parameters can be also changed programmatically.

If you are using GIF, Font, you need to compile another dependencies like this
```groovy
compile 'com.bobble.android:bobble-android-sdk-gif:x.y.z'
compile 'com.bobble.android:bobble-android-sdk-font:x.y.z'
```

At the time of including BobbleStickerView, you need to implement onTapListener;
```java
// registering it
bobbleStickerView.init(this);
// This will implement the following methods.
public void onStickerTap(Uri uri){

}
public void onGifTap(Uri uri){

}
```

### Adding BobbleSuggestionView in your UI:
```xml
<me.bobbleapp.sdk.widget.BobbleSuggestionView
android:id="@+id/bobbleSuggestionView"
android:layout_width="wrap_content"
android:layout_height="100dp"
/>
```

Following method are available on this view :
```java
bobbleSuggestionView.update(yourInputText);
bobbleSuggestionView.show();
bobbleSuggestionView.hide();
```

### Getting CoolBobbleText:
```java
String text = BobbleSDK.getCoolBobbleText(yourInputText);
```

### Getting best suggested sticker on the basis of yourInputText at any time:
```java
Bitmap bitmap = BobbleSDK.getSticker(yourInputText,headId);
```

### Getting Personalized Notification Data:
```java
NotificationData notificationData = BobbleSDK.getStickerPackDetails(headId);
```
NotificationData includes following:
```java
public class NotificationData{
  private String smallText;
  private String largeText;
  private String link;
  private Bitmap image;
}
```

### Showing BobbleStickerPreview;
You need to get and load BobbleStickerPreviewFragment like this;
```java
Fragment fragment = new BobbleStickerPreviewFragment(stickerUri);
```

### ShutDown BobbleSDK:
```java
BobbleSDK.shutDown()
```







