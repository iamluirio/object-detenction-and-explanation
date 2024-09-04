# Text and Object Detenction with Subsequent Explanation

Creazione di un modello di rete neurale **CRNN** (composto da **CNN** (**Convolutional Neural Networks**) + **RNN** (**Recurrent Neural Networks**)).

Obiettivo del modello è: **data una o più immagini di input**, il modello deve prevedere:
1. **Se le immagini contengono del testo**. Se il modello viene sviluppato sotto forma di app, si potrebbe inserire un bottone per abilitare l'identificazione di oggetti, o se solo in una delle due, e l'altra per fornire contesto.
   - **In caso di risposta affermativa**, **deve prevedere il testo rappresentato nell'immagine**.
   - **In caso di risposta negativa**, deve poter affermare che l'immagine non contiene del testo. In più, **deve poter chiedere all'utente se si vuole riconoscere gli oggetti nell'immagine (Object Detenction)**.
   - In entrambe i casi, sia di immagine senza testo che con, **tramite un prompt si può comunicare con il modello nel seguente modo**: deve apparire un messaggio per l'utente **che richieda se si vuole fornire ulteriori informazioni per poter richiedere qualcosa**, ovvero che **dia un contesto all'immagine**: l'utente spiega dove ha scattato l'/le immagine/i, o dove l'/le ha recuperata/e (esempio: un cartello in prossimità di una scuola, o un divieto di sosta) e il modello deve saper spiegare **il contesto dell'oggetto o del testo nell'/nelle immagine/i**.

Esempio 1: l'utente scatta una foto ad un cartello triangolare bianco dipinto sulla strada rappresentante i bambini che vanno a scuola (immagine 1), con successivo cartello rosso circolare 10km (immagine 2). Nel prompt, l'utente spiega "Mi trovo in prossimità di una scuola. Perchè c'è questo cartello segnaletico?". Il modello deve restituire all'utente: "I cartelli, insieme, vogliono esprimere agli automobilisti la necessità di mantenere una velocità bassa, perchè in prossimità si trova una scuola. Perciò i bambini o i ragazzi potrebbero sbucar fuori dalla strada all'improvviso. Se il guidatore va forte, potrebbe investirli".

Esempio 2: l'utente scatta una foto a Rapallo, in Liguria, dove si ha parcheggiato in un parcheggio bianco, quindi non a pagamento e non adibito ai residenti (immagine 1). In prossimità del parcheggio proprio, si trova un cartello con indicata rimozione del mezzo, e divieto di sosta (immagine 2). L'utente vuole sapere se può lasciare la macchina in quel parcheggio, oppure se deve spostarla perchè magari è ignaro di qualche regola impostata dal comune che impone qualche vincolo particolare. Tramite prompt, l'utente, dopo aver inserito le immagini, digita: "Mi trovo nel comune di Rapallo, in Liguria (Italia). Posso lasciare la macchina qui, oppure prenderò la multa/mi verrà rimosso il veicolo?". Il modello deve poter rispondere: "Si/No" dopo essersi informato sulle regole e sulle leggi del comune di Rapallo. Se non sono presenti leggi particolari per quel comune, cercherà nel regolamento stradale italiano, e in base alla combinazione dei due cartelli, risponderà in modo affermativo piuttosto che negativo.

## CRNN
Una **CRNN (Convolutional Recurrent Neural Network)** è un tipo di rete neurale artificiale che combina **due tipi di reti neurali**: **le reti neurali convoluzionali (CNN) e le reti neurali ricorrenti (RNN)**. Questo tipo di architettura viene utilizzato principalmente **per elaborare dati sequenziali o strutturati come immagini, video, testo o segnali audio**.

- La parte convoluzionale della CRNN viene utilizzata per estrarre caratteristiche spaziali dai dati, come avviene nelle immagini. Le CNN sono molto efficaci nell'identificare pattern locali all'interno di dati con struttura spaziale (ad esempio, le immagini).
- Dopo la parte convoluzionale, le caratteristiche estratte vengono passate alla parte ricorrente della rete, tipicamente una RNN o una variante come LSTM (Long Short-Term Memory) o GRU (Gated Recurrent Unit). Le RNN sono ideali per catturare le dipendenze temporali o sequenziali nei dati, come il contesto temporale in un video o la sequenza di parole in una frase.

![image](https://github.com/user-attachments/assets/91c5f430-2b2b-4704-9500-255eda5c13f3)

## Architettura del Modello ad Alto Livello 
Per progettare un modello di rete neurale CRNN che possa soddisfare i requisiti descritti, è necessario suddividere l'architettura in due blocchi principali.

#### Blocco di Classificazione Testo/Non Testo
Questo blocco **determina se l'immagine contiene testo o meno**. Utilizza una rete **CNN** per estrarre caratteristiche e classificare l'immagine. **Strato di Classificazione**: **un livello di classificazione completamente connesso (fully connected) che fornisce un output binario: "Testo" o "Non Testo".** Utilizza funzioni di attivazione come Softmax o Sigmoid per produrre la probabilità che l'immagine contenga testo.

### Blocco di Riconoscimento del Testo (CRNN)
Questo blocco è **responsabile del riconoscimento del testo nell'immagine**.

- **Parte Convoluzionale (CNN)**: utilizza strati convoluzionali per estrarre caratteristiche spaziali dall'immagine.
- **Parte Ricorrente (RNN)**: questa parte serve a "leggere" il testo estratto dalla parte convoluzionale e trasformarlo in una sequenza di caratteri.

#### Riconoscimento Oggetti (Object Detection)
Se l'immagine è classificata come "Non Testo", **implementa un meccanismo per chiedere all'utente se desidera riconoscere gli oggetti presenti nell'immagine**.
