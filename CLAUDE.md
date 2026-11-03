# numeri-whatsapp

Pagina interna di Salone Vincente per collegare i **numeri WhatsApp NOSTRI** (hiring e
altri) all'app Meta «Agenda Salone Vincente» `1025459190200664`, la stessa di ANIMA, ma
**fuori da ANIMA**: questi numeri non sono centri e non hanno la receptionist.

- Live: https://mach10account.github.io/numeri-whatsapp/ (GitHub Pages da `main`, pubblica:
  qui non va MAI un segreto). Il dominio `mach10account.github.io` è già tra quelli dell'app
  Meta, per questo il bottone sta qui e non su manager.mach10holding.com.
- Accesso: chiave in `~/.segreti/numeri-whatsapp.txt` (nella funzione c'è solo l'hash).
- Backend: edge function **`wa-interni`** sul progetto SV Platform `hypkwdvvrmakqrowbkqw`,
  sorgente in `wa-receptionist/supabase/functions/wa-interni/`, tabelle `wa.numeri_interni`
  e `wa.interni_messaggi` (`wa-receptionist/sql/018_numeri_interni.sql`).
- Il bottone fa l'Embedded Signup (config `1586007669939026`); al collegamento la WABA
  viene iscritta con `override_callback_uri` = `wa-interni`, così le risposte non passano da
  `wa-inbound` (la receptionist dei centri).

## Come la usano i workflow n8n

`POST https://hypkwdvvrmakqrowbkqw.supabase.co/functions/v1/wa-interni`

```json
{ "chiave": "…", "azione": "invia", "numero": "hiring", "a": "+39…",
  "template": { "nome": "candidatura_setter", "lingua": "it", "parametri": ["Mario"] } }
```

Altre azioni: `template` (elenco e stato), `crea_template`, `inoltro` (webhook n8n che
riceve le risposte), `conversazione`, `elenco`, `config`.
