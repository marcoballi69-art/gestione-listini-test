GESTIONE LISTINI 2.0 — PACCHETTO DI LAVORO AGGIORNATO

CONTENUTO
- index.html
- app.js
- sw.js
- README.txt
- manifest.webmanifest

MODIFICHE INCLUSE IN QUESTA REVISIONE
- Interfaccia riordinata per iniziare dalla scelta del cliente, con percorso guidato.
- Pulsanti e campi più grandi, finestra scanner più contenuta.
- Selezione numerata automaticamente in sequenza annuale (es. 1/2026).
- Ricerca archivio per nome cliente o numero selezione.
- Eliminazione della selezione completa con conferma; il progressivo eliminato non viene riutilizzato.
- Dopo il salvataggio, la schermata viene azzerata per inserire un nuovo cliente.
- Opzione per includere/escludere i prezzi in PDF ed email.
- PDF semplice con titolo "SELEZIONE N.", senza codice articolo e senza intestazioni/condizioni commerciali.
- Note del singolo articolo riportate nel PDF e nel testo dell'email.
- Email senza codici articolo.
- Anteprima PDF dentro l'app, con comando per tornare all'app e comando stampa/salvataggio.
- Interfaccia inglese per le etichette e le voci principali.
- Backup JSON conserva anche il contatore delle selezioni.
- Cache offline aggiornata.

SCANNER
- Usa BarcodeDetector quando disponibile e decoder locale EAN-8/EAN-13 come alternativa.
- Richiede la fotocamera posteriore quando disponibile e tenta autofocus/zoom se il dispositivo espone i relativi controlli.
- Il decoder campiona più righe e media più pixel per ridurre il rumore.
- NON è stato possibile eseguire una prova reale con la fotocamera di iPhone in questa sessione. La lettura su iPhone deve essere verificata sul dispositivo prima di considerare concluso il lavoro.

PDF E CONDIVISIONE SU IPHONE
- Il PDF viene mostrato in un'anteprima interna all'app.
- Il pulsante "Condividi / Salva PDF" apre la finestra di stampa del browser. Su iPhone, dalla schermata di stampa si usa il comando di condivisione/salvataggio di iOS.
- Il comando email prepara il testo dell'email, includendo le note articolo e applicando l'opzione prezzi. L'allegato PDF va condiviso dalla schermata di stampa.

DATI E COMPATIBILITÀ
- Il database locale mantiene lo stesso nome e la stessa versione IndexedDB del pacchetto precedente per conservare la compatibilità con i dati già presenti sul dispositivo.
- Prima di aggiornare un dispositivo con dati importanti, è consigliato esportare un backup JSON.
- Il pacchetto non cancella intenzionalmente gli archivi locali già presenti.
- Il servizio offline mantiene in cache la pagina e gli script dell'app.
- Le librerie di importazione PDF/Excel sono esterne e vengono memorizzate in cache quando possibile; la prima importazione può richiedere una connessione.

VERIFICHE E LIMITI
- Sintassi JavaScript verificata con Node.js.
- Collegamenti tra gli ID HTML e quelli richiamati dal codice controllati.
- Non è stato eseguito un test end-to-end in Safari/iPhone.
- Non è stato verificato il flusso reale di stampa/condivisione PDF su iPhone.
- Non dichiarare lo scanner verificato finché non viene provato su iPhone.


REVISIONE SCANNER OFFLINE v5
- Avvio della richiesta fotocamera immediatamente al tocco del pulsante, senza attendere altre operazioni asincrone.
- Richiesta della fotocamera posteriore con vincoli minimi, più compatibili con Safari su iPhone.
- Attesa del video pronto prima di avviare la scansione.
- Attributi playsinline e webkit-playsinline per mantenere la fotocamera nella pagina su iOS.
- Decoder EAN locale prioritario e indipendente dalla rete; BarcodeDetector è soltanto un ripiego opzionale.
- Mantenuta la decodifica EAN-8 ed EAN-13 con verifica della cifra di controllo.
- Conservati gli zeri iniziali dei codici EAN durante il confronto con l'archivio.
- Aggiornata la cache offline alla versione gestione-listini-v7 e il riferimento del service worker.
- Migliorata la gestione degli errori e la pulizia della fotocamera quando l'avvio non riesce.

