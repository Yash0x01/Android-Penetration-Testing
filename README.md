# Android-Penetration-Testing-Guide

## Tools

```bash
1. Android Emulator
2. Jadx
3. Apk Tool
4. ADB Tools
5. Frida
6. Objection
7. MobSF
8. BurpSuite
9. rootAVD/Magisk
10. Drozer
```

## Commands

It lists all the packages (applications) installed on an Android device or emulator.

```bash
adb shell pm list packages
```

It is primarily used to find the file path of an installed app's APK on an Android device or emulator.

```bash
adb shell pm path <package-name>
```

The command is used to start an activity within an Android application directly from the command line. The adb shell am command utilizes the Android Activity Manager (AM) to perform actions on the Android system, and start specifically launching an activity.

```bash
adb shell am start <package-name/.activity-name>

Example: Androgoat Vulnerable Application
package name = "owasp.sat.agoat" and activity = "AccessControl1ViewActivity"

adb shell am start owasp.sat.agoat/.AccessControl1ViewActivity
```

It is used in Android development to copy files from an Android device to your computer.

```bash
adb pull <file-name>
```

It allows developers to copy files from their local machine to an Android device or an emulator.

```bash
adb push <file-name>
```

It is used to retrieve the CPU architecture of an Android device.

```bash
adb shell getprop ro.product.cpu.abi 
```

This command allows users to perform actions that require elevated permissions, such as accessing system directories, modifying system files, or executing commands that are typically restricted to the root user.

```bash
adb root
```

It is used to install an APK file onto an Android device from a computer.

```bash
adb install example.apk
```
This command is used to uninstall an APK file from an Android device or emulator.


```bash
adb uninstall <package-name>
```

It is used to display all running processes.

```bash
ps -A
```

This command is used to terminate a process by its process ID (PID).

```bash
kill <PID>
```

## SSL Pinning Bypass Methods

### Method 1: Using Objection

- Automate using objection.

```bash
objection patchapk --source example.apk
```

### Method 2: Using Frida Server and Frida Script

- Frida Server and Frida Script
- (Note: The Frida server must be located in `/data/local/tmp/`. Also, ensure to add the Burpsuite CA certificate in the tmp folder as `cert-der.crt`.)
- Now, provide execute permissions to the Frida server and run the server.
- Now, download the ssl bypass script from https://codeshare.frida.re/.
- After running the Frida server, execute the following command.

```bash
frida -U -f <package-name> -l <path-of-frida-script.js>
```

### Method 3: Using Objection and Frida Server

- Using Objection and Frida Server
- After running the Frida server, execute the following command.

```bash
objection --gadget <package-name> explore --startup-command "android sslpinning disable"
```

### Method 4: Manual Decompilation

1. Decompile the APK file using apktool.
2. Inject the Frida gadget.

## Root Detection Bypass Methods

### Method 1: Using Magisk and Zygisk

1. Install Magisk on your device.
2. Use the Zygisk module to hide root detection.

### Method 2: Using Frida Scripts

Download root detection bypass scripts from https://codeshare.frida.re/

