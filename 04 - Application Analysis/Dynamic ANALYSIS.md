`adb install apkfilename.apk`  

okay, now how intercept traffic of the application?  

Burp Suite: Is an integrated platform for performing security testing of web applications. Its various tools work seamlessly together to support the entire testing process, from initial mapping and analysis of an application’s attack surface, through to finding and exploiting security vulnerabilities.

[Configure the Burp Proxy listener(opens in new tab)](https://support.portswigger.net/customer/portal/articles/1841101-configuring-an-android-device-to-work-with-burp)

Installing trusted CA at the Android OS level (Root device/Emulator) for Android N+ as the following:

  

`openssl x509 -inform PEM -subject_hash -in BurpCA.pem | head -1`

`cat BurpCA.pem > 9a5ba580.0`

`openssl x509 -inform PEM -text -in BurpCA.pem -out /dev/null >> 9a5ba580.0`

`adb root`

`abd remount`

`adb push 9a5ba580.0 /system/etc/security/cacerts/`

`adb shell "chmod 644 /system/etc/security/cacerts/9a5ba580.0"`

`adb shell "reboot"`

---
[PID Cat(opens in new tab)](https://github.com/JakeWharton/pidcat)

Tool for shows log entries for a specific application package when debug=true is enable in the app.

![](https://github.com/JakeWharton/pidcat/raw/master/screen.png)  
[Drozer(opens in new tab)](https://github.com/FSecureLABS/drozer)

drozer helps to provide confidence that Android apps and devices being developed by, or deployed across, your organisation do not pose an unacceptable level of risk. By allowing you to interact with the Dalvik VM, other apps’ IPC endpoints and the underlying OS.

drozer provides tools to help you use and share public exploits for Android. For remote exploits, it can generate shellcode to help you to deploy the drozer Agent as a remote administrator tool, with maximum leverage on the device.

drozer is a comprehensive security audit and attack framework for Android.  

Basic example, Abusing unprotected activities:

The requirement for this is you have install drozer in your computer and drozer agent in your emulator or devices. Click in the title, for the tutorial of how install...

Commands:

`adb forward tcp:31415 tcp:31415`

`drozer console connect`  

Now download and install [apk(opens in new tab)](https://github.com/as0ler/Android-Examples/raw/master/sieve.apk) for this example

![](https://1.bp.blogspot.com/-gsDR47x_3dM/XbmxvRPEWuI/AAAAAAAAATU/alGUO8pabwQqOxMH4f15JsjpRSqu5YXIACLcBGAsYHQ/s1600/dro1.png)  

Retrieving package information:

`run app.package.list -> see all the packages installed`  

![](https://1.bp.blogspot.com/-hZEQXTuaEsk/XbmxuztqE-I/AAAAAAAAATM/UHQb8TeBs0cceAuuEufxW67X5M6Nw372ACLcBGAsYHQ/s1600/dro2.png)  

`run app.package.info -a -> view package information.`

![](https://1.bp.blogspot.com/-cH4fQR_g_xI/Xbmxu1LTiGI/AAAAAAAAATI/PvGJ7n3OHs4W9dTkHhWqkEsjpX1d6gk-wCLcBGAsYHQ/s1600/dro3.png)  

Identifying the attack surface -> activities unprotected and more....  

`run app.package.attacksurface package_name`  

![](https://1.bp.blogspot.com/-OdHlf3BwLdw/XbmxvaddpnI/AAAAAAAAATQ/fOzZhtJxUEwFvFo-ztRvNO16AFdM_jgIACLcBGAsYHQ/s1600/dro4.png)  

view what activities can be exploited.  

`run app.activity.info -f package_name`  

![](https://1.bp.blogspot.com/-ISiTx7LIdsA/XbmxvoN4j3I/AAAAAAAAATY/2693VgbHP4En7MN6w5KrvtSoNsL5NF1hgCLcBGAsYHQ/s1600/dro5.png)  

start activities unprotected !

`run app.activity.start --component package name component_name`

![](https://1.bp.blogspot.com/-lYaJXJeIUVo/XbmxwID1-2I/AAAAAAAAATc/vKPPlYFLq84n74PxuUP4USCKA1UvUYYVACLcBGAsYHQ/s1600/dro6.png)

---

## **Inspeckage - Android Package Inspector**  

My favorite tool, [Inspeckage] is a tool developed to offer dynamic analysis of Android applications. By applying hooks to functions of the Android API, Inspeckage will help you understand what an Android application is doing at runtime. Inspeckage will let you interact with some elements of the app, such as activities and providers (even unexported ones), and apply some settings on Android.

Since dynamic analysis of Android applications (usually through hooks) is a core part of several mobile application security tests, the need of a tool that can help us do said tests is real. Even though there are other tools that promise to help you do that, I’ve run across some limitations when testing them:

- Lack of interaction with the user doing the tests;
- Only work in emulators;
- Plenty of time to update the tool after an Android update;
- Very poor output;
- Very costly setup.

**Android Package Inspector Features**

With Inspeckage, we can get a good amount of information about the application’s behavior:

**Information gathering**

- Requested Permissions;
- App Permissions;
- Shared Libraries;
- Exported and Non-exported Activities, Content Providers,Broadcast Receivers and Services;
- Check if the app is debuggable or not;
- Version, UID and GIDs;
- etc.

**Hooks**

With the hooks, we can see what the application is doing in real time:

- Shared Preferences (log and file);
- Serialization;
- Crypto;
- Hashes;
- SQLite;
- HTTP (an HTTP proxy tool is still the best alternative);
- File System;
- Miscellaneous (Clipboard, URL.Parse());
- WebView;
- IPC.

How to use:
![[Inspeckage Tutorial.mp4]]

---


**Insecure Data Storage**  

We've totally interacted with our app now it's time to see the files created locally.

Many developers assume that storing data on client-side will restrict other users from having access to this data. Interestingly, most of the top mobile application security breaches have been caused by insecure or unnecessary client-side data storage. File systems on devices are no longer a sandboxed environment and rooting or jailbreaking usually circumvents any protections.

One needs to understand what different types of data are there and how are these stored insecurely.

Data - Usernames, Authentication tokens or passwords, Cookies, Location data, Stored application logs or Debug information, Cached application messages or transaction history, UDID or EMEI, Personal Information (DoB, Address, Social, etc), Device Name, Network Connection Name, private API calls for high user roles, Credit Card Data or Account Data, etc.

All apps (root or not) have a default data directory, which is /data/data/<package_name>. By default, the apps databases, settings, and all other data go here.  

- **databases**/: here go the app's databases
- **lib**/: libraries and helpers for the app
- **files**/: other related files
- **shared_prefs**/: preferences and settings
- **cache**/: well, caches

For interact with device or emulator 

`adb shell`

Sqlite database file

Once you are able to access the SQLite database file on an emulator, rooted device or via adb shell / run as [package name], there are a few options to inspect the schema and your SQLite database on device.

**[Inspect SQLite db via a GUI tool(opens in new tab)](https://sqlitebrowser.org/dl/)**

Pull the file from device first, then use a GUI software to look the schema and content. I use SQLite browser which allows you to see the database schema, table content, as well as executing some simple SQL scripts.

`adb pull /data/data/package-name/databases/sqlitedatabse`

**Inspect SQLite db via sqlite3 command line tool**

For me the easier option is to use sqlite3 command line tool to inspect the database from adb shell.

`cd data/data/package-name/databases/`

`sqlite3 db-name`

`.tables`

`.schema table-name`

Example in the real life:

![](https://1.bp.blogspot.com/-5dkR-xzaA7o/Xbm_8j-FJfI/AAAAAAAAAUE/7e7UeC5OdeYzhi7egq1pLKgr9mT_Zm8ygCLcBGAsYHQ/s1600/shared1.png)

Shared Preferences Files

The SharedPreferences API is commonly used to permanently save small collections of key-value pairs. Data stored in a SharedPreferences object is written to a plain-text XML file. The SharedPreferences object can be declared world-readable (accessible to all apps) or private. Misuse of the SharedPreferences API can often lead to exposure of sensitive data. Consider the following example:

SharedPreferences sharedPref = getSharedPreferences("key", MODE_WORLD_READABLE);
SharedPreferences.Editor editor = sharedPref.edit();
editor.putString("username", "administrator");
editor.putString("password", "supersecret");
editor.commit();

  

Once the activity has been called, the file key.xml will be created with the provided data. This code violates several best practices.

  

<?xml version='1.0' encoding='utf-8' standalone='yes' ?>
<map>
  <string name="username">administrator</string>
  <string name="password">supersecret</string>
</map>

  

Example in the real life: 

  

![](https://1.bp.blogspot.com/-ft-7-Cc64BU/XbrxkMtrp6I/AAAAAAAAAUk/zUMZAkEqkbsySiWG70inJcU4zor5RLfggCLcBGAsYHQ/s1600/shared.png)

Stopped On task 9 (Come back to later!)


---
**Hooking applications**:

Techniques used to alter the behaviour of applications. 

**Frida**

In short, it is a dynamic instrumentation framework, which enables function hooking and allows to provide a definition to it during runtime. Basically, it injects JavaScript code into a process. Suppose, there is a function called “foo” in a program with a specific body/implementation. Using “Frida”, one can change the body/implementation of the “foo” function during runtime. “Frida” supports a variety of platforms like Windows, macOS, GNU/Linux, iOS, Android, and QNX. More information on “Frida” can be found [here(opens in new tab)](https://www.frida.re/docs/home/).

for install 

`pip install frida-tools`  

Now check version and download the server, in my case is 12.6.8

`frida --version`

unzip file and push the server in the local system /data/local/tmp

`adb push /path/serverfrida /data/local/tmp`

Permissions

`adb shell chmod 777 /data/local/tmp/frida-server`  

run frida server

adb shell /data/local/tmp/frida-servername&  

now execute in your command line **frida-ps -U**

# Bypass SSL pinning tutorial BELOW:

1. Setup and Installation_
2. Frida Server Setup
3. Setup BurpSuite
4. Pushing the proxy’s CA Certificate:
5. Script injection to bypass SSL pinning
6. All stuff in a nutshell
7. Troubleshooting

## 1. Introduction to Frida _and SSL pinning_

Frida framework is the last stop for SSL pinning bypass.

As per frida [**website**](https://www.frida.re/docs/home/):

> “ It’s [Greasemonkey](https://addons.mozilla.org/en-US/firefox/addon/greasemonkey/) for native apps, or, put in more technical terms, it’s a dynamic code instrumentation toolkit. It lets you inject snippets of JavaScript or your own library into native apps on Windows, macOS, GNU/Linux, iOS, Android, and QNX. Frida also provides you with some simple tools built on top of the Frida API. These can be used as-is, tweaked to your needs, or serve as examples of how to use the API.”

Press enter or click to view image in full size

![](https://miro.medium.com/v2/resize:fit:700/1*42qQYWNSdimNUEW4okfdgw.jpeg)

> Certificate pinning is hardcoding certificate trusted by the remote server within application itself so that it will ignore devices certificate store and will trust on his own hardcoded certificate which further application will use to communicate with remote server “securely”.

SSL pinning bypass is major step needs to be done when we even start the dynamic analysis of HTTP requests for most of the mobile application nowadays as organizations are more concern about data privacy and secure transfer of data over the network from threads like Man-in-The-Middle (MiTM) attacks.

Frida is a framework that injects scripts to native apps to manipulate application’s logic in runtime which is more dynamic approch for pentesting mobile applications.

## 2. Requirements

Let's gather and fulfill all requirements before performing our magic trick. This setup takes some time for the first time as the requirement list is quite long. Once we are done with all setup, from next time it will be a piece of cake. If you stuck at any step there is _“_**_Troubleshooting_**_”_ section at the end of the blog. Saving all downloaded stuff in one folder is recommended.

**I. Rooted device/emulator:**

We will be needing a rooted device or emulator as we need to inject script into the root directory of the device. I’m using genymotion for this one. Genymotion is easy to set-up and use and can download it from below.

> [**_https://www.genymotion.com/fun-zone/_**](https://www.genymotion.com/fun-zone/)

Once we are done installing genymotion, we need to install an android device. Android 7+ version will be good to go. I will be using ‘_Google pixel XL’_ device with the following configuration.

![](https://miro.medium.com/v2/resize:fit:620/1*_WFyTAo9-G7Zcq_XDGGoHg.jpeg)

**II. Python frida packages installation:**

Install Python for windows from here.

> [**_https://www.python.org/downloads/windows/_**](https://www.python.org/downloads/windows/)

We need to install some python packages for frida server. For this enter following command in terminal:

python -m pip install Frida  
python -m pip install objection  
python -m pip install frida-toolsorpip install Frida  
pip install objection  
pip install frida-tools

**III. Platform-tools (adb):**

Download platform-tools for windows from the following the link:

> [**_https://dl.google.com/android/repository/platform-tools-latest-windows.zip_**](https://dl.google.com/android/repository/platform-tools-latest-windows.zip)

![](https://miro.medium.com/v2/resize:fit:322/1*VEwoPGbBF-YTJqo3WjE0bA.png)

**IV. Download injection script:**

We need to download injection script from below which we will push into the device for injecting into target application.

> [**_https://codeshare.frida.re/@pcipolloni/universal-android-ssl-pinning-bypass-with-frida/_**](https://codeshare.frida.re/@pcipolloni/universal-android-ssl-pinning-bypass-with-frida/)

or you can save this code as **fridascript.js** in same folder as adb.

/*   
   Android SSL Re-pinning frida script v0.2 030417-pier$ adb push burpca-cert-der.crt /data/local/tmp/cert-der.crt  
   $ frida -U -f it.app.mobile -l frida-android-repinning.js --no-pause[https://techblog.mediaservice.net/2017/07/universal-android-ssl-pinning-bypass-with-frida/](https://techblog.mediaservice.net/2017/07/universal-android-ssl-pinning-bypass-with-frida/)  
     
   UPDATE 20191605: Fixed undeclared var. Thanks to [@oleavr](http://twitter.com/oleavr) and [@ehsanpc9999](http://twitter.com/ehsanpc9999) !  
*/setTimeout(function(){  
    Java.perform(function (){  
     console.log("");  
     console.log("[.] Cert Pinning Bypass/Re-Pinning");var CertificateFactory = Java.use("java.security.cert.CertificateFactory");  
     var FileInputStream = Java.use("java.io.FileInputStream");  
     var BufferedInputStream = Java.use("java.io.BufferedInputStream");  
     var X509Certificate = Java.use("java.security.cert.X509Certificate");  
     var KeyStore = Java.use("java.security.KeyStore");  
     var TrustManagerFactory = Java.use("javax.net.ssl.TrustManagerFactory");  
     var SSLContext = Java.use("javax.net.ssl.SSLContext");// Load CAs from an InputStream  
     console.log("[+] Loading our CA...")  
     var cf = CertificateFactory.getInstance("X.509");  
       
     try {  
      var fileInputStream = FileInputStream.$new("/data/local/tmp/cert-der.crt");  
     }  
     catch(err) {  
      console.log("[o] " + err);  
     }  
       
     var bufferedInputStream = BufferedInputStream.$new(fileInputStream);  
    var ca = cf.generateCertificate(bufferedInputStream);  
     bufferedInputStream.close();var certInfo = Java.cast(ca, X509Certificate);  
     console.log("[o] Our CA Info: " + certInfo.getSubjectDN());// Create a KeyStore containing our trusted CAs  
     console.log("[+] Creating a KeyStore for our CA...");  
     var keyStoreType = KeyStore.getDefaultType();  
     var keyStore = KeyStore.getInstance(keyStoreType);  
     keyStore.load(null, null);  
     keyStore.setCertificateEntry("ca", ca);  
       
     // Create a TrustManager that trusts the CAs in our KeyStore  
     console.log("[+] Creating a TrustManager that trusts the CA in our KeyStore...");  
     var tmfAlgorithm = TrustManagerFactory.getDefaultAlgorithm();  
     var tmf = TrustManagerFactory.getInstance(tmfAlgorithm);  
     tmf.init(keyStore);  
     console.log("[+] Our TrustManager is ready...");console.log("[+] Hijacking SSLContext methods now...")  
     console.log("[-] Waiting for the app to invoke SSLContext.init()...")SSLContext.init.overload("[Ljavax.net.ssl.KeyManager;", "[Ljavax.net.ssl.TrustManager;", "java.security.SecureRandom").implementation = function(a,b,c) {  
      console.log("[o] App invoked javax.net.ssl.SSLContext.init...");  
      SSLContext.init.overload("[Ljavax.net.ssl.KeyManager;", "[Ljavax.net.ssl.TrustManager;", "java.security.SecureRandom").call(this, a, tmf.getTrustManagers(), c);  
      console.log("[+] SSLContext initialized with our custom TrustManager!");  
     }  
    });  
},0);

## 3. Setup and installation:

**I. Connect device to adb:**

We need to connect our device to adb to run commands on device. But first goto _settings >> Developer options_ and enable debugging mode in device so that adb can communicate with the device.

Goto the folder where platform tools have been extracted and run the following command to connect the device to adb

//adb connect <ip of device:port>  
adb connect 192.168.1.190:5555

Click on ‘Allow’ if pop-up appears in device.

Press enter or click to view image in full size

![](https://miro.medium.com/v2/resize:fit:700/1*qAQcWV36trLxPMVR1jf3Wg.png)

To check if device is connected to adb:

adb devices

You should see ip of your device along with device name.

**II.Download frida server for supported android device’s arch version:**  
We need to download the frida server package for our android device according to our device’s arch version.

> [https://github.com/frida/frida/releases/](https://github.com/frida/frida/releases/)

To find out the arch version of the device, run following command.

==adb shell getprop ro.product.cpu.abi==

To cut short download following if device configuration is the same as mentioned above:

> frida-server-12.4.7-android-x86.xz  
> frida-server-12.4.7-android-x86_64.xz

**IV. Install the target application in the device.**

Install your application who’s SSL pinning has to be bypassed in our device. Open the application and keep it running in the background.

## 4. Frida Server Setup:

We need to run frida server into device before injection our script. Follow the steps below:

## Get Vedant’s stories in your inbox

Join Medium for free to get updates from this writer.

Subscribe

Remember me for faster sign in

**I. Push frida-server into device:**

Now we need to push our frida-server file into device. Extract and Copy “_frida-server-12.4.7-android-x86”_ file in adb folder rename file as “frida-server”. After this, run following command.

//adb push <path_of_frida_server_folder><space></data/local/tmp>adb push C:\ADB\frida-server /data/local/tmp

**II. Give permissions to frida-server:**

adb shell chmod 777 /data/local/tmp/frida-server

## **5. Setup BurpSuite’s:**

Follow this awesome guide to set proxy in burp for android device:

> [**https://support.portswigger.net/customer/portal/articles/1841101-configuring-an-android-device-to-work-with-burp**](https://support.portswigger.net/customer/portal/articles/1841101-configuring-an-android-device-to-work-with-burp)

## 6. Pushing the proxy’s CA Certificate:

In order to be able to [intercept the traffic](https://guidedhacking.com/register/), frida needs to have access to our Burpsuite’s CA certificate. We will push the same certificate downloaded in step 5. in BurpSuite Setup.

Push the certificate into the device and into the same location as the frida-server, name it _cert-der.crt_ (as this name and path has been already mentioned in fridascript.js to avoid any issues)

// adb push <path to cacert.der> /data/local/tmp/cert-der.crt  
adb push cacert.der /data/local/tmp/cert-der.crt

## **7. Script injection to bypass SSL pinning:**

Now its time for real magic. we will inject **‘fridascript.js’** into the target application.

**I. Push fridascript.js into device:**

Copy fridascript.js into adb folder and run following command to push fridascript.js into device.

//adb push <path_to_fridascript.js_folder> /data/local/tmp  
adb push C:\ADB\fridascript.js /data/local/tmp

**II. Check and run frida server in device**

adb shell /data/local/tmp/frida-server &

This will run frida-server into device. Maybe you will not get any output of this command in terminal.

**III. List all running processes on device:**

Now, we need to find out id of our target application. We will list all running services on devices including your application process.

Open new terminal and type following command.

frida-ps -U

**IV. Locate your application’s package name.**

![](https://miro.medium.com/v2/resize:fit:494/1*kFQ8zBh9TT3jjqMUyN4KqQ.png)

**V. Hook fridascript.js into target application:**

Finally, we will hook fridascript.js into the native application with the following command:

//frida -U -f <your_application_package_name> -l <path_to_fridascript.js_on_your_computer> --no-pausfrida -U -f com.twitter.android -l D:\frida\fridascript.js --no-paus

Press enter or click to view image in full size

![](https://miro.medium.com/v2/resize:fit:700/1*twPxbDXLD64sYfXplq1q5g.png)

**VI. Bypassed!!**

Once all things go smooth, all traffic of the target app will get intercepted into BurpSuite. We need to keep frida server on as long as we are intercepting traffic into BurpSuite.

Press enter or click to view image in full size

![](https://miro.medium.com/v2/resize:fit:700/1*jpMMcQedWy8Y4N4awj_-0w.png)

## 8. All stuff in a nutshell:

**1. Download and install the device on genymotion  
2. Install frida and objection tools**

**python -m pip install Frida  
python -m pip install frida-tools  
python -m pip install objection****or****pip install Frida  
pip install frida-tools  
pip install objection**

**3. Download adb platform tools  
4. Download frida injection script  
5. Connect device to adb**

**//adb connect <ip of device:port>**

**6.Download frida server for supported android device’s arch version  
7. To find out arch version of device**

**adb shell getprop ro.product.cpu.abi**

**8. Install the target application in the device.  
9. Push frida-server into device:**

**//adb push <path of frida-server folder><space></data/local/tmp>**

**10. Give permissions to frida-server:**

**adb shell chmod 777 /data/local/tmp/frida-server**

**11. Setup burpsuite  
12. Pushing the proxy’s CA Certificate**

**// adb push <path to cacert.der> /data/local/tmp/cert-der.crt**

**13. Push fridascript.js into device:**

**//adb push <path to fridascript.js folder> /data/local/tmp**

**14. Check and run frida server in device**

**adb shell /data/local/tmp/frida-server &**

**15. List all running processes on device:**

**frida-ps -U**

**16.Locate your application’s package name  
17. Hook fridascript.js into target application**

**//frida -U -f <your_application_package_name> -l <path_to_fridascript.js_on_your_computer> --no-paus**

**18. Intercept traffic in BurpSuite.**

## 9. Troubleshooting:

**1. ADB Deamon failed to connect**

If you are getting error like this:

adb devices  
adb server is out of date. killing...  
cannot bind 'tcp:5037'  
ADB server didn't ACK  
*failed to start daemon*  
error:

i. Open environment System properties>>Advanced>>Environment Variables  
ii. Click on path and delete entry of C:/Android or path where adb tools are pointed  
iii. Copy all platform tools into genymotion>>tools folder  
iv. Create new path and add path of genymotion>>tools folder.

**2. frida/ pip is not recognized as an internal or external command**  
i. Open environment System properties>>Advanced>>Environment Variables  
ii. Create new path and add path of Python>>script folder

**3. Arm translation error while installing application into device.**

i. Download arm translation file from here  
[_https://androidfilehost.com/?fid=23252070760974384_](https://androidfilehost.com/?fid=23252070760974384)  
ii. Drag and drop file into device emulator or flash this file from recovery if you are using physical device  
iii. Restart device and you will be able to drag and drop install target application

**4. Failed to spawn: the ‘argv’ option is not supported when spawning Android apps**

Check your fridascript.js path on your computer. Path maybe incorrect. You have to give the absolute path of fridascript.js file. [Absolute path?](https://www.computerhope.com/issues/ch001708.htm)

**5. Started frida server but not able to list services**

Disconnect and re-connect wifi in device.

![](https://miro.medium.com/v2/resize:fit:600/1*K2wHwYDnwVqrHzSyUhBf5w.jpeg)

More hooks :v is your mision :33