## Challenge di Architettura Cloud - Sistema di Indicizzazione di documenti aziendali

## Scenario:

Un'azienda di revisione contabile ha accumulato nel corso degli anni una vasta quantità di documenti
di società esterne, tra cui bilanci, relazioni, dossier, analisi finanziarie e ogni altro tipo di documento pertinente.

Un team dell'azienda è responsabile del caricamento dei documenti tramite un'interfaccia web personalizzata, mentre un
secondo team svolge operazioni di analisi sui documenti precedentemente caricati.

In un secondo momento, per questioni di ottimizzazione del business, sorge la necessità di ottimizzare il workflow del
team di analisi poiché esso riscontra difficoltà nel fruire i documenti pertinenti a causa del loro incremento
considerevole.

## Requisiti:

1. Progetta un'infrastruttura cloud che consenta l'indicizzazione event-driven e la ricerca fulltext di questi
   documenti.

2. L'infrastruttura deve essere altamente scalabile per gestire una crescita costante del numero di documenti. Deve
   essere in grado di gestire documenti in formati comuni come doc, docx, pdf e xls.

3. Il servizio di ricerca sarà utilizzato intensivamente solo in periodi specifici dell'anno (stagionalità). In altri
   momenti, sarà pressoché inutilizzato, comportando uno spreco di budget. L'infrastruttura deve essere in grado di
   adattarsi a picchi di utilizzo stagionali.

4. Per ogni utente che effettua ricerche, è necessario mantenere una cronologia delle ricerche che risale al massimo a
   30 giorni. Trascorsi 30 giorni, la cronologia delle ricerche deve essere automaticamente eliminata.

5. Deve essere considerata un'infrastruttura cloud agnostica, consentendo al candidato di scegliere autonomamente i
   servizi e le tecnologie da utilizzare, giustificando le scelte effettuate.

6. Deve essere inclusa una breve descrizione dell'architettura proposta, con particolare attenzione a come i vari
   servizi saranno integrati per fornire una soluzione completa.

## Nota:

Il candidato non è tenuto a implementare fisicamente l'infrastruttura o il codice effettivo. La sfida si concentra
sull'architettura e sulla selezione dei servizi e delle tecnologie più adatti per soddisfare i requisiti suindicati.
