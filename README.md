# Holo Card AR prototype

This is a one-card, no-install WebAR prototype. The page uses MindAR image tracking to keep a 3D character attached to the card in the camera view.

## Run the current Hainanese chicken rice prototype

1. In a terminal, change into this `holo-card-ar` folder and run `node server.js`.
2. Open **http://localhost:8000** on the same computer. Do not open `index.html` directly as a `file://` URL; the browser blocks the model and tracking-file requests that way.
3. Allow camera access, then point the webcam at a print or another screen showing `assets/target_holo.png`.
4. For a phone test, host this folder at an **HTTPS** URL, open it in Safari or Chrome, allow camera access, and point the phone at the card. A plain local-network HTTP address will not grant phone camera access.

The page currently uses `assets/targets.mind` and `assets/hainanese_chicken_rice.glb`.
The food model is scaled to 20% and rotated 90 degrees so the plate faces the camera and occupies about two-thirds of the tracked card width.

The model metadata credits [National Heritage Board, "Hainanese Chicken Rice"](https://sketchfab.com/3d-models/hainanese-chicken-rice-6a0d0aa3851849508f584248f96cd417) under [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/). Keep this attribution with any published prototype that uses it.

## Use a different card or model later

1. Finish one card face. Use an image with clear, varied detail across the card; use the *final* artwork as the tracking target.
2. Upload that image to the [MindAR image target compiler](https://hiukim.github.io/mind-ar-js-doc/tools/compile/), inspect the feature distribution, and replace `assets/targets.mind` with the new file.
3. Change `imageTargetSrc` in `index.html` to `./assets/targets.mind`.
4. Export your character as a lightweight `.glb`, save it in `assets`, and change the `a-asset-item` URL in `index.html` to its filename.
5. Adjust the model's `scale`, `position`, and `rotation` until it appears to emerge from the artwork. Keep `targetIndex: 0` for the first card.
6. Print a QR code that links to the hosted page. Put it on the back or outside the tracked artwork. Test the *printed* card on iPhone and Android in bright and dim light, especially if it has reflective foil.

The QR code opens the webpage. Once open, the webpage uses the card artwork as its tracking target; the QR code itself does not keep the model attached to the card.

## Put it on the web

The `publish` folder contains the ready-to-upload static site. It has `index.html` plus the tracking image, compiled target, and 3 MB model. It excludes the local Node server and the unused 22 MB model.

1. Visit [Netlify Drop](https://app.netlify.com/drop) and drag the entire `publish` folder onto the upload area.
2. Open the resulting `https://...netlify.app` address on a phone, allow camera access, and point it at the printed card.
3. Make a QR code for that final address. To update the site later, rebuild the `publish` folder from the latest source files and upload it again through the site's deploy page.

Keep the 3D model attribution on the page when publishing.

## References

- [MindAR quick start](https://hiukim.github.io/mind-ar-js-doc/quick-start/overview/)
- [MindAR target compilation](https://hiukim.github.io/mind-ar-js-doc/quick-start/compile/)
- [Camera permission and HTTPS requirement](https://developer.mozilla.org/en-US/docs/Web/API/MediaDevices/getUserMedia)
