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
- **Don’t rely only on automation**: Tools like axe catch ~30–40% of issues—manual testing is essential.

## 🧠 Bonus
- Follow **WCAG 2.1 AA** guidelines.
- Include accessibility tests in your **Definition of Done (DoD)**.
- Educate developers on accessible components and common mistakes.

> 💬 Accessibility is not a feature—it’s a responsibility. Testing with empathy helps everyone access your product with dignity and ease.
