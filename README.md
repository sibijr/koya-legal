# Koya — website and legal pages

https://koyamanifest.com, served by GitHub Pages from this repository. DNS is on Cloudflare
(apex A records to GitHub Pages, `www` CNAME to sibijr.github.io, all DNS only). The old
`sibijr.github.io/koya-legal/...` links redirect here automatically, so links already in the app
and App Store Connect keep working.

- `index.html` — the marketing site (`site.css`). Hero and ambient loops are Veo clips from TakeWeaver
- `get.html` — the single-purpose landing page for paid ads (`/get`)
- `legal.html` — the old index listing the documents
- `support.html` — Support
- `terms.html` — Terms of Use
- `privacy.html` — Privacy Policy
- `style.css` — Koya's brand tokens, taken from `ios/Koya/Theme.swift`

## Why this repository is separate

The app itself lives in a private repository. These pages have to be publicly reachable, because
App Store Connect and the in-app paywall link to them and Apple checks that the links resolve.

## Changing them

These documents describe what the app **actually does**, not what it might do. Before changing a
factual claim here, check it against the code. Three claims in particular were verified and are
easy to get wrong later:

- **Analytics carry no content.** True because `ios/Koya/Analytics.swift` declares every event the
  app can send. If an event is added that carries a story title, a desire or a name, the Privacy
  Policy becomes false.
- **Sleep audio is not personalised.** It is a shared library, the same for everyone. See migration
  `0112_sleep_is_out_of_mlp_scope.sql`.
- **A voice is deleted only with the account.** There is no standalone delete-voice option in the
  app. The `delete-voice` function exists server side but nothing calls it.
- **Account deletion is immediate.** There is no seven day grace period in the app any more; see
  `ios/Koya/DeleteAccount.swift`. The server still supports one, so an account that requested it
  before the change can still cancel, but these pages must not offer it to anybody new.
- **The free sample is per device, disclosed in section 8.** It uses Apple's DeviceCheck, and Koya
  keeps no record of a deleted account. If a tombstone table of deleted identifiers is ever added,
  that section becomes false. Apple also requires the reset path that `support.html` promises, so
  that promise is not decoration.

The minimum age is **18**, and it is enforced in three places: these pages, `AgeTape.low` in
`ios/Koya/OnboardingBits.swift`, and the `profiles_age_check` constraint from migration `0125`.
Changing one without the others makes the documents untrue.

## Contact

koyamanifest@gmail.com
