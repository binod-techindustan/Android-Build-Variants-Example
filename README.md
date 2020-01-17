Android Build Type Example
===================================

Creating Build Type
--------------
In app level build.gradle file inside android you can create custom build types as per development process :
<br/>
```
   buildTypes {
        release {
            minifyEnabled false
            proguardFiles getDefaultProguardFile('proguard-android-optimize.txt'), 'proguard-rules.pro'
        }
        debug {
            debuggable true
            signingConfig signingConfigs.debug
        }
        staging {
            debuggable = true
            signingConfig signingConfigs.debug
        }
        
      }
 ```

Creating resource variable
--------------
Inside build type you can create you own variable and it can be use in the resource files like Strings.xml file
<br/>
```
      staging {
            resValue 'string', 'APP_NAME', '"AppName-Stage"'
      }
 ```
 The resource file define in build type can be access from resoure file for example from strings.xml:
 <br/>
 ```
      <resources>
           <string name="app_name">@string/APP_NAME</string>
      </resources>
 
 ```

Creating BuildConfig variable
--------------
You can create your own varialble for different build types. For example you can set your `BASE_URL` value for build types and access from your code.
<br>
```
    staging {
            buildConfigField "String", "BASE_URL", '"http://api.dev.domain.com/"'
        }

```
You can access the variable from code like this:

```
    String baseUrl=BuildConfig.BASE_URL;
    
```

Creating different package name/applicationId for build types
--------------

You can append a suffix to application package name from buildTypes:

```
  buildTypes {
    staging {
            applicationIdSuffix ".stage"
        }
  }       
```
Changing output apk name 
--------------
You can change the output apk name for every build type from build.gradle file like below:
<br/>

```
        android {
          applicationVariants.all { variant ->
            variant.outputs.all {
                //output file name has limit so you can give a short name
                //you can get app name from config itself using variable ${applicationName}
                outputFileName = "AppName-${variant.name}.apk"
            }
          }
         }
```
