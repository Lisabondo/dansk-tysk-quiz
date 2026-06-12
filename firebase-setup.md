# Firebase opsætning — delt kalender

Dette er en **engangssætning** på ca. 10 minutter. Når det er gjort, deler I og din kærestes kalender og fremskridt automatisk i realtid.

---

## Trin 1 — Opret Firebase-projekt

1. Gå til [console.firebase.google.com](https://console.firebase.google.com)
2. Log ind med din Google-konto
3. Klik **"Add project"** (eller **"Tilføj projekt"**)
4. Giv det et navn, f.eks. `dansk-tysk-quiz`
5. Slå Google Analytics **fra** (ikke nødvendigt) → klik **"Create project"**
6. Vent til projektet er oprettet → klik **"Continue"**

---

## Trin 2 — Aktivér Realtime Database

1. I venstre menu: klik **"Build"** → **"Realtime Database"**
2. Klik **"Create Database"**
3. Vælg region: **"Europe (belgium)"** (nærmest Danmark)
4. Vælg **"Start in test mode"** → klik **"Enable"**

---

## Trin 3 — Hent din config

1. Klik på **tandhjulet** ⚙️ øverst til venstre → **"Project settings"**
2. Scroll ned til **"Your apps"**
3. Klik på **web-ikonet** `</>`
4. Giv appen et navn (f.eks. `quiz`) → klik **"Register app"**
5. Du ser nu en kodeblok der ligner dette:

```javascript
const firebaseConfig = {
  apiKey: "AIzaSy...",
  authDomain: "dansk-tysk-quiz.firebaseapp.com",
  databaseURL: "https://dansk-tysk-quiz-default-rtdb.europe-west1.firebasedatabase.app",
  projectId: "dansk-tysk-quiz",
  storageBucket: "dansk-tysk-quiz.appspot.com",
  messagingSenderId: "123456789",
  appId: "1:123456789:web:abc123"
};
```

Kopier denne blok (alle 8 linjer inde i `{}`).

---

## Trin 4 — Indsæt config i HTML-filen

1. Åbn `dansk-tysk-quiz.html` i en teksteditor (f.eks. Notepad, TextEdit, VS Code)
2. Find denne sektion øverst i JavaScript-koden (ca. linje 3 i `<script>`):

```javascript
const FIREBASE_CONFIG = {
  apiKey: "PASTE_YOUR_API_KEY",
  authDomain: "PASTE_YOUR_PROJECT_ID.firebaseapp.com",
  databaseURL: "https://PASTE_YOUR_PROJECT_ID-default-rtdb.europe-west1.firebasedatabase.app",
  ...
};
```

3. Erstat de 7 linjer med dine egne værdier fra trin 3
4. Gem filen

---

## Trin 5 — Upload til GitHub Pages

1. Omdøb filen til `index.html`
2. Gå til dit GitHub-repo
3. Upload filen (erstat den gamle)
4. GitHub Pages opdaterer automatisk inden for ~1 minut

---

## Trin 6 — Første gang på begge telefoner

1. Åbn appen på **begge** telefoner
2. I "Forbind jer"-skærmen: skriv **den samme kode** på begge (f.eks. `lisa-og-mads`)
3. Koden er jeres delte nøgle til Firebase-databasen

✅ Nu synkroniserer jeres kalender automatisk — når én spiller færdig, ser den anden det med det samme!

---

## Sikkerhed

Firebase er sat op i "test mode" — det betyder at alle med jeres couple-kode kan læse/skrive jeres data. Da koden er privat og svær at gætte, er det fint for en personlig app. Vil du låse det mere ned, kan du opdatere "Rules" i Firebase Realtime Database til:

```json
{
  "rules": {
    "couples": {
      "$code": {
        ".read": true,
        ".write": true
      }
    }
  }
}
```

---

## Pris

Firebase Realtime Database er **gratis** op til 1 GB lagring og 10 GB/måned datatrafik. En quiz-kalender bruger < 1 MB total. I kommer aldrig i nærheden af grænsen.
