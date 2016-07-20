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
<me.bobbleapp.sdk.BobbleButton
android:id="@+id/bobbleButton"
android:layout_width="48dp"
android:layout_height="48dp"
/>
```          





