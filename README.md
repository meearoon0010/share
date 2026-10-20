# Direct Transfer — iOS ↔ Android file sharing

A single-file web app (PWA-friendly) that sends files directly between an iPhone and an Android phone using WebRTC. No server, no accounts, no upload: files go device-to-device.

## Deploy on GitHub Pages
1. Create a new GitHub repo and upload `index.html` and this README.
2. Repo **Settings → Pages → Deploy from a branch → `main` / root**.
3. Open `https://<your-username>.github.io/<repo>/` on **both** phones (HTTPS is required for the camera).

## Use
1. Phone A: **Start** → shows a QR code.
2. Phone B: **Join** → scan A's QR → B shows a reply QR.
3. Phone A: **Scan reply QR**. Connected!
4. Either phone: **Choose files to send**. The other taps **Save**.

QR not working? Tap **QR not working? Use a short code**: one device shows a 6-character code, the other types it (needs internet; uses the free public PeerJS service only to introduce the devices, files still go directly).

No camera? Use **Copy code** and paste it on the other device (e.g. via a chat app).

## Notes
- Works best on the same Wi-Fi; STUN is included so it can also work across networks (strict/symmetric NATs may fail).
- Files are buffered in memory on the receiver, so keep to a few hundred MB on iPhone.
- Needs iOS 16.4+ / a recent Chrome on Android (uses `CompressionStream` to shrink QR codes; falls back to uncompressed).
- Libraries loaded from cdnjs: `qrcode-generator@1.4.4`, `jsQR@1.4.0`.

## Background & offline
- While connected, the app holds a screen wake lock and plays inaudible audio so the browser is less likely to pause it when minimized (best effort — iOS may still suspend it; use the checkbox on the transfer screen to turn this off).
- Add the page to your Home Screen (iOS: Share → Add to Home Screen; Android: Install app). It then opens like an app and works offline, so hotspot transfers need no internet.
- Upload all files: `index.html`, `manifest.webmanifest`, `sw.js`, `icon.svg`, `icon-192.png`, `icon-512.png`.
