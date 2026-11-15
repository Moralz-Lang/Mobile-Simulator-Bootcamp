`TOOL`

**Android Debug Bridge (ADB)** is a development tool that facilitates communication between an Android device and a personal computer.

[How to Install ADB on Windows, macOS, and Linux(opens in new tab)](https://www.xda-developers.com/install-adb-windows-macos-linux/)

Note: You need debug usb enable in your emulator or device.

**How view devices?**

`adb devices`

![](https://1.bp.blogspot.com/-9LRRjROx5Dc/XbhSGAPA7UI/AAAAAAAAAOM/eAW8d9TstSgBPfLE_eXg7pyaLSTMbsLogCLcBGAsYHQ/s1600/de.png)

**How extract apk?**

For this you need have installed the application in your device and know package name

`adb shell pm path package_name`

This command print the path to the APK of the given  

![](https://1.bp.blogspot.com/-SZgJ7uGif1A/XbhSBXjgoRI/AAAAAAAAANQ/kAxiijq98IcL3ZCQFI1wPAgb8Z1-qddxgCLcBGAsYHQ/s1600/2019-10-28%2B15_07_17-Select%2BCommand%2BPrompt.png)

`adb pull <remote> [<locaDestination>]`  

This command pulls the file **remote** to **local**. If **local** isn’t specified, it will pull to the current folder.

![](https://1.bp.blogspot.com/-qv_YAwNZUu0/XbhSBRoPNnI/AAAAAAAAANU/Svu-OtoY61YCw87HQbk9gYZ5gCTJiT-7gCLcBGAsYHQ/s1600/2019-10-28%2B15_12_48-Select%2BCommand%2BPrompt.png)  

`Now,how a get source code?`

[jadx(opens in new tab)](https://github.com/skylot/jadx/releases/): The jadx suite allows you to simply load an APK and look at its Java source code. What’s happening under the hood is that jADX is decompiling the APK to smali and then converting the smali back to Java.

**Usage:**

`jadx -d [path-output-folder] [path-apk-or-dex-file]`

![](https://1.bp.blogspot.com/-c6lXRh1B01Y/XbhSBSFrFrI/AAAAAAAAANM/hWHM5_y1CUo_kJN9TWLHAWer5yMJpbd7wCLcBGAsYHQ/s1600/2.png)  

![](https://1.bp.blogspot.com/-u7fpX8PLn6w/XbhSB3i8wAI/AAAAAAAAANY/yktEGUW53g4oNyAUkKWcGAO9oicg_koUgCLcBGAsYHQ/s1600/3.png)  

[Dex2Jar(opens in new tab)](https://sourceforge.net/projects/dex2jar/): use dex2jar to convert an APK to a JAR file.

`d2j-dex2jar.sh or .bat /path/application.apk`

![](https://1.bp.blogspot.com/-0-UigTjn75k/XbhSByN_RaI/AAAAAAAAANc/bDtRMqg8zJEVBwLpNkjVg1SUW4deRbrXwCLcBGAsYHQ/s1600/4.png)  

Once you have the JAR file, simply open it with [JD-GUI(opens in new tab)](http://java-decompiler.github.io/) and you’ll see its Java code.

![](https://1.bp.blogspot.com/-rjJmAfX6PfA/XbhSCaWUPkI/AAAAAAAAANg/PH07DWI_Iz8z5t9MN_TqEbdHMYoBKmCbQCLcBGAsYHQ/s1600/5.png)  

  

[apktool(opens in new tab)](https://ibotpeaches.github.io/Apktool/install/): This tool get a source code in smali.

  

`apktool d file.apk`

  

![](https://1.bp.blogspot.com/-QcAGFBjR72Y/XbhSC5oLZgI/AAAAAAAAANk/PFtdPK3lfg0oO5XqzsfQ9Ne7IgyFJVSMgCLcBGAsYHQ/s1600/6.png)  

  

![](https://1.bp.blogspot.com/-gZ6rjaQp9io/XbhSDjr_l8I/AAAAAAAAANo/4t5U3rlxzP4Nx8M0K-KbvjE0M88xZAlAQCLcBGAsYHQ/s1600/7.png)  

  

**jadx-gui:**  UI version of jadx

`jadx\bin\jadx-gui`

![](https://1.bp.blogspot.com/-5tc4y5f0_pk/XbhSDmw11vI/AAAAAAAAANs/CkEsROS7l0Y3HKbwM65V3A3rJymmcr_YgCLcBGAsYHQ/s1600/8.png)

Q 3. What is the apk path of Black Hat Europe?

Ans. /data/app/com.swapcard.apps.android.blackhat=/base.apk

Solution: — Install Black hat Europe application in simulator

(If don’t want to sign in in playstore, we can download apk from below link)

[

## Download Black Hat Europe Apk file (12.94Mb) 4.18.0-1, com.swapcard.apps.android.blackhat.apk

### Download Black Hat Europe 4.18.0-1 APK file (12.94Mb) for Android (com.swapcard.apps.android.blackhat.apk), instant…

www.apk4now.com



](https://www.apk4now.com/apk/359900/black-hat-europe/download/372509?source=-----9298b632d82f---------------------------------------)

C:\platform-tools> .\adb install “C:\Users\Deepak Kushwah\Downloads\com.swapcard.apps.android.blackhat.apk”

Press enter or click to view image in full size

![](https://miro.medium.com/v2/resize:fit:700/1*b1yTUGzUCOUR7JeYGO3gPw.png)

Press enter or click to view image in full size

![](https://miro.medium.com/v2/resize:fit:700/1*fVJu9qPcGZiu_2voURymWA.png)

.\adb shell pm path com.swapcard.apps.android.blackhat

Q 4. Command for extract apk of Back Hat Europe?

## Get Deepak Kushwah’s stories in your inbox

Join Medium for free to get updates from this writer.

Subscribe

Remember me for faster sign in

Note: command and path

Ans. adb pull /data/app/com.swapcard.apps.android.blackhat=/base.apk

Press enter or click to view image in full size

![](https://miro.medium.com/v2/resize:fit:700/1*9ssSA5RKhjstXQUZelQdvg.png)