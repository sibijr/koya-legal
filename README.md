# Koya — legal pages

The Terms of Use and Privacy Policy for the Koya iOS app, served as a static site by GitHub Pages.

- `index.html` — landing page linking to both documents
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

The minimum age is **18**, and it is enforced in three places: these pages, `AgeTape.low` in
`ios/Koya/OnboardingBits.swift`, and the `profiles_age_check` constraint from migration `0125`.
Changing one without the others makes the documents untrue.

## Contact

koyamanifest@gmail.com
