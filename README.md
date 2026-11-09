# tucarmd.github.io — CarMD Connect deep link test site

Test-only copy of the `app.carmd.com` deep link pages, used to try the deferred deep link solution for Sprint 213
(CC-901, CC-903, CC-905) before anything changes on the production domain.

The site has to be the user site (`tucarmd.github.io`), not a project site. iOS and Android only read
`apple-app-site-association` and `assetlinks.json` from the root of the domain.

## Pages

- `/promo/?code=XXXXXX`: promo code page. Add `&debug=1` to see the generated URLs.
  - Android: opens the app with `carmd-connect://promo?code=…`. If the app is missing, it goes to the Play Store with
    `referrer=promo_code%3D…`.
  - iOS: the "Copy code & Get the app" button copies `CARMD-PROMO:<code>` to the clipboard and opens the App Store.
  - Desktop: shows the code only (CC-903).
- `/deeplink/group/index.html?qr=…`: copy of the group invite page.
- `/verify-email/?email=…&status=…`: copy of the verify email page.

## Verification files

- `/.well-known/assetlinks.json`: the 3 fingerprints served by `app.carmd.com` today (includes the shared debug key).
- `/apple-app-site-association` and `/.well-known/apple-app-site-association`: app `D258PF2KBU.com.carmd.connect`,
  paths `/promo*`, `/deeplink/group/*`, `/verify-email*`.
- `.nojekyll` makes GitHub Pages publish the `.well-known` folder.

App side: branch `feat/CC-901-deferred-deeplink-test` in `carmd-dev/carmd-connect-app`.
