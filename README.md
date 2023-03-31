# Build Release app for Android & iOS :—

## Android

## Step 1 :-  Add Your App Icon

  —> Get AppIcon in for all Suggested Size<br>
  —> Then use flutter_launcher_icons, so that we can easily changed the icon, add these package in “dev_dependencies”<br>
  —> Create a Assets folder in root directory, inside assets create one more folder name as icons and all your icons inside that folder<br>
  —> add flutter_icons inside pubsec.yaml file similar to dev_dependencies<br>
  ```
  eg:— flutter_icons:
		android: “launcher_icon”
		iOS: true
		image_path: “your_image_path”
  ```
—> then run “flutter pub get” and then run these command “flutter pub run flutter_launcher_icons:main”

## Step 2 :-  Add App name
—> Go to android\app\src\main\AndroidManifest.xml and change the android label,

### NOTE :— We need Keystore to publish app on play store 

## Step 3 :- Create  a Keystore
  —> Run the following command to create a Keystore.       
 For Windows :    
```
keytool -genkey -v -keystore c:\Users\USER_NAME\key.jks -storetype JKS -keyalg RSA -keysize 2048 -validity 10000 -alias key
```
For Mac & linux :
```
keytool -genkey -v -keystore ~/key.jks -keyalg RSA -keysize 2048 -validity 10000 -alias key
```  

—> If already have one Keystore you can also use that. This command will make a key.jks file inside the home directory.

## Step 4 :- Create a Keystore reference inside your app
  —> Create a file inside <app dir>/android/key.properties that contains a reference to your Keystore:  
```
			storePassword=testpassword
			keyPassword=testpassword
			keyAlias=testkey
			storeFile=D:/keystore.jks  //your_home_directory
```
## Step 5 :- Signing in Gradle
  —> add these content in app/build.gradle.  below apply plugins section 
```
      def keystoreProperties = new Properties()
			def keystorePropertiesFile = rootProject.file('key.properties')
			if (keystorePropertiesFile.exists()) {
					    keystoreProperties.load(new FileInputStream(keystorePropertiesFile))
			}
```
—> add signingConfigs and buildTypes
```
			 signingConfigs {
        release {
            keyAlias keystoreProperties['keyAlias']
            keyPassword keystoreProperties['keyPassword']
            storeFile keystoreProperties['storeFile'] ? file(keystoreProperties['storeFile']) : null
            storePassword keystoreProperties['storePassword']
        }
    }
    buildTypes {
        release {
            signingConfig signingConfigs.release
        }
    }
```
## Step 6 :- Build an release apk to upload on play store 
—> flutter build apk 

## Step7 :- Go on Google Play console  follow the steps and you are ready to publish your app
