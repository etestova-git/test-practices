
# 📱 Mobile Testing Guide

This page provides an overview of best practices for mobile app testing, 
including device selection, 
the role of emulators and simulators, 
core testing areas, 
and using Charles Proxy.

---

## 🔍 1. How to Choose Mobile Devices

### ✅ Key Criteria:
- **OS Versions:** Test across different major versions of Android and iOS (e.g., iOS 17, Android 14, etc.)
- **Device Models:** Prioritize popular and widely used devices (check market data)
- **Screen Sizes & Resolutions:** Include both small and large screen sizes to test responsive behavior
- **Hardware Capabilities:** Devices with different RAM, CPU, and GPU capabilities
- **Manufacturers & Brands:** Samsung, Google Pixel, Xiaomi, OnePlus, iPhone (multiple generations)
- **Network Types:** Test over WiFi, 3G, 4G, 5G to simulate real usage

### 📱 Compatibility Testing
- **Device Coverage:** Define a "device matrix" in collaboration with the Product Manager based on analytics. Include top devices like iPhones, Samsung Galaxy, and Google Pixel with OS versions such as iOS 15–17 and Android 12–14.
- **Screen Size & Resolution:** Ensure no layout issues on small and large screens.
- **Execution Strategy:** Combine physical devices with cloud testing farms (e.g., Sauce Labs, BrowserStack) for broader coverage.

---
- Cloud tools of real devices **Firebase Test Lab**, **BrowserStack**, **Sauce Labs**.
- Maintain a **device matrix** for the product or a fiture.
---

## 🧪 2. Emulators vs. Simulators

### 💻 Emulators (Android)
- Mimic both software and hardware of real Android devices
- Provided by Android Studio (AVD Manager)
- Good for functional and UI testing
- Slower than real devices

### 📱 Simulators (iOS)
- Simulate the iOS environment (software only)
- Provided by Xcode
- Cannot test hardware-specific features (e.g., camera, GPS)

### ⚠️ Limitations:
- **No real hardware behavior** (e.g., CPU throttling, battery drain)
- **No realistic performance data**
- **Limited support for gesture, touch, and physical sensors**

### ✅ Use Real Devices For:
- Final verification
- Performance and battery testing
- Hardware-specific feature testing

---

## 🧩 3. What to Test in Mobile Apps

### ✅ 1. Functional Testing
- Ensure the app behaves as expected.
- Navigation between screens
- Input field validation
- Button actions and links
- Business logic (e.g., calculations, workflows)
- API responses and error handling
- File uploads/downloads
- Push notifications behavior

### ✅ 2. UI/UX Testing

- Verify visual consistency and usability.
- Layouts on different screen sizes/resolutions
- Fonts, colors, icons, spacing
- Touch responsiveness (tap, swipe, pinch, drag)
- Accessibility (labels, ARIA roles, screen reader compatibility)
- Orientation changes (portrait ↔ landscape)

### ✅ 3. Cross-Platform Testing

- Test across different OS and device types.
- iOS vs. Android
- Phones vs. tablets
- Different OS versions (e.g., Android 12, iOS 17)
- Device-specific behaviors (camera, sensors, back button)

### ✅ 4. Performance Testing

- Check app speed and resource usage.
- App launch time
- Memory and battery consumption
- Scrolling smoothness and frame rates
- Response time for user actions and API calls
- Handling large data sets or images

### ✅ 5. Network Testing

- Ensure proper behavior under different network conditions.
- 3G, 4G, 5G, Wi-Fi, airplane mode
- Handling slow or lost connections
- Retry logic for failed requests
- Offline mode support

### ✅ 6. Security Testing

- Protect user data and prevent vulnerabilities.
- Secure login/authentication (e.g., OAuth, biometrics)
- Data encryption (at rest and in transit)
- No sensitive data stored in logs or cache
- Certificate pinning, HTTPS enforcement
- In-app permissions handling

### ✅ 7. Localization Testing

- Verify language and region-specific content.
- Translations of all UI elements
- Number/date/time/currency formats
- Text expansion in different languages (e.g., German vs. English)

