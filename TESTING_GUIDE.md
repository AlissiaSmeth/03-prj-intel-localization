# Accessibility Testing Guide
## Intel Sustainability Website

This guide helps you manually test and verify all accessibility features of the website.

---

## Quick Start Testing (5 minutes)

### 1. Test Keyboard Navigation
**Goal:** Verify all interactive elements work with keyboard only

**Steps:**
1. Open the website in your browser
2. Press `Tab` repeatedly to navigate through all elements
3. Observe the **blue focus outline** appears around:
   - Header logo
   - "Learn More" buttons in the 3-column section
   - Form inputs (Name, Email, Checkbox)
   - "Subscribe" button
   - Footer links

**Expected Result:** You can reach and interact with all elements without using a mouse

**Pass/Fail:** _____ 

---

### 2. Test Form Validation
**Goal:** Verify form shows proper error messages and accessibility

**Steps:**
1. Scroll to the "Subscribe to Intel's Sustainability Newsletter" section
2. Click the "Subscribe" button without filling any fields
3. Observe the error messages appear below each field
4. Verify focus automatically moves to the first empty field
5. Fill in the form:
   - Name: "Test User"
   - Email: "test@example.com"
   - Check the consent checkbox
6. Click "Subscribe" again
7. See the success message appear

**Expected Behavior:**
- ❌ Required fields show red error messages
- ❌ Form blocks submission until all fields are valid
- ❌ First invalid field gets keyboard focus (blue outline)
- ✅ Email validation works (try "invalid-email")
- ✅ Success message appears with green background
- ✅ Form resets after 3 seconds

**Pass/Fail:** _____

---

### 3. Test Color Contrast
**Goal:** Verify text is readable against backgrounds

**Visual Check:**
- [ ] Dark blue headings (#0d47a1) on white background - VERY clear
- [ ] Dark gray body text (#212529) on white - VERY clear
- [ ] White button text on dark blue button - VERY clear
- [ ] Gray helper text (#6c757d) on white - CLEAR
- [ ] Red error text (#dc3545) on white - CLEAR

**Use an online tool:**
1. Visit: https://webaim.org/resources/contrastchecker/
2. For any element you're unsure about:
   - Note the foreground color
   - Note the background color
   - Enter into the tool
   - Verify it shows "AA" or "AAA" (it should!)

**Pass/Fail:** _____

---

### 4. Test Image Alt Text
**Goal:** Verify all images have descriptive alternative text

**Method 1: Browser Developer Tools**
1. Right-click on any image → "Inspect" (or press F12)
2. Look for the `alt` attribute in the HTML
3. Verify the alt text describes the image meaningfully

**Method 2: Disable images**
1. Disable images in your browser (Developer Tools → Settings)
2. Reload the page
3. You should still understand what each image represents from its alt text

**Timeline Images Should Have Alt Text Like:**
- "Intel founders Robert Noyce and Gordon Moore in 1968 establishing Intel Corporation"
- "Intel 4004 microprocessor, the world's first commercial microprocessor from 1971"
- "Chart showing Intel's peak greenhouse gas emissions in 2006 with downward trend afterward"

**Pass/Fail:** _____

---

## Advanced Testing (15 minutes)

### 5. Test with Screen Reader
**For Windows Users (NVDA):**
1. Download NVDA: https://www.nvaccess.org/download/
2. Install and start NVDA
3. Press `Ctrl + Home` to go to page start
4. Press `H` repeatedly to navigate through headings
5. Press `K` to jump between links
6. Use arrow keys to read content

**For Mac Users (VoiceOver):**
1. System Preferences → Accessibility → VoiceOver
2. Press `Cmd + F5` to enable VoiceOver
3. Use `VO + U` (where VO = Control + Option) to open rotor
4. Navigate using VO + arrow keys

**Expected Behavior:**
- Screen reader announces all headings
- Form fields are announced with their labels
- Button purposes are clear
- Images have descriptive alt text read aloud
- Links are identified clearly

**Pass/Fail:** _____

---

### 6. Test Zoom (200%)
**Goal:** Verify site is usable when zoomed in

**Steps:**
1. Press `Ctrl + +` (or Cmd + +) three times to zoom to 200%
2. Verify no text is cut off
3. Verify form is still usable
4. Verify buttons are still clickable
5. Verify no horizontal scrolling required (if possible)

**Expected Result:** Site remains usable and readable at 200% zoom

**Pass/Fail:** _____

---

### 7. Test RTL (Right-to-Left) Text
**Goal:** Verify the site works in RTL languages

**Browser Language Switch Method:**
1. Open Developer Tools (F12)
2. Go to Console
3. Run these commands:

```javascript
// Switch to Arabic (RTL)
document.documentElement.lang = 'ar';

// Switch back to English (LTR)
document.documentElement.lang = 'en';
```

**Expected Behavior:**
- ✅ When set to 'ar' or 'he': Text direction becomes right-to-left
- ✅ Grid columns flip direction automatically
- ✅ Buttons and form elements flip
- ✅ Bootstrap RTL stylesheet loads automatically

**Visual Indicators of RTL:**
- Text reads from right to left
- Layout mirrors horizontally
- Numbers and punctuation may behave differently

**Pass/Fail:** _____

---

### 8. Test Link Underlines (Focus Indicators)
**Goal:** Verify focus indicators are visible

**Steps:**
1. Tab through the page
2. When focus is on a link or button, you should see:
   - **2px solid blue outline** around the element
   - Outline should have clear contrast with background

**Expected Result:** Every interactive element has a visible, clear focus indicator

**Pass/Fail:** _____

---

### 9. Validate HTML
**Goal:** Verify no semantic HTML errors

**Method:**
1. Visit: https://validator.w3.org/
2. Enter your site URL or paste HTML
3. Check for errors
4. Expected: No errors, only warnings (if any)

**Common Elements to Verify:**
- ✅ Proper heading hierarchy (h1 → h2 → h3)
- ✅ No empty headings
- ✅ Form has label for every input
- ✅ Button text is descriptive
- ✅ Navigation is semantically marked

**Pass/Fail:** _____

---

### 10. Mobile Touch Testing
**Goal:** Verify touch targets are appropriately sized

**If on Desktop:**
1. Open Developer Tools (F12)
2. Toggle Device Toolbar (or Ctrl+Shift+M)
3. Switch to mobile view

**Verify:**
- [ ] Buttons are at least 44x44 pixels
- [ ] Form inputs are easy to tap
- [ ] Links have adequate spacing
- [ ] No element is too small to interact with

**Expected:** Comfortable touch interaction without misclicks

**Pass/Fail:** _____

---

## Detailed Feature Testing

### Form Accessibility Checklist

#### Full Name Field
- [ ] Has visible label "Full Name"
- [ ] Label is properly associated via `for` attribute
- [ ] Input has `aria-required="true"`
- [ ] Helper text below: "Please enter your first and last name"
- [ ] Error message appears when empty
- [ ] Field shows blue outline when focused

#### Email Field
- [ ] Has visible label "Email Address"
- [ ] Accepts only valid email format
- [ ] Shows error if format is wrong (try: "invalid")
- [ ] Helper text: "We'll never share your email..."
- [ ] Has `aria-required="true"`
- [ ] Field shows blue outline when focused

#### Consent Checkbox
- [ ] Has visible label "I agree to receive..."
- [ ] Shows error if not checked before submit
- [ ] Has `aria-required="true"`
- [ ] Helper text explains what consent means

#### Submit Button
- [ ] Has text label: "Subscribe"
- [ ] Shows blue outline when focused
- [ ] Can be activated with spacebar or Enter
- [ ] Disables after submit (prevents double-submit)
- [ ] Shows success message: green background with checkmark

---

## Color Contrast Verification

### Using Browser Extension

**Install axe DevTools:**
1. Chrome: https://chrome.google.com/webstore
2. Search for "axe DevTools"
3. Install and enable
4. Run scan → Check "Color Contrast" section
5. All should show ✅ PASS

**Install WAVE:**
1. Chrome/Firefox: Search "WAVE Web Accessibility Evaluation Tool"
2. Click the WAVE icon
3. Look for red/yellow contrast warnings
4. Should be minimal or none

---

## Accessibility Issues Log

Use this table to log any issues you find:

| # | Issue Description | Location | Severity | Status |
|---|---|---|---|---|
| 1 | | | | |
| 2 | | | | |
| 3 | | | | |

**Severity Levels:**
- 🔴 Critical: Blocks access for some users
- 🟠 High: Significantly impacts usability
- 🟡 Medium: Noticeable impact on some users
- 🟢 Low: Minor issue

---

## Quick Checklist Summary

```
Keyboard Navigation
  ☐ Tab navigates all elements
  ☐ Shift+Tab goes backwards
  ☐ Enter activates buttons
  ☐ Space activates checkboxes
  ☐ All elements have focus indicators

Form Validation
  ☐ Required fields marked
  ☐ Error messages shown
  ☐ Focus moves to errors
  ☐ Success message shown
  ☐ Form resets properly

Color Contrast
  ☐ Headings are dark and bold
  ☐ Body text is readable
  ☐ Links are distinguishable
  ☐ Buttons have contrast
  ☐ Helper text is visible

Images
  ☐ All images have alt text
  ☐ Alt text is descriptive
  ☐ Alt text isn't redundant

Focus & Navigation
  ☐ Blue outline visible on focus
  ☐ Logical tab order
  ☐ No focus traps
  ☐ Footer links keyboard accessible

RTL Support
  ☐ Arabic layout works
  ☐ Hebrew layout works
  ☐ Layout flips correctly
  ☐ Bootstrap CSS switches

Responsive Design
  ☐ Mobile (< 640px) works
  ☐ Tablet (640px - 1024px) works
  ☐ Desktop (> 1024px) works
  ☐ Form stacks on mobile
  ☐ No horizontal scroll on mobile

ARIA
  ☐ Form fields have aria-required
  ☐ Descriptions have aria-describedby
  ☐ Alerts have role="alert"
  ☐ Error fields have aria-invalid
```

---

## Recommended Tools for Testing

### Free Online Tools
- **WAVE:** https://wave.webaim.org/
- **Lighthouse:** Built into Chrome DevTools
- **axe DevTools:** https://www.deque.com/axe/devtools/
- **Color Contrast Checker:** https://webaim.org/resources/contrastchecker/
- **HTML Validator:** https://validator.w3.org/

### Assistive Technology (Free)
- **NVDA (Windows):** https://www.nvaccess.org/download/
- **JAWS (Windows):** Trial version available
- **VoiceOver (Mac/iOS):** Built-in
- **TalkBack (Android):** Built-in
- **ORCA (Linux):** Usually pre-installed

### Browser Extensions
- **axe DevTools** (Chrome/Firefox)
- **WAVE** (Chrome/Firefox)
- **Lighthouse** (Chrome only, built-in)
- **Contrast Ratio** (Chrome/Firefox)
- **Keyboard Navigation Tester** (Chrome)

---

## Testing Results

**Test Date:** _______________
**Tester Name:** _______________
**Browser:** _______________
**Operating System:** _______________

**Overall Result:**
- ☐ Fully Accessible ✅
- ☐ Mostly Accessible (minor issues)
- ☐ Needs Improvement (significant issues)
- ☐ Not Accessible (critical issues)

**Comments:**
_____________________________________________________________________

_____________________________________________________________________

_____________________________________________________________________

---

## Next Steps

1. **Share Results:** Report findings to the development team
2. **Priority:** Focus on critical and high-severity issues first
3. **Retest:** After fixes, retest using this guide
4. **Regular Review:** Test accessibility quarterly or after major changes

---

**For More Information:**
- WebAIM: https://webaim.org/
- W3C WCAG: https://www.w3.org/WAI/WCAG21/quickref/
- MDN Web Docs: https://developer.mozilla.org/en-US/docs/Web/Accessibility

