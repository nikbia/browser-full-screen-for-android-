# Kiosk Browser

App Android minimale che apre a schermo intero, senza barra degli indirizzi e senza pulsanti,
la pagina web all'indirizzo `http://192.168.1.10`.

## Caratteristiche
- Nessuna barra degli indirizzi, nessun pulsante, nessuna action bar
- Modalità immersiva: nasconde anche la barra di stato e i tasti di navigazione Android
- Se il dispositivo all'IP indicato non è raggiungibile, riprova automaticamente ogni 3 secondi
- Il tasto "indietro" ricarica la pagina invece di chiudere l'app (utile per un vero utilizzo "kiosk")
- Permette traffico HTTP (non HTTPS) verso l'IP 192.168.1.10, che di solito è quello usato per i dispositivi in rete locale

## Come ottenere l'APK senza installare nulla (consigliato)
Questo progetto include già un workflow di GitHub Actions che compila l'APK automaticamente.

1. Crea un account gratuito su [github.com](https://github.com) se non ne hai già uno.
2. Crea un nuovo repository (può essere privato), es. "kiosk-browser".
3. Carica tutti i file di questa cartella nel repository (dalla pagina del repo puoi trascinare i file,
   oppure usa git da riga di comando: `git init`, `git add .`, `git commit -m "primo commit"`,
   `git remote add origin <url-del-tuo-repo>`, `git push -u origin main`).
4. Vai nella scheda "Actions" del repository su GitHub: partirà automaticamente la compilazione
   (workflow "Build APK"). Attendi 2-3 minuti.
5. Al termine, apri l'esecuzione completata (segno verde ✓) e in fondo alla pagina trovi la sezione
   "Artifacts" con un file chiamato `KioskBrowser-debug-apk`: scaricalo, dentro c'è `app-debug.apk`.
6. Trasferisci `app-debug.apk` sul tablet (email, chiavetta, cavo, Google Drive, ecc.) e aprilo per
   installarlo. Dovrai autorizzare l'installazione da "origini sconosciute" nelle impostazioni del tablet
   quando richiesto.

## Come compilarla con Android Studio (alternativa)
1. Installa [Android Studio](https://developer.android.com/studio) (gratuito).
2. Apri Android Studio → "Open" → seleziona la cartella `KioskBrowser` di questo progetto.
3. Lascia che Gradle sincronizzi le dipendenze (la prima volta scarica alcuni pacchetti, serve internet).
4. Collega il tablet via USB (con il debug USB attivo) oppure usa un emulatore, poi premi "Run ▶".
5. In alternativa, da menu Build → "Build Bundle(s) / APK(s)" → "Build APK(s)" per generare un file .apk da installare manualmente.

## Se l'indirizzo cambia
Apri il file:
```
app/src/main/java/com/example/kioskbrowser/MainActivity.kt
```
e modifica questa riga in cima al file:
```kotlin
private const val TARGET_URL = "http://192.168.1.10"
```

Se in futuro l'indirizzo dovesse diventare HTTPS con un certificato valido, non serve modificare nulla
di particolare; se invece l'IP cambia, aggiorna anche il file:
```
app/src/main/res/xml/network_security_config.xml
```
sostituendo `192.168.1.10` con il nuovo indirizzo, altrimenti il traffico HTTP verso il nuovo indirizzo
verrebbe bloccato da Android per motivi di sicurezza.

## Nota
Questa app richiede che il telefono sia sulla stessa rete locale (Wi-Fi) del dispositivo con indirizzo
192.168.1.10, altrimenti la pagina non sarà raggiungibile.
