# 📱 FaceTracker — MediaPipe + GitHub Pages

> Realtids ansiktsigenkänning i webbläsaren med Google MediaPipe.  
> Fungerar direkt i Safari på iPhone — ingen app-installation.

![iOS](https://img.shields.io/badge/iOS-Safari%2015%2B-black?style=flat-square&logo=safari)
![MediaPipe](https://img.shields.io/badge/MediaPipe-Face%20Mesh-blue?style=flat-square)
![GitHub Pages](https://img.shields.io/badge/Hosting-GitHub%20Pages-222?style=flat-square&logo=github)

---

## ✨ Vad den gör

| Funktion | Detalj |
|---|---|
| 🔲 Realtidsdetektering | Hörn-boxar runt varje ansikte, ~30 fps |
| 👤 Unika ID:n | Person 1, Person 2... — automatiskt per session |
| 👥 Flera ansikten | Upp till 6 ansikten i bild samtidigt |
| 📸 Automatiska foton | Sparas var 2.5:e sekund per person |
| 📂 Bildgalleri | Klicka på en person → se alla sparade foton |
| 🔒 Helt lokalt | Inget skickas till internet |

---

## 🚀 Lägg upp på GitHub Pages

### Steg 1 — Skapa repo
Gå till **github.com/new** och skapa ett nytt repo, t.ex. `facetracker`

### Steg 2 — Ladda upp filen
Klicka **Add file → Upload files** och dra in `index.html`

### Steg 3 — Aktivera GitHub Pages
```
Settings → Pages → Source: Deploy from branch
Branch: main   /   Folder: / (root)
→ Save
```

### Steg 4 — Öppna på iPhone
```
https://DITT-NAMN.github.io/facetracker
```
Öppna i **Safari** → tryck **Starta** → tillåt kameråtkomst

> 💡 Lägg till på hemskärmen:  
> Safari → Dela-knapp → "Lägg till på hemskärmen" → app-ikon!

---

## ⚙️ Konfigurera

Ändra konstanterna i `CFG`-objektet i `index.html`:

| Konstant | Standard | Förklaring |
|---|---|---|
| `CAPTURE_INTERVAL` | `2500` ms | Tid mellan sparade foton |
| `MATCH_THRESHOLD` | `18` | Lägre = striktare matchning |
| `CONFIRM_FRAMES` | `4` | Frames för att bekräfta ny person |
| `MAX_PHOTOS` | `40` | Max foton per person |
| `PHOTO_SIZE` | `128` px | Storlek på sparade thumbnails |

---

## 🔬 Hur igenkänningen fungerar

```
MediaPipe FaceMesh
    → 468 landmarks per ansikte
    → 20 nyckellandmarks väljs ut
    → Normaliseras mot ansiktets mittpunkt + storlek
    → 40-dimensionell descriptor skapas

Ny descriptor jämförs mot alla kända:
    → Euklidiskt avstånd < 18  →  samma person
    → Annars buffras i "pending" i 4 frames
    → Om samma ansikte ses 4 gånger → ny bekräftad person

Descriptor uppdateras löpande (glidande medelvärde)
för att hantera rörelse, ljusförändringar etc.
```

---

## 🛠 Felsökning iPhone

| Problem | Lösning |
|---|---|
| Kameran startar inte | Öppna i **Safari** (inte Chrome/Firefox) |
| "Tillåt kamera" syns inte | Inställningar → Safari → Kamera → Tillåt |
| Appen är långsam | Stäng andra appar, ladda om Safari |
| Samma person får nytt ID | Sänk `MATCH_THRESHOLD` till `14` |
| För många falska nya | Höj `CONFIRM_FRAMES` till `6` |
| Modellen laddar inte | Kontrollera wifi, ladda om sidan |

---

## 🔒 Integritet

- All bearbetning sker lokalt i webbläsarens minne
- Foton försvinner när sidan stängs eller laddas om  
- Inga bilder, descriptors eller persondata skickas någonstans
- Modellfilerna laddas från `cdn.jsdelivr.net` (Googles MediaPipe)

---

*Skolprojekt — temporär lokal data, inget lagras permanent.*
