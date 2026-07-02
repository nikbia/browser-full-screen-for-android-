# UI24R Browser full screen

App Android minimale che apre a schermo intero, senza barra degli indirizzi e senza pulsanti,
la pagina web all'indirizzo `http://192.168.1.10`.

## Caratteristiche
- Nessuna barra degli indirizzi, nessun pulsante, nessuna action bar
- Modalità immersiva: nasconde anche la barra di stato e i tasti di navigazione Android
- Se il dispositivo all'IP indicato non è raggiungibile, riprova automaticamente ogni 3 secondi
- Il tasto "indietro" ricarica la pagina invece di chiudere l'app (utile per un vero utilizzo "kiosk")
- Permette traffico HTTP (non HTTPS) verso l'IP 192.168.1.10, che di solito è quello usato per i dispositivi in rete locale


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
