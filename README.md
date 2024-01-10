# ADB tasks

 1. Display the connected device in the console.
 
 solution:

 ```
./adb devices

List of devices attached
emulator-5554	device
```

 2. Install the .apk file of the "todolist" application on the connected device from a computer via ADB
 
 solution:

 ```
./adb install /Users/ostalskyi/hw_ksendzov_courses/Android_Studio/TodoList.apk

Performing Streamed Install
Success
```
 3. Display the address of the "todolist" application on the connected device

 solution:
  - find out how the "todolist" application is registered in the Android system
 
 ```
./adb shell pm list packages | grep todolist

package:com.android.todolist
```
- find out the address of the "todolist" application on the connected device

```
./adb shell pm path com.android.todolist  

package:/data/app/~~B2XTwM4QjhemIS_KewTxqQ==/com.android.todolist-uA6bqVQHo_s8xJlzSF036g==/base.apk
 ```

4. Take a screenshot of the running "todolist" app and copy it to computer in one command.

solution:
```
./adb shell screencap /storage/emulated/0/Pictures/Screenshots/todolist_sreenshot.png && ./adb pull /storage/emulated/0/Pictures/Screenshots/todolist_sreenshot.png /Users/ostalskyi/Desktop/ScreenRec

/storage/emulated/0/Pictures/Screenshots/todol..., 0 skipped. 10.8 MB/s (72252 bytes in 0.006s)
```
- also you can take a screenrecord of the running "todolist" app and copy it to computer
```
 ./adb shell screenrecord --time-limit 30 /storage/emulated/0/Pictures/Screenshots/todolist_sreenrec.mp4 && ./adb pull /storage/emulated/0/Pictures/Screenshots/todolist_sreenrec.mp4 /Users/ostalskyi/Desktop/ScreenRec

/storage/emulated/0/Pictures/Screenshots/todol..., 0 skipped. 2.8 MB/s (746136 bytes in 0.256s)
```
 
5. Output "todolist" application logs to the console

 solution:
 ```
./adb logcat | grep com.android.todolist

09-25 13:26:18.502   487   528 V BackupManagerService: [UserID:0] restoreAtInstall pkg=com.android.todolist token=2 restoreSet=0
09-25 13:26:18.504   487   528 I AppsFilter: interaction: PackageSetting{70599a5 com.qrolic.reminderapp/10155} -> PackageSetting{cd0e17a com.android.todolist/10154} BLOCKED
09-25 13:26:18.560  1313  1313 I MediaProvider: Invalidating LocalCallingIdentity cache for package com.android.todolist. Reason: package android.intent.action.PACKAGE_ADDED ...
```
6. Copy "todolist" application logs to the computer.
 
 solution:
```
./adb logcat | grep com.android.todolist > todolist.log
```
7. Uninstall "todolist" application from the phone via ADB

   solution:
```
./adb uninstall com.android.todolist

Success
```
