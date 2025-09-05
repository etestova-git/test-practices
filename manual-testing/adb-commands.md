# 🔹 Main ADB Commands for Manual Testing

## 📱 Device Management
- `adb devices`  
  List all connected devices/emulators.  
- `adb connect <ip:port>`  
  Connect to a device over Wi-Fi.  
- `adb reboot`  
  Restart the device.  
- `adb reboot recovery` | `adb reboot bootloader`  
  Reboot into recovery or bootloader mode.  

---

## 📂 App Management
- `adb install app.apk`  
  Install an APK on the device.  
- `adb install -r app.apk`  
  Reinstall (keep app data).  
- `adb uninstall com.package.name`  
  Uninstall app.  
- `adb shell pm clear com.package.name`  
  Clear app data (reset app to fresh install state).  
- `adb shell pm list packages`  
  List all installed packages.  

---

## 📜 Logs & Debugging
- `adb logcat`  
  View live system/app logs.  
- `adb logcat > log.txt`  
  Save logs to a file.  
- `adb logcat | find "com.package.name"`  
  Filter logs by package name.  
- `adb bugreport > bugreport.zip`  
  Generate full system bug report.  

---

## 🔄 App Control
- `adb shell am start -n com.package.name/.ActivityName`  
  Launch specific activity.  
- `adb shell am force-stop com.package.name`  
  Force stop an app.  
- `adb shell am start -a android.intent.action.VIEW -d <url>`  
  Open a deep link in the app.  

---

## 🌍 Network & Device State
- `adb shell svc wifi disable` | `adb shell svc wifi enable`  
  Toggle Wi-Fi.  
- `adb shell svc data disable` | `adb shell svc data enable`  
  Toggle mobile data.  
- `adb shell settings put global airplane_mode_on 1`  
  Enable airplane mode.  
- `adb shell settings put global airplane_mode_on 0`  
  Disable airplane mode.  
- `adb shell am broadcast -a android.intent.action.AIRPLANE_MODE`  
  Apply airplane mode change.  

---

## 🔔 Notifications & Permissions
- `adb shell dumpsys notification`  
  Show active notifications.  
- `adb shell pm grant com.package.name android.permission.CAMERA`  
  Grant permission.  
- `adb shell pm revoke com.package.name android.permission.CAMERA`  
  Revoke permission.  

---

## 📷 Screenshots & Screen Recording
- `adb exec-out screencap -p > screen.png`  
  Take screenshot.  
- `adb shell screenrecord /sdcard/test.mp4`  
  Record screen.  
- `adb pull /sdcard/test.mp4`  
  Copy recording to computer.  

---

## 🔋 Battery & Performance
- `adb shell dumpsys battery`  
  Show battery status.  
- `adb shell dumpsys meminfo com.package.name`  
  Show memory usage of app.  
- `adb shell top -n 1 | grep com.package.name`  
  Check CPU usage of app.  

---

# ✅ Tips for QA
- Always run `adb devices` first to check connectivity.  
- Use **logcat filters** to track crashes, ANRs, and app-specific logs.  
- Combine `adb` commands in scripts for repetitive test flows.  
