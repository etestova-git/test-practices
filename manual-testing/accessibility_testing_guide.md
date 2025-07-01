# Accessibility (A11y) Testing Guide for QA Engineers

## 👨‍🔧 1. How to Perform Accessibility Testing

### 🧪 Web Applications
- Use a screen reader like **NVDA** (Windows) or **VoiceOver** (macOS).
- Navigate using keyboard only (Tab, Shift+Tab, Enter, Space, Arrow keys).
- Test dynamic components (modals, dropdowns, popups) for keyboard and screen reader support.
- Validate semantic HTML: use proper headings, landmark roles (`<nav>`, `<main>`, `<header>`, etc.).

### 📱 Mobile Applications (iOS / Android)
- Enable **VoiceOver** (iOS) or **TalkBack** (Android).
- Use gestures to navigate the app and check that all elements are announced correctly.
- Test custom controls and gesture-based components for proper accessibility behavior.
- Ensure screen reader focus follows visual focus.

## 🛠 2. Tools to Use

### Web
| Tool               | Purpose                                       |
|--------------------|-----------------------------------------------|
| **NVDA**           | Free screen reader for Windows                |
| **VoiceOver**      | Built-in screen reader on macOS/iOS           |
| **axe DevTools**   | Browser extension for automated a11y testing  |
| **Lighthouse**     | Chrome tool for accessibility audits          |
| **WAVE**           | Web accessibility evaluation tool             |
| **Keyboard only**  | Manual keyboard navigation                    |

### Mobile
| Platform   | Tools                                      |
|------------|--------------------------------------------|
| iOS        | VoiceOver, Accessibility Inspector (Xcode) |
| Android    | TalkBack, Accessibility Scanner            |

## 🔍 3. What to Test

- **Screen reader compatibility**: Are all UI elements read out loud clearly and in logical order?
- **Keyboard navigation**: Can all actions be completed using only the keyboard?
- **Focus management**: Does the focus move logically between UI elements?
- **Color contrast**: Text should have a contrast ratio of at least 4.5:1.
- **Labels & roles**: Ensure buttons, links, and inputs have accessible labels and ARIA roles.
- **Alt text**: Images must have meaningful `alt` text.
- **Form validation**: Error messages should be announced clearly to assistive tech.

## 💡 4. A11y Testing Tips & Tricks

- **Use tab order to catch hidden traps**: If you get “lost” while tabbing, so will screen reader users.
- **Inspect ARIA attributes**: Misused ARIA can break accessibility—use them only when needed.
- **Reduce motion settings**: Honor OS-level “reduce motion” preferences for animations.
- **Screen reader practice**: Learn common gestures and commands for NVDA, VoiceOver, and TalkBack.
- **Use real devices**: Emulators miss subtle behavior (e.g., custom gesture issues).
- **Annotate a11y bugs clearly**: Include steps to reproduce with screen reader or keyboard only.

---

### **Screen Reader Command & Gesture Cheat Sheet**

| Action / Command | NVDA (Windows) | VoiceOver (iOS - Touch Gestures) | TalkBack (Android - Touch Gestures) |
| :--- | :--- | :--- | :--- |
| **Start/Stop Reading** | `Ctrl` | Two-finger tap | Two-finger tap |
| **Read Next Item** | `Down Arrow` or `Tab` | Swipe right | Swipe right |
| **Read Previous Item** | `Up Arrow` or `Shift`+`Tab` | Swipe left | Swipe left |
| **Activate Item (Click)** | `Enter` or `Space` | Double-tap anywhere | Double-tap anywhere |
| **Go to Next Heading** | `H` | Swipe down/up to "Headings", then swipe right/left | Swipe up then down (or down then up) to "Headings", then swipe right/left |
| **Go to Next Link** | `K` | Swipe down/up to "Links", then swipe right/left | Swipe up then down to "Links", then swipe right/left |
| **Go to Next Form Field** | `F` | Swipe down/up to "Form Controls", then swipe right/left | Swipe up then down to "Form Controls", then swipe right/left |
| **Go to Next Button** | `B` | Swipe down/up to "Form Controls", then swipe right/left | Swipe up then down to "Buttons", then swipe right/left |
| **Go to Next Table** | `T` | Swipe down/up to "Tables", then swipe right/left | Swipe up then down to "Tables", then swipe right/left |
| **Read Page Title** | `NVDA`+`T` | (Usually read on page load) | (Usually read on page load) |
| **List All Elements** | `NVDA`+`F7` | **The Rotor:** Two-finger twist gesture | **The Reading Menu:** Swipe up then down (or down then up) |
| **Scroll Down a Page** | *(Handled by browser)* | Three-finger swipe up | Two-finger swipe up |
| **Scroll Up a Page** | *(Handled by browser)* | Three-finger swipe down | Two-finger swipe down |
| **Go to Home Screen** | *(OS command)* | Swipe up from bottom edge | Swipe up from bottom edge |

---

## Follow **WCAG 2.1 AA** guidelines.
  
**1. Perceivable**
- Text Alternatives: All non-text content (like images) must have a text alternative (e.g., alt text) so it can be read by screen readers.
- Captions & Audio Descriptions: Videos must have synchronized captions for the hearing-impaired. Prerecorded videos also need audio descriptions of important visual information for the visually-impaired.
- Adaptable Content: Content must be structured logically (using proper headings) so it can be presented in different ways (e.g., by a screen reader) without losing its meaning.
- Distinguishable Content:
Color is not the only means of conveying information. For example, don't just make an error field's border red; add an icon and text.
- Color Contrast (Crucial AA rule): The visual presentation of text must have a contrast ratio of at least 4.5:1 against its background. For large text (18pt or 14pt bold), the ratio is 3:1.
- Text can be resized up to 200% without loss of content or functionality.
- Reflow: Content can be viewed in a single column (like on a mobile phone at 400% zoom) without requiring horizontal scrolling.

**2. Operable**
- Keyboard Accessible: All functionality must be operable through a keyboard interface without requiring specific timings for individual keystrokes. You must be able to "tab" to every interactive element.
- No Keyboard Traps: A user must be able to navigate to and away from any element using only the keyboard. They can't get stuck in a component.
- Adjustable Timing: If there are time limits, users must be able to turn them off, adjust them, or extend them.
- No Seizures: Pages cannot contain anything that flashes more than three times in any one-second period.
- Navigable: Provide ways to help users navigate and find content, such as a "Skip to Main Content" link and logical page titles and headings.
- Pointer Gestures: If functionality requires a complex gesture (like a two-finger pinch), there must be a way to operate it with a single pointer (e.g., plus/minus buttons for zoom).

**3. Understandable**
- Readable: The language of the page (e.g., lang="en") must be identified in the code.
- Predictable: Navigation and components should behave in predictable ways. Changing a setting should not unexpectedly change the entire page context.
- Error Identification: If an input error is detected, the item in error is identified, and the error is described to the user in text.
- Labels and Instructions: Forms must have clear labels or instructions for all inputs.
- Error Suggestion: If an error is found and suggestions for correction are known, they are provided to the user.

**4. Robust**
- Parsing: Code must be clean, with no major errors (like duplicate element IDs) so that assistive technologies like screen readers can parse it reliably.
- Name, Role, Value: For all custom-built components, their name and role must be programmatically determined (using ARIA attributes if necessary), and their state (e.g., checked, expanded) must be available to assistive technologies.
