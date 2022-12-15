# Splash Screen sample app for Fire TV

This project is an Android TV app showcasing how to develop a Splash Screen for Fire TV apps.

As Fire TV devices are running Fire OS (based on Android 11 or lower) currently you cannot use the
Android 12 new SplashScreen APIs as described in [https://developer.android.com/develop/ui/views/launch/splash-screen](https://developer.android.com/develop/ui/views/launch/splash-screen).

You can follow this guide and check this repository to develop your custom splash screen

## 💻 Building the Splash Screen TV demo

1. Clone the following repository:

`git clone git@github.com:giolaq/splash-screen-fire-tv-demo.git`

2. Connect your Fire TV device following these [instructions](https://developer.amazon.com/docs/fire-tv/connecting-adb-to-device.html)

3. Run the app


## How to develop a custom splash screen for your Fire TV Apps

**Step 1:** Create your custom splash screen

Create a file named splashscreen.xml in the drawable directory. This file will contain all the graphic elements and layers of your splash screen, such as the background color and the main graphic. This file should have the following markup:
```xml
<?xml version="1.0" encoding="utf-8"?>
<layer-list xmlns:android="http://schemas.android.com/apk/res/android" android:opacity="opaque">
    <item>
        <shape android:shape="rectangle">
            <solid android:color="@android:color/white"/>
        </shape>
    </item>

    <item android:drawable="@drawable/splashscreen_logo" android:gravity="center"/>

</layer-list>
```

*Note:* The SVG (Scalable Vector Graphics) image format load faster compared to other image formats when testing on FireTV devices.

**Step 2:** Create the splash screen theme

Define a new style in the file styles.xml of your project then add an android:windowBackground item set as the @drawable/splashscreen splash screen you created in the prior step:

 ```xml
    <style name="SplashScreenTheme" parent="Theme.SplashScreenTV.NoActionBar">
        <item name="android:windowBackground">@drawable/splashscreen</item>
    </style>
```

**Step 3:** Create the splash screen activity

Create a new activity responsible for displaying the splash screen, launch the main activity, then terminate:

```kotlin
class SplashScreenActivity : AppCompatActivity() {

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)

        startActivity(Intent(this, MainActivity::class.java))
        finish()
    }
}
```
**Step 4:** Apply the splash screen theme to the splash screen activity

In AndroidManifest.xml, set the theme attribute of the SplashScreenActivity to the theme you setup in step 2. The SplashScreenActivity will be the first activity called by the launcher, so remember to move the intent filter with the action android.intent.action.MAIN and category android.intent.category.LEANBACK_LAUNCHER from the Main Activity to the SplashScreenActivity:

```xml
<activity
    android:name=".SplashScreenActivity"
    android:exported="true"
    android:label="@string/title_activity_splash_screen"
    android:theme="@style/SplashScreenTheme">
    <intent-filter>
        <action android:name="android.intent.action.MAIN" />

        <category android:name="android.intent.category.LEANBACK_LAUNCHER" />
    </intent-filter>
</activity>
```

## Success: Your custom splash screen is now complete!

You have now implemented a custom splash screen and optimized the starting time of your Fire TV app displaying your branding image. To test this for yourself, use the Android Debug Bridge and follow our docs on installing your app on Fire TV (https://developer.amazon.com/docs/fire-tv/installing-and-running-your-app.html).

![splash screen at cold start](images/splashscreen.gif)

## Get support

If you found a bug or want to suggest a new [feature/use case/sample], please [file an issue](../../issues).

If you have questions, comments, or need help with code, we're here to help:
- on Twitter at [@AmazonAppDev](https://twitter.com/AmazonAppDev)
- on Stack Overflow at the [amazon-appstore](https://stackoverflow.com/questions/tagged/amazon-appstore) tag

Sign up to [stay updated with the developer newsletter](https://m.amazonappservices.com/subscribe-newsletter).

## Authors

- [@giolaq](https://twitter.com/giolaq)
