# Masjid Putra visitor tour

A mobile web tour for non-Muslim visitors to Masjid Putra, Putrajaya. Visitors walk eight stations, from borrowing a robe to hearing the adhan. At each one they can read or listen to what happens there and why it matters to Muslims, with the Quran and hadith sources behind it.

**Status:** prototype. The content is pending scholar review (see [CONTENT-REVIEW.md](CONTENT-REVIEW.md)), and the illustrations stand in for real photography.

## What's in it

- `index.html` is the whole app: a single page with no build step. Routes are hash URLs (`#tour`, `#ablution`, `#more-ablution`, `#questions`, `#finish`, `#plaques`).
- `vendor/` holds two small libraries the page loads only when needed:
  - [jsQR 1.4.0](https://github.com/cozmo/jsQR) (Apache-2.0) decodes QR codes in browsers that lack the built-in `BarcodeDetector`, such as iOS Safari and Firefox.
  - [qrcode-generator 1.4.4](https://github.com/kazuhikoarase/qrcode-generator) (MIT) draws the printable station plaques.

## Station QR codes

Each station plaque carries a QR code for `<published URL>#<station id>`. That gives visitors two ways in:

- Tap **Scan station code** in the tour. This opens the rear camera in the page. If the camera can't start, or the visitor declines permission, the page opens the next unvisited station instead.
- Point the phone's own camera app at the code. The tour opens straight at that station.

To print the codes, open `#plaques` from the address you'll publish to; there's a link at the foot of the welcome screen. Codes printed from `localhost` point to `localhost`.

The camera works only over HTTPS (or `localhost`), which GitHub Pages provides.

## Run locally

```sh
python3 -m http.server 8000
# open http://localhost:8000
```

## Publish on GitHub Pages

In the repository, go to **Settings → Pages → Build and deployment**. Set **Source** to *Deploy from a branch*, choose `main` and `/ (root)`, and save. The site appears at `https://<user>.github.io/masjid-putra-tour-demo/`.

## Adapting it to another mosque

The mosque's name and intro are in `MOSQUE` near the top of the script. The stations are in `STATIONS`, the FAQ is in `FAQ`, and the floor-plan coordinates are in `STOPS` and `ROUTE`.

## Not built yet

- **Other languages.** The language buttons show a "coming in the pilot" note. Translations of religious content need native-speaking translators and the same scholar review as the English.
- **Recorded narration.** The listen button uses the device's text-to-speech for now.
- **Real photos and floor plan.**
- **Back end.** Guide questions and visitor feedback are stored only on the visitor's own phone (`localStorage`). Nothing reaches mosque staff yet.
