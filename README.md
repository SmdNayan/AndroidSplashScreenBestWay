# Android Splash Screen Best Case
When our app is lanch we always try to add a splash (Lancher) Screen. But If we add a normal splash screen like using using Activity and a layout file 
it's always give a boring black/with screen before lanch splash screen. But I try to solve this problem using best case to make a splash screen.
After complete full implementation. The result is: 
![Result](../data/example.gif?raw=true)

## Implementation
In here we implement an splash screen that don't show any black/white screen before launch. Also, we don't need any extra `Splash Screen Activity` and `Layout` file.
First, I make a lancher drawable file using background color and logo. Then make a custom `Theme` using `Style` file. 
After that I lancher drawable file from it from the custom `Theme`. Then I call custom theme from the `AndroidMenifest.xml` and set to the ManiActivity `android:theme="@style/AppTheme"`
Then set the theme for `MainActivity.class` befor `super.onCreate()`

###### Step-1
Make drawable file using backgroud color and app logo. Also, We can use custom `.png` file.

```
<layer-list xmlns:android="http://schemas.android.com/apk/res/android">

    <!-- Splash screen background-->
    <item android:drawable="@drawable/splash_background" />

    <!-- Splash screen logo (Also make it center) -->
    <item>
        <bitmap android:src="@drawable/ic_splah"
            android:gravity="center"/>
    </item>

</layer-list>
```

If use a full screen background image like `.png` file. then use below code 
```
<layer-list xmlns:android="http://schemas.android.com/apk/res/android">

    <!-- Add splash png file drawable here  -->
    <item android:drawable="@drawable/ic_splash_with_background"/>

</layer-list>
```

###### Step-2
Here I make the custom theme `AppTheme.Lancher`. Add below code to your `style.xml` file find on `res/values/style.xml`
```
<!--Splash screen theme -->
<style name="AppTheme.Launcher">
    <item name="android:windowBackground">@drawable/lancher_with_bg_and_icon</item>
    <item name="android:windowNoTitle">true</item>
    <item name="android:windowActionBar">false</item>
     <item name="android:windowFullscreen">true</item>
    <item name="android:windowContentOverlay">@null</item>
</style>
```

###### Step-3 
Then add the custom theme `AppTheme.Lancher` on `AndroidMenifest.xml` file. Follow the below code:
```
<activity android:name=".MainActivity"
        android:theme="@style/AppTheme.Launcher">
        <intent-filter>
            <action android:name="android.intent.action.MAIN" />

            <category android:name="android.intent.category.LAUNCHER" />
        </intent-filter>
</activity>
```

###### Step-4
Then call `app theme` from `mainActivity.class` before `super.onCreate()` 
```
public class MainActivity extends AppCompatActivity {
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        //Set the theme before super.onCreate of Manifest to replace theme
        setTheme(R.style.AppTheme);
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
    }
}
```

And we are done to make an awesome splash screen without any timer and any extra `Splash Screen Activity`.
Now make yours and enjoy.

Happy Coding :)

## REferences 
- [The (Complete) Android Splash Screen Guide](https://android.jlelse.eu/the-complete-android-splash-screen-guide-c7db82bce565) 
- [Android Splash Screen Implementation – Bad, Good and Best way](https://hellohasan.com/2018/07/24/android-splash-screen-bad-good-best-right-way/)
 