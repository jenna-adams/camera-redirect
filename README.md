# QR Code Scanner Demo

A mobile-optimized demo comparing two approaches to QR code scanning on Android devices.

## Overview

This app demonstrates the tradeoffs between two QR scanning approaches:

1. **Web Scanner** - Browser-based scanning with full control
2. **Native Camera** - Deep-linking to the device's camera app

## The Two Approaches

### 🌐 Web Scanner (Recommended)

**How it works:** Launches a webpage that requests camera access and scans QR codes directly in the browser using the [html5-qrcode](https://github.com/mebjas/html5-qrcode) library.

**Pros:**
- ✅ **100% reliability** - Works on every Android device with a browser
- ✅ **Full control** - Customize the UX exactly how you want
- ✅ **Flexible scanning** - Build it for instant auto-scan (max speed) or "tap to scan" (user control)
- ✅ **Rich feedback** - Add vibration, animations, custom success states
- ✅ **No device fragmentation** - One experience across all devices

**Cons:**
- ❌ **One-time permission** - User must grant camera access on first use
- ❌ **Requires HTTPS** - Camera API only works on secure connections
- ❌ **Browser dependency** - Needs modern browser with camera support

---

### 📱 Native Camera (Inconsistent)

**How it works:** Deep-links to the device's default camera app using `<input type="file" capture="camera">`.

**Pros:**
- ✅ **No web permissions** - Uses system-level camera access
- ✅ **Familiar UX** - Users see their default camera interface
- ✅ **High quality** - Native camera apps often have better image processing

**Cons:**
- ❌ **Massive fragmentation** - Every manufacturer (Samsung, Google, Motorola, Xiaomi) builds their own camera app
- ❌ **Unreliable QR support** - Many native cameras don't scan QR codes at all
- ❌ **Examples of failures:**
  - Samsung Tab S7 camera doesn't scan/redirect QR codes
  - Budget Android devices often lack QR detection
  - Older devices may not support this feature
- ❌ **Zero control** - Can't customize the scanning experience
- ❌ **Manual capture** - User must tap to take photo, then app processes it

**Bottom line:** If a user's default camera doesn't support QR reading, they're completely out of luck.

---

## Recommendation

**Use the Web Scanner approach** for any production application. The Native Camera option exists only to demonstrate why it's problematic—device fragmentation makes it unreliable across the Android ecosystem.

## Quick Start

1. Open `index.html` in a mobile browser
2. Toggle between modes to compare the experience
3. Grant camera permission when prompted (Web Scanner only)

## Customization

The web scanner can be configured for different use cases:

```javascript
// Auto-scan (instant, like this demo)
const config = { fps: 10, qrbox: { width: 250, height: 250 } };

// Manual scan (user taps to capture)
// Modify onScanSuccess to trigger on button press instead
```

Change what happens after scanning:
```javascript
// Current: Shows alert
alert("Scanned: " + decodedText);

// For redirect:
window.location.href = decodedText;
```

## Requirements

- Modern browser (Chrome, Safari, Firefox, Edge)
- HTTPS connection (for camera access)
- Mobile device recommended (works on desktop for testing)

## Browser Support

- ✅ Chrome/Edge (Android/Desktop)
- ✅ Safari (iOS/macOS)
- ✅ Firefox (Android/Desktop)
- ✅ Samsung Internet

---

**Built with:** HTML5, CSS3, JavaScript, [html5-qrcode](https://github.com/mebjas/html5-qrcode)
