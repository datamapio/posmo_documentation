# Posmo Documentation
Documentation for the Posmo SDK

[JavaDoc Posmo SDK](https://sdk-docs.datamap.io/io/datamap/posmosdk/PosmoSDK.html)


## Posmo Android SDK
### 1. Usage  
#### Android Manifest and Gradle Instructions

Add this code snippet to your **root build.gradle** file.      
Note: This is not the same as your module build.gradle file.
```
allprojects {
    repositories {
        maven { url "https://nexus.datamap.io/repository/maven-releases/" }
    }
}
```
Add this code snippet to your **module's build.gradle** file
```
implementation 'io.datamap:posmosdk:1.0.27'
```


### 2. Library Initialization with the Client API Key
Dont forget to use your own CLIENT_API_KEY
```
 new PosmoSDK.Builder()
                .withToken("CLIENT_API_KEY")
                .build();
```
### 3. Login / Registration / Forgot Password
#### Login
```
PosmoSDK.login(context, "username", "password", new OnResultListener() {
            @Override
            public void onResultSuccess(APIResponse apiResponse) {
                Toast.makeText(getApplicationContext(), "Success", LENGTH_LONG ).show();
            }
            @Override
            public void onResultError(String s) {
                Toast.makeText(getApplicationContext(), "Error: "+s, LENGTH_LONG ).show();
            }
        });
```

#### Logout
```
boolean success=PosmoSDK.logout(context);
```

#### Registration
```
 PosmoSDK.register(context, "username", "password", new OnResultListener() {
            @Override
            public void onResultSuccess(APIResponse apiResponse) {
            }
            @Override
            public void onResultError(String s) {
            }
        });
```

#### Forgot password
```
  PosmoSDK.forgotPassword(context, "email", new OnForgotPassResultListener() {
            @Override
            public void onResultSuccess() {
            }

            @Override
            public void onError(String s) {
            }
        });
```
### 4. Places Search / Autocomplete Search 
**lon** (longitude) and **lat** (latitude) and can be null if the current location is unknown.
```
 PosmoSDK.placeSearch(context, "Bellinzona", lat, lon, new OnPlaceSearchResultListener() {
            @Override
            public void onResult(io.datamap.posmosdk.PlacesAPI.APIResponse apiResponse) {
                
            }

            @Override
            public void onResultError(String s) {

            }
        });
```

## Posmo TMS Library
TMS stands for Timeline, Map, Stats

![Webp net-resizeimage (1)](https://user-images.githubusercontent.com/11587927/54697494-f6ef4c00-4b2d-11e9-8aee-09e1c1d600b4.png)
![Webp net-resizeimage](https://user-images.githubusercontent.com/11587927/54697501-f787e280-4b2d-11e9-9dc1-0c1ec4b3723d.png)

### 1. Usage
#### Android Manifest and Gradle Instructions

Add this code snippet to your **root build.gradle** file.      
Note: This is not the same as your module build.gradle file.
```
allprojects {
    repositories {
        maven { url 'https://jitpack.io' }
        maven { url "https://nexus.datamap.io/repository/maven-releases/" }
    }
}
```
Add this code snippet to your **module's build.gradle** file
```
implementation 'io.datamap:posmotmsview:1.0.6'
```
#### Layout file
```
<RelativeLayout
        android:id="@+id/insideFrameContainer"
        android:layout_width="match_parent"
        android:layout_height="match_parent">

        <io.datamap.posmotmview.PosmoTMView
            android:id="@+id/posmoTMView"
            android:layout_width="match_parent"
            android:layout_height="match_parent"
            />
</RelativeLayout>
```

#### Inside Fragment or Activity
```
 @Override
    public void onViewCreated(@NonNull View view, @Nullable Bundle savedInstanceState) {
        super.onViewCreated(view, savedInstanceState);

        //Find view which is defined in layout
        PosmoTMView posmoTMView = view.findViewById(R.id.posmoTMView);

        //Listener for calendar toogle
        posmoTMView.setOnCalendarToogle(new OnCalendarToogle() {
            @Override
            public void calendarHidden() {
            }

            @Override
            public void calendarShow() {
            }
        });

        //Option for saving state of calendar
        posmoTMView.setSaveState(true);

        //Start foreground service
        PosmoSDK.startService( getContext());

        //Providing fragment manager
        posmoTMView.setFragmentManager(getFragmentManager(), R.id.frameLayout);

    }
```

#### Android manifest
Boot Receiver to automatically start the service after booting.
```
  <receiver android:name="io.datamap.posmosdk.services.BootReceiver">
            <intent-filter>
                <action android:name="android.intent.action.BOOT_COMPLETED"/>
            </intent-filter>
        </receiver>
```
Declaration of service.
```
        <service
            android:name="io.datamap.posmosdk.services.PosmoServiceV2"
            >
        </service>
```
### 2. Customization
### 3. View Components
* Timeline
* Map
* Calendar
* (Stats)
* (Edit)


    implementation 'io.datamap:posmosdk:1.0.15'
