# Posmo Documentation
Documentation for the Posmo SDK

## Posmo SDK
### 1. Usage  
#### Android Manifest and Gradle Instructions

Add this in your root build.gradle file (not your module build.gradle file):
```
allprojects {
    repositories {
        maven { url "https://nexus.datamap.io/repository/maven-releases/" }
    }
}
```
Add this to your module's build.gradle file
```
implementation 'io.datamap:posmosdk:1.0.15'
```

#### iOS

### 2. Library Initialization with Client API Key
Dont forget to use your CLIENT_API_KEY
```
 new PosmoSDK.Builder()
                .withToken("CLIENT_API_KEY")
                .build();
```
### 3. Login / Registration / Forgot Password
**Login**
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

**Registration**
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

**Forgot password**
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

## Posmo TMS Library
TMS stands for Timeline, Map, Stats
### 1. Usage
### 2. Customization
### 3. View Components
* Timeline
* Map
* Calendar
* (Stats)
* (Edit)


    implementation 'io.datamap:posmosdk:1.0.15'