VERIFICHE E LIMITI
Il decoder locale è stato provato con immagini sintetiche EAN-8 (96385074) ed EAN-13 (4006381333931), entrambe decodificate correttamente.
Il codice scanner non richiede servizi o librerie di decodifica esterne.
La lettura ottica reale e il comportamento della fotocamera devono comunque essere confermati su iPhone fisico; l'accesso alla fotocamera richiede HTTPS e il permesso del browser.
\n\nREVISIONE SCANNER OFFLINE v8\n- Decoder EAN locale: scansione su più righe dell’immagine e con soglie di contrasto alternative.\n- Video scanner più compatto e centrato su schermi iPhone.\n- Richiesta video con risoluzione ideale maggiore, senza vincoli rigidi.\n- Nessuna libreria o richiesta di rete necessaria per la decodifica EAN-8/EAN-13.\n
REVISIONE SCANNER v10
- Rafforzato il decoder EAN locale con ricerca su più righe dell'immagine,
  soglie multiple e tolleranza a piccoli errori di scala/allineamento.
- Verificata la decodifica sintetica dei codici EAN-13 4006381333931
  ed EAN-8 96385074.
- Ridotta la dimensione del riquadro video per schermi iPhone.
- Cache offline aggiornata a gestione-listini-v10.
Nota: i test sintetici non sostituiscono la prova con fotocamera reale.


REVISIONE COLLEGAMENTO SCANNER DEDICATO v12
- Integrata la cartella scanner fornita (scanner/index.html e html5-qrcode.min.js).
- Aggiunto il pulsante "Apri scanner dedicato" nell'app Gestione Listini.
- Collegamento popup tramite i messaggi GESTIONE_LISTINI_BARCODE,
  GESTIONE_LISTINI_SCAN_RESULT e GESTIONE_LISTINI_SCAN_FINISH.
- Il codice letto viene cercato nell'archivio locale; se presente viene aggiunto
  alla scelta secondo le regole già esistenti, se non presente viene proposta
  l'inserzione manuale.
- Lo scanner dedicato e la libreria sono inclusi nella cache del service worker
  per l'uso offline dopo il primo caricamento completo online.
- Mantenuto anche lo scanner integrato già presente nell'app come alternativa.

VERIFICHE E LIMITI DELLA REVISIONE v12
- Controllata la sintassi JavaScript dell'app, del service worker e dello scanner.
- Controllati i riferimenti agli elementi HTML richiamati dall'app.
- Non eseguito test reale con fotocamera fisica iPhone: permessi, apertura popup
  e decodifica ottica devono essere confermati sul dispositivo.

REVISIONE SCANNER v13
- Unificato l'avvio in un solo pulsante nell'app.
- Il pulsante usa direttamente html5-qrcode, caricato dalla cartella locale ./scanner/:
  non apre popup e non dipende da una CDN per la decodifica dei codici.
- La lettura gestisce EAN-13, EAN-8, UPC-A, UPC-E, Code 128, Code 39 e ITF.
- La libreria locale è inclusa nella cache del service worker per l'uso offline,
  dopo la prima apertura online e il completamento della cache.
- Rimane necessario verificare la lettura ottica su iPhone fisico; la sintassi
  e i collegamenti locali sono stati controllati, ma non equivalgono a una prova
  reale della fotocamera.


REVISIONE v15 — SCANNER E LISTINO PDF PERSISTENTE
- Scanner configurato per analizzare l'intero fotogramma (nessuna piccola area qrbox),
  con fotocamera posteriore preferita e risoluzione ideale 1920x1080.
- Disabilitato il BarcodeDetector nativo sperimentale: viene usato il decoder ZXing
  incluso nella libreria locale html5-qrcode, per mantenere la decodifica EAN coerente.
- Area video ampliata per facilitare la messa a fuoco dei codici a barre lineari.
- Ricerca compatibile anche con UPC-A a 12 cifre e corrispondente EAN-13 con zero iniziale.
- Dopo la scansione il nome dell'articolo viene mostrato anche se prima occorre selezionare
  il cliente; in tal caso l'articolo non viene aggiunto finché il cliente non è selezionato.
- Dopo l'importazione PDF restano visibili nome file e righe dell'anteprima; il riquadro
  viene salvato in IndexedDB e ripristinato alla successiva apertura dell'app.
- Versione cache service worker aggiornata a v15 per evitare di riutilizzare gli asset v13.

VERIFICHE v15
- Controllata la sintassi JavaScript con Node.js e l'integrità dello ZIP.
- Controllati gli ID HTML usati dallo script e i collegamenti alla libreria scanner locale.
- La documentazione ufficiale html5-qrcode conferma il supporto iOS Safari (iOS >= 15.1)
  e i formati EAN-13/EAN-8/UPC-A/UPC-E.
- Non è possibile certificare la lettura ottica reale senza prova su iPhone fisico.