### ✅ 8. Installation and Upgrade Testing

- Ensure app setup and updates work smoothly.
- First-time install
- Update from older versions
- Clean uninstall and reinstall
- Handling corrupted installation

### ✅ 9. Push Notification Testing

- Check messaging behavior.
- Receiving and tapping notifications
- Foreground, background, and killed app states
- Action buttons and deep linking
- Opt-in/opt-out handling

### ✅ 10. Crash and Recovery Testing

- Ensure app stability and error recovery.
- App doesn’t crash on invalid inputs
- Recover gracefully from unexpected behavior
- Logs collected for debugging
- ANR (Application Not Responding) scenarios

### 📝 Optional: Additional Areas

- Battery drain in long use
- App store compliance (Apple, Google)
- Analytics and tracking validation
- Third-party integrations (payment gateways, social login)
- Accessibility compliance (for WCAG standards)
  
### 🤖 4. Automation Strategy
- **Automation Candidates:** Automate key user flows (login, main features) for regression coverage
- **Tooling Choices:**
  - **Appium:** Cross-platform automation for iOS and Android
  - **XCUITest:** For iOS-native deep testing
  - **Espresso:** For fast Android testing with native integration

---

## 🔍 4. Using Charles Proxy for Mobile App Testing

### 🛠 Setup Steps:
1. **Install Charles Proxy** on your desktop: [https://www.charlesproxy.com/](https://www.charlesproxy.com/)
2. Connect your mobile device and desktop to the **same WiFi network**
3. On desktop: Go to `Proxy → Proxy Settings` and note the port (default: 8888)
4. On mobile:
   - Go to WiFi settings → Modify network → Set manual proxy
   - IP address: Your desktop IP
   - Port: 8888
5. Trust Charles SSL certificate:
   - On desktop: `Help → SSL Proxying → Install Charles Root Certificate`
   - On mobile: Open `[http://charlesproxy.com/getssl](http://chls.pro/ssl)` in browser and install the certificate (needed for HTTPS)

### 🔍 What You Can Do:

#### 1. Viewing and Inspecting Traffic
- See every API call the app makes, including headers, payloads, status codes, and timings
- **Verify API Calls:** Confirm correct endpoints and parameters
- **Debug UI Issues:** Reveal real backend error messages
- **Security Check:** Ensure sensitive data is sent securely and no secrets are leaked

#### 2. Network Throttling
- Simulate poor network conditions: slow 3G, flaky 4G, high latency
- **Test UI behavior:** Validate use of loading indicators
- **Timeout Handling:** Ensure the app responds gracefully to timeouts
- **Data Optimization:** Check if large resources (e.g., images) are efficiently loaded

#### 3. Breakpoints and Modifying Requests/Responses
- Intercept and modify data before it reaches the app/server
- **Edge Cases:** Manually test rare input combinations
- **Error Simulation:** Force custom server errors (e.g., 500, 403)
- **Layout Validation:** Inject long text, special characters, or invalid content

#### 4. SSL Proxying (HTTPS Decryption)
- Decrypt and inspect HTTPS traffic using Charles's root certificate
- Enables visibility into secure API traffic

#### 5. Map Remote and Rewrite Tools
- **Map Remote:** Redirect traffic to a staging/dev server without modifying the app
- **Rewrite Tool:** Automatically modify headers, query parameters, or response data

---

## 1. How to Test Push Notifications in Mobile Apps?

Testing push notifications is important to ensure messages are delivered and displayed correctly on different devices and OS versions.

### Steps:
1. **Enable Push in the App**
   - Make sure the app is installed and has push permissions enabled in settings.
   - For iOS: Settings → Notifications → [Your App].
   - For Android: Settings → Apps → Notifications.

2. **Send Test Notifications**
   - Use **Firebase Cloud Messaging (FCM)** for Android and **Apple Push Notification Service (APNs)** for iOS.
   - Developers can also use server scripts or tools like **Postman** to trigger test pushes.

3. **Check Behavior**
   - Verify the notification arrives (foreground, background, and when the app is closed).
   - Check text, icon, sound, and deep links (does the correct screen open?).
   - Test on multiple OS versions and device models.

4. **Edge Cases**
   - Disabled network → notification should be queued/delayed.
   - User denies permissions → app should handle gracefully.
   - Multiple notifications → check grouping and stacking behavior.

---

## 2. How to Use Android Studio and Xcode for Manual Testing?

Both **Android Studio** (for Android) and **Xcode** (for iOS) can be used by QA engineers to install, run, and debug apps during manual testing.

### Android Studio
1. **Set Up Emulator**
   - Go to `Tools → Device Manager → Create Virtual Device`.
   - Select phone model and Android version.
   - Start the emulator.

2. **Install and Run App**
   - Load the `.apk` or project into Android Studio.
   - Click **Run ▶️** to install on emulator or real device.
   - Logs and errors appear in **Logcat**.

3. **Testing Features**
   - Use emulator tools: simulate calls, SMS, GPS location, battery, rotation.
   - Capture logs for bug reporting.

---

### Xcode (for iOS)
1. **Set Up Simulator**
   - Open `Xcode → Window → Devices and Simulators`.
   - Choose device type (iPhone, iPad) and iOS version.

2. **Install and Run App**
   - Load the `.ipa` or project into Xcode.
   - Click **Run ▶️** to install on simulator or real iPhone (requires developer certificate).
   - Logs appear in the **Debug console**.

3. **Testing Features**
   - Use simulator menu to simulate rotation, memory warnings, and location.
   - For real devices: capture system logs via **Console app** or **Xcode Devices**.

---
# ✅ UI Testing Checklist

## 🔹 Basic UI Elements
- [ ] All **buttons** are clickable and perform the correct action  
- [ ] **Text fields** accept valid input and show proper error messages for invalid input  
- [ ] **Checkboxes, switches, radio buttons** work correctly and reflect state changes  
- [ ] **Labels, icons, and tooltips** are displayed clearly and correctly  
- [ ] No overlapping or cut-off text on different screen sizes  

---

## 🔹 Navigation & Flows
- [ ] App **launches without crashes**  
- [ ] Navigation between **Activities/Fragments** works as expected  
- [ ] **Back button** returns to the correct screen  
- [ ] **Intents** (e.g., opening email, maps) trigger properly  
- [ ] **Deep links** open the right screen  

---

## 🔹 Lists & Dynamic Content
- [ ] **RecyclerView/ListView** scrolls smoothly  
- [ ] Items are **loaded, displayed, and clickable**  
- [ ] Pagination or lazy loading works  
- [ ] Pull-to-refresh updates content  

---

## 🔹 System & Permissions
- [ ] **Permissions dialogs** appear and handle correctly (Allow/Deny)  
- [ ] Notifications are displayed properly (with correct icon/text)  
- [ ] Push notifications open the right screen when tapped  
- [ ] Background/foreground transitions don’t break UI  

---

## 🔹 Device States & Configurations
- [ ] Works in **portrait** and **landscape** mode  
- [ ] Handles **screen rotation** without crashing or losing data  
- [ ] App responds to **offline mode** gracefully (no crash, proper error message)  
- [ ] Works with **different screen sizes** (phone, tablet, foldable)  
- [ ] **Dark/Light themes** display correctly  

---

## 🔹 Visual & Accessibility
- [ ] **Layouts, spacing, and alignment** look correct across devices  
- [ ] Text is **readable** (contrast, font size scaling)  
- [ ] App is usable with **TalkBack/VoiceOver**  
- [ ] **Content descriptions** exist for icons/images  
- [ ] No broken/missing images or icons  

---

## 🔹 Performance
- [ ] No **UI freezes or ANRs** when interacting with screens  
- [ ] Memory usage is stable (no leaks)  
- [ ] Screen transitions are smooth (no jank or frame drops)  
- [ ] Battery drain is reasonable under normal use  

---

## 🔹 Testing Tools
- [ ] Espresso tests cover main flows  
- [ ] UI Automator tests handle system dialogs  
- [ ] Logs (Logcat) are captured for failed test runs  
- [ ] Screenshots are taken for **visual regression comparison**  
