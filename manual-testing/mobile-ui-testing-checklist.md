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
