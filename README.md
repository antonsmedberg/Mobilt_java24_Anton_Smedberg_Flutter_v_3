# Reflector (Android + Web)

Reflector är min lilla idé om ett gränssnitt som känns lika självklart på mobilen som i webbläsaren. Du gör dina val – namn, mörkt läge, volym – och får direkt se resultatet i en ren förhandsvisning. Jag har hållit det enkelt, lugnt och responsivt.

## Så här funkar det

- Profilsidan: skriv ett visningsnamn, växla mörkt läge, justera volym. “Save & Preview” sparar och går vidare.
- Förhandsvisningen: visar dina val och en nätbild. Tillbaka fungerar både i webben och på Android.
- Preferenserna sparas lokalt och följer med mellan starter.

## Varför just så här?

Två skärmar, tydliga interaktioner och navigation som beter sig likadant på båda plattformar. Ingen överlast – bara det som behövs för en smidig upplevelse.

## Struktur i stora drag

```
lib/
  main.dart
  app/        (router, tema)
  core/       (UserPrefs + Scope)
  features/profile/pages/
    profile_setup_page.dart
    preview_page.dart
web/index.html (brandat, favicon)
test/user_prefs_test.dart
```

## Små val som gör skillnad

- Material 3 med färgtema ger lugn bas; maxbredd (~560 px) gör läsningen behaglig på stora skärmar.
- Spara‑knappen är inaktiverad tills formuläret är giltigt; en liten SnackBar bekräftar sparning.
- Webbnavigering använder `go('/')` istället för “pop” för att undvika tom historik.
- En lokal bild i profilen och en nätbild i förhandsvisningen – enkelt men effektfullt.

## Kort om plattformarna

Webben bryr sig om URL och historik; därför använder jag `go('/')` när man går tillbaka från förhandsvisningen. På Android sköter systemet backstacken, och appen är låst i portrait för stabilitet. Känslan blir konsekvent på båda plattformar.

## Tekniskt i ett nötskal

- Navigering: `go_router` med två rutter (`/`, `/preview`).
- Tillstånd & lagring: `UserPrefs` + `shared_preferences` (namn, mörkt läge, volym).
- UI: Material 3, semantiska bildetiketter, tydliga etiketter och validering.
- Ikoner: Android‑ikoner via `flutter_launcher_icons`, favicon i `web/index.html`.
- API/utmaningar: ingen extern REST‑källa används; CORS för nätbilder beaktat; webben kan varna om trädsakning av ikoner, vilket är ofarligt.

## Kom igång

1) `flutter pub get`
2) `flutter run -d chrome` eller `flutter run -d android`
3) `flutter test`

## Bygga

- APK: `flutter build apk --release` → `build/app/outputs/flutter-apk/app-release.apk`
- Web: `flutter build web --release` → `build/web/`

---

