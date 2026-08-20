# ITS Video Player SDK (Enterprise Edition)

[![Version](https://img.shields.io/badge/version-3.0.9-blue.svg)](https://github.com/itsignaturepvtltd/ITS_Js_Web_Player_SDK)
[![License](https://img.shields.io/badge/license-Proprietary-red.svg)](https://www.itsignature.com)
[![Security](https://img.shields.io/badge/security-AES--256%20Encrypted-success.svg)](#security-features)

The **ITS Video Player SDK** is an enterprise-grade, highly secure HTML5 & YouTube video player JavaScript library engineered for LMS, E-Learning, and private educational platforms.

---

## 🌟 Key Features

* 🔐 **AES-256 Client-Side Decryption:** Video IDs are encrypted on the backend and decrypted securely at runtime.
* 🛡️ **Screen Recording & Copy Protection:** Dynamic user watermark floating overlay (Student Name, User ID, Phone Number).
* 🚫 **Anti-DevTools & Debugging Lock:** Prevents F12, right-click context menu, inspect element, and debugger timing traps.
* 📱 **iOS Inline Playback & PiP Prevention:** Enforces `playsinline: 1` and disables Picture-in-Picture on Apple Safari / iOS devices.
* ⏱️ **Watch Progress Sync & View Limit:** Real-time periodic API callbacks for attendance tracking and view count restrictions.

---

## 🚀 Quick Start / CDN Embed

Include the minified CSS and obfuscated JavaScript SDK in your web application:

```html
<!-- 1. ITS Video Player SDK CSS -->
<link rel="stylesheet" href="https://cdn.jsdelivr.net/gh/itsignaturepvtltd/ITS_Js_Web_Player_SDK@main/dist/its-video-player.min.css">

<!-- 2. Domain Security Token (Optional Anti-Theft Lock) -->
<!-- Double-base64 encoded domain token on body tag prevents unauthorized site embedding -->
<body id="app-id" data-id="YkcxekxtMWhaM1Z6WTNWaVpTNWpiMjA9">

<!-- 3. Target Player Container (Inline Container OR Inside Popup Modal) -->
<div id="videoContainer"></div>

<!-- Modal Container Example (Optional for Popup Player) -->
<div id="itsModal" class="its-modal" style="display:none;">
    <div id="itsModalBody" class="its-modal-content its-fullscreen">
        <span class="its-close">&times;</span>
        <div id="modalPlayerTarget"></div>
    </div>
</div>

<!-- 4. ITS Video Player SDK JS -->
<script src="https://cdn.jsdelivr.net/gh/itsignaturepvtltd/ITS_Js_Web_Player_SDK@main/dist/its-video-player.min.js"></script>

<script>
  // Instantiate ITS Video Player
  const player = new ITSVideoPlayer(
    "videoContainer",                                     // 1. Target Container DIV ID
    "ENCRYPTED_AES256_YOUTUBE_ID",                        // 2. Encrypted YouTube Video ID String
    "Student Name (0771234567)",                          // 3. Watermark Text / Student Info
    "https://yourdomain.com/logo.png",                    // 4. Branding Logo URL
    "Play Video",                                         // 5. Button Text
    "fullscreen-button",                                  // 6. Button CSS Class
    "landscape",                                          // 7. Orientation ('landscape' / 'portrait')
    3,                                                    // 8. Allowed View Count Limit
    101,                                                  // 9. Category / Lesson ID
    true,                                                 // 10. Enable Progress API Sync (true/false)
    false,                                                // 11. Enable View Count API Sync (true/false)
    "USER_DECRYPTION_KEY",                                // 12. AES-256 Key Material 1 (UserId)
    "PHONE_DECRYPTION_KEY",                               // 13. AES-256 Key Material 2 (Phone)
    "https://yourdomain.com/demo/callback.php",           // 14. Custom API Base Endpoint URL
    false,                                                // 15. Enable Autoplay on Load (true/false)
    true,                                                 // 16. Show Access/Continue Prompt Popup (true/false)
    true                                                  // 17. Auto Show Bottom Controls Bar on Play (true/false)
  );
</script>
```

---

## ⚙️ Configuration Parameters

| # | Parameter | Type | Description |
|---|---|---|---|
| 1 | `playerId` | `string` | Target HTML Container DIV ID |
| 2 | `videoId` | `string` | AES-256 Encrypted YouTube Video ID |
| 3 | `userName` | `string` | Student Name / Phone Number for Floating Watermark |
| 4 | `logoUrl` | `string` | Custom Watermark Branding Logo Image URL |
| 5 | `fullScreenButtonText` | `string` | Button Label Text (`"Play"`) |
| 6 | `fullScreenButtonClasses` | `string` | Button CSS Class (`"fullscreen-button"`) |
| 7 | `orientation` | `string` | Display orientation (`"landscape"` / `"portrait"`) |
| 8 | `viewCount` | `number` | Allowed maximum view limit |
| 9 | `catId` | `number` / `string` | Lesson / Category ID for tracking |
| 10 | `isEnableProgressSync` | `boolean` | Enables background progress API sync every 5 seconds |
| 11 | `isEnableViewCountSync` | `boolean` | Enables view count API sync |
| 12 | `decryptKeyUserId` | `string` | AES-256 key material 1 |
| 13 | `decryptKeyPhoneNumber` | `string` | AES-256 key material 2 |
| 14 | `customApiUrl` | `string` | Custom API Endpoint Base URL (e.g., `"https://api.lms.com/callback.php"`) |
| 15 | `isAutoPlay` | `boolean` | Enables automatic video playback when player loads (default: `false`) |
| 16 | `isShowPrompt` | `boolean` | Shows video access/continue prompt popup overlay (default: `true`) |
| 17 | `isShowControls` | `boolean` | Auto shows bottom controls bar on video play start (default: `true`) |

---

## 📥 Backend API Callback Protocol

When `isEnableProgressSync` is enabled, the player sends periodic HTTP POST requests to `${customApiUrl}/save-progress`:

### Request Body (`POST`):
```json
{
  "userId": "student_001",
  "videoId": 101,
  "time": 145.2,
  "duration": 600,
  "timestamp": "2026-08-07T15:00:00.000Z",
  "isCompleted": false
}
```

### Expected Response (`JSON`):
```json
{
  "status": "success",
  "data": {
    "viewCount": 1,
    "time": 145.2
  }
}
```

---

## 🔒 Security & Rights

Copyright (c) 2026 **ITSignature Pvt Ltd**. All Rights Reserved.
Unauthorised distribution or reproduction of this SDK is strictly prohibited.
