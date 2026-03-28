# 📱 FaceTracker Web — iOS & GitHub Pages

> Realtids ansiktsdetektering direkt i webbläsaren. Fungerar på iPhone via Safari.
> Ingen installation krävs — öppna bara länken.

![Plattform](https://img.shields.io/badge/Plattform-iOS%20%7C%20Android%20%7C%20Desktop-blue?style=flat-square)
![Modell](https://img.shields.io/badge/Modell-face--api.js-green?style=flat-square)
![Hosting](https://img.shields.io/badge/Hosting-GitHub%20Pages-black?style=flat-square)
![Licens](https://img.shields.io/badge/Licens-MIT-yellow?style=flat-square)

---

## ✨ Funktioner

- 🔲 **Realtidsdetektering** — färgade boxar runt varje ansikte
- 👤 **Unika ID:n** — Person 1, Person 2 osv. automatiskt
- 👥 **Flera ansikten** — hanterar multipla ansikten samtidigt
- 📸 **Bildgalleri** — sparar foton per person, klicka för att se alla
- 📱 **iPhone-optimerad** — fungerar i Safari utan app-installation
- 🔒 **100% lokalt** — all data stannar i webbläsaren, inget skickas online

---

## 🚀 Lägg upp på GitHub Pages (steg för steg)

### 1. Skapa ett nytt repo på GitHub
Gå till [github.com/new](https://github.com/new) och skapa ett repo, t.ex. `facetracker`

### 2. Ladda upp filen
```bash
git init
git add index.html
git commit -m "Initial commit"
git remote add origin https://github.com/DITT-NAMN/facetracker.git
git push -u origin main
```

### 3. Aktivera GitHub Pages
1. Gå till repot på GitHub
2. Klicka på **Settings** → **Pages**
3. Under *Source*: välj `main` branch, mapp `/ (root)`
4. Klicka **Save**

### 4. Öppna på iPhone
Efter ~1 minut får du en länk:
```
https://DITT-NAMN.github.io/facetracker
```
Öppna denna i **Safari på iPhone** → tryck "Starta" → tillåt kameråtkomst.

> **Tips:** Lägg till sidan på hemskärmen via Safari → dela-knappen → "Lägg till på hemskärmen" för en app-liknande upplevelse!

---

## 🔬 Hur det fungerar

Appen använder **face-api.js** med tre förtränade modeller:

| Modell | Storlek | Syfte |
|---|---|---|
| `tinyFaceDetector` | ~190 KB | Hittar ansikten i bilden |
| `faceLandmark68TinyNet` | ~80 KB | 68 ansiktspunkter |
| `faceRecognitionNet` | ~6.2 MB | 128-dim encoding per ansikte |

Varje ansikte omvandlas till en 128-siffrig vektor. Euklidiskt avstånd < 0.5 = samma person.
Nya personer måste synas 3 frames i rad innan de bekräftas (minskar falska ID:n).

---

## ⚙️ Konfigurera i koden

Ändra dessa konstanter i `index.html`:

| Konstant | Standard | Förklaring |
|---|---|---|
| `MATCH_THRESHOLD` | `0.5` | Lägre = striktare matchning |
| `CONFIRM_FRAMES` | `3` | Frames innan ny person |
| `CAPTURE_INTERVAL` | `3000` | ms mellan sparade foton |
| `DETECT_INTERVAL` | `200` | ms mellan detekteringar |
| `MAX_PHOTOS` | `30` | Max foton per person |

---

## 🔒 Integritet

- All bearbetning sker **lokalt i webbläsaren**
- Inga bilder eller data skickas till någon server
- Sparade foton försvinner när sidan stängs/laddas om
- Modellerna laddas från ett publikt CDN (jsdelivr.net)

---

## 🛠 Felsökning

| Problem | Lösning |
|---|---|
| Kameran startar inte på iPhone | Öppna i **Safari** (inte Chrome/Firefox) |
| "Kunde inte ladda modellen" | Kontrollera internetanslutning, ladda om |
| Samma person får flera ID:n | Sänk `MATCH_THRESHOLD` till `0.45` |
| För många falska nya personer | Höj `CONFIRM_FRAMES` till `5` |
| Appen är långsam | Öka `DETECT_INTERVAL` till `400` |

---

*Skolprojekt — data lagras temporärt enbart i webbläsarens minne och försvinner vid omladdning.*
