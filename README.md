# Text and Object Detenction with Subsequent Explanation

Creazione di un modello di rete neurale **CRNN** (composto da **CNN** (**Convolutional Neural Networks**) + **RNN** (**Recurrent Neural Networks**)).

Obiettivo del modello è: **data una o più immagini di input**, il modello deve prevedere:
1. **Se le immagini contengono del testo**. Se il modello viene sviluppato sotto forma di app, si potrebbe inserire un bottone per abilitare l'identificazione di oggetti, o se solo in una delle due, e l'altra per fornire contesto.
   a) **In caso di risposta affermativa**, **deve prevedere il testo rappresentato nell'immagine**.
   b) **In caso di risposta negativa**, deve poter affermare che l'immagine non contiene del testo. In più, **deve poter chiedere all'utente se si vuole riconoscere gli oggetti nell'immagine (Object Detenction)**.
   c) In entrambe i casi, sia di immagine senza testo che con, **tramite un prompt si può comunicare con il modello nel seguente modo**: deve apparire un messaggio per l'utente **che richieda se si vuole fornire ulteriori informazioni per poter richiedere qualcosa**, ovvero che **dia un contesto all'immagine**: l'utente spiega dove ha scattato l'/le immagine/i, o dove l'/le ha recuperata/e (esempio: un cartello in prossimità di una scuola, o un divieto di sosta) e il modello deve saper spiegare **il contesto dell'oggetto o del testo nell'/nelle immagine/i**.

Esempio 1: l'utente scatta una foto ad un cartello triangolare bianco dipinto sulla strada rappresentante i bambini che vanno a scuola (immagine 1), con successivo cartello rosso circolare 10km (immagine 2). Nel prompt, l'utente spiega "Mi trovo in prossimità di una scuola. Perchè c'è questo cartello segnaletico?". Il modello deve restituire all'utente: "I cartelli, insieme, vogliono esprimere agli automobilisti la necessità di mantenere una velocità bassa, perchè in prossimità si trova una scuola. Perciò i bambini o i ragazzi potrebbero sbucar fuori dalla strada all'improvviso. Se il guidatore va forte, potrebbe investirli".

Esempio 2: l'utente scatta una foto a Rapallo, in Liguria, dove si ha parcheggiato in un parcheggio bianco, quindi non a pagamento e non adibito ai residenti (immagine 1). In prossimità del parcheggio proprio, si trova un cartello con indicata rimozione del mezzo, e divieto di sosta (immagine 2). L'utente vuole sapere se può lasciare la macchina in quel parcheggio, oppure se deve spostarla perchè magari è ignaro di qualche 
