# IHC EMR Project

---

## For Clients

The client section assumes that the user will be running the server on a Raspberry Pi Model 3+
and the application on an Android tablet. An APK file will be posted through the Releases section
on GitHub with the server IP address already pre-configured during the build process.

TODO

---

## For Developers

The developers section assumes that the user will be running the app on an Android tablet emulator,
and the server is hosted on a local MongoDB instance.

### Local Environment Setup

1. Make sure you have npm and jdk 1.8 (JAVA 8) installed. Run ```npm install -g react-native-cli``` in your terminal.
2. In terminal, go to your preferred directory for the project to be located at and run  ```git clone <repo url>```
3. In the directories `ihc/mobile/Ihc`, `ihc/server`, and `ihc/server/src run` ```npm install```
4. Install Mongodb.
5. (Recommended) Open the project through Android Studio.
6. Change the fetchUrl field within `mobile/ihc/config.json` to your computer's IP address. This is required to connect to the Express server.
7. Set environment variable `ANDROID_HOME` to the location of Android SDK on computer. Set environment variable `JAVA_HOME` to the location of jdk 1.8(JAVA 8) on computer.

### Running the Application

1. In Android Studio, press the AVD Manager button on the top right. Create a new virtual device, a 10 inch tablet and run the emulator.
2. Make sure MongoDB is running. [Link to Instructions](https://medium.com/swlh/get-up-and-running-with-mongodb-in-under-5-minutes-abc8770b1ef8)
3. In directory `ihc/server/`, run ```npm start``` to run the server.
4. In directory `ihc/mobile/IHC`, run ```react-native run-android``` to start the application on the emulator.

### Building an APK

1. If you don't have a signing key yet, generate a signing key. In `mobile/Ihc/android/app` run this command and follow the steps to generate the key:

   `keytool -genkey -v -keystore my-key.keystore -alias my-key -keyalg RSA -keysize 2048 -validity 10000`

2. In `mobile/Ihc/android/gradle.properties` add the password you used to generate your keystore from the last step to both the `MYAPP_RELEASE_STORE_PASSWORD` and `MYAPP_RELEASE_KEY_PASSWORD` entries. Edit the `MYAPP_RELEASE_KEY_ALIAS` entry if you chose a different alias when running the `keytool` command.

3. In `mobile/Ihc/config.json`, double check that `fetchUrl` is set to the IP address of the server like this: `"http://<IP Address>:8000"`(Make sure there's no "/" at the end!)

4. Now, to generate the APK, make sure you are in `mobile/Ihc/android`, then run:

   - `./gradlew assembleRelease` for Mac/Linux
   - `gradlew assembleRelease` for Windows

5. Done! You'll find the APK at `mobile/Ihc/android/app/build/outputs/apk/app-release.apk`!

### Installing the APK

1. Allow unknown apps by doing(these steps might be different depending on your device):

   1. Go into Settings.
   2. Tap Security (or Lock Screen and Security).
   3. Scroll down to the Device Administration section, and enable Unknown Sources.

2. Download the APK to the device(either using Google Drive or another method).
3. If a pop-up comes up saying "This type of file can harm your device," accept it.
4. Tap the downloaded APK file and tap `Install`.
5. The app should now show up in the app library as `ihc`.
