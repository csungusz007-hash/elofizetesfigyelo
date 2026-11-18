# Előfizetés-figyelő

Android-alkalmazás, ami megmutatja, mennyit fizetsz havonta és évente az előfizetéseidre, és értesít, mielőtt levonják a következő díjat vagy lejár egy ingyenes próbaidő.

**Funkciók**
- Előfizetések listája a következő terhelés szerint rendezve: „Próbaidő”, „Következő 7 nap”, „Később”
- Havi és éves összesítés (Ft, € és $)
- Gyors felvétel a gyakori szolgáltatásokból (Netflix, Spotify, HBO Max…)
- Próbaidő figyelése: előtte is, az utolsó előtti napon is, és a lejárat napján is szól
- Értesítés 1, 3 vagy 7 nappal a terhelés előtt
- Áttekintés: melyik előfizetés mekkora részt visz el, és mennyi terhelés jön még ebben a hónapban
- Világos és sötét mód, nagy betűméret támogatása, képernyőolvasó-címkék
- Nincs fiók, nincs reklám, és nincs internet-engedély: minden adat a telefonon marad

---

## APK készítése a GitHubbal (Android Studio nélkül)

1. Regisztrálj vagy lépj be a **github.com** oldalon.
2. Jobb felül: **+ → New repository**. Név: `elofizetes-figyelo` → **Create repository**.
3. Kattints az **„uploading an existing file”** linkre, és húzd be a kicsomagolt mappa **teljes tartalmát**: az `app`, `gradle` és `.github` mappát, valamint a többi fájlt.
   - Macen a `.github` mappa rejtett. A Finderben a **Cmd + Shift + .** billentyűkkel jeleníted meg.
   - Ha a `.github` mappa mégsem töltődne fel: **Add file → Create new file**, a fájl neve legyen `.github/workflows/build.yml`, a tartalmába pedig másold be a csomagban lévő azonos nevű fájlt.
4. **Commit changes**.
5. Nyisd meg az **Actions** fület. Az „APK build” magától elindul, és kb. 5–8 percig tart.
6. Ha zöld pipát látsz, kattints a futásra. Lent az **Artifacts** résznél töltsd le az **Elofizetes-figyelo-APK** csomagot.
7. A ZIP-ben két APK van:
   - `release/app-release.apk`: kisebb, ezt ajánlom
   - `debug/app-debug.apk`: tartalék
8. Másold az APK-t a telefonodra, és nyisd meg. Engedélyezd az „Ismeretlen forrásból származó alkalmazások telepítése” lehetőséget.

## Feltöltés a Google Play áruházba

A Play áruház nem APK-t kér, hanem **saját kulccsal aláírt AAB-fájlt**.

1. Hozz létre fejlesztői fiókot: **play.google.com/console** (egyszeri 25 USD).
2. Nyisd meg a projektet **Android Studióban** → **Build → Generate Signed App Bundle / APK → Android App Bundle**. Hozz létre új kulcsot (keystore), és **őrizd meg biztonságos helyen**, mert minden frissítéshez kelleni fog.
3. Play Console → **Alkalmazás létrehozása** → töltsd fel az `.aab` fájlt.
4. Az **Adatbiztonság** űrlapon jelölheted, hogy az app **nem gyűjt és nem oszt meg adatot**.
5. Kell még: ikon (512×512), legalább 2 képernyőkép és egy rövid leírás.

Új fejlesztői fiókoknál a Google először zárt tesztet kér (általában 12 tesztelő, 14 napig), csak utána engedi a nyilvános megjelenést.

## Technikai adatok
- Kotlin + Jetpack Compose, minSdk 26 (Android 8.0), targetSdk 35
- Értesítések: WorkManager, naponta reggel 9 körül
- Adatok: helyi JSON-fájl
