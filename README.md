<H1 align="center">The Last of Events</H1>
<H2 align="center">an OOP-Java project made with Spring</H2>
<H4 align="center">Repository progetto programmazione OO febbraio 2021</H4>

## Sommario:
- [Introduzione](#introduzione)
- [Installazione](#installazione)
- [Configurazione API Ticketmaster](#configurazione-api-ticketmaster)
- [UML](#uml)
  - [Use Case Diagram](#use-Case-diagram)
  - [Class Diagram](#class-diagram)
  - [Sequence Diagram](#sequence-diagram)
  - [Sequence Diagram Rotta “/eventi”](#sequence-diagram-rotta-eventi)
- [Rotte](#rotte)
  - [Filtri e Stats Richiesti](#filtri-e-stats-richiesti)
  - [Filtri e Stats aggiuntivi](#filtri-e-stats-aggiuntivi)
- [Test](#test)
- [Documentazione](#documentazione)
- [Software Utilizzati](#spftware-utilizzati)
- [Autori](#autori)
 
## Introduzione
Il tema principale, da cui origina l’applicazione ivi presentata, descritta e documentata, è quello di realizzare una Filter-App dell’applicativo Ticketmaster, un noto software dedito alla gestione ed alla prenotazione di eventi musicali, teatrali, cinematografici ed artistici, reperibile presso l’indirizzo https://www.ticketmaster.it/.
In particolare, attraverso le API derivate dalla pagina TM Developer, accessibili mediante l’indirizzo Discovery API - The Ticketmaster Developer Portal, il programma dovrà valutare esclusivamente gli eventi siti in Australia ed in  Nuova Zelanda, al fine di cercare gli eventi relativi ad ogni Stato e di produrre statistiche, che possono essere di Default o Personalizzate, in base ai risultati ottenuti dalla ricerca.
Continuando, dal punto di vista delle specifiche tecniche, il Web Service proposto offre le seguenti funzionalità:
* filtraggio degli eventi, previsti in Australia e/o Nuova Zelanda, attraverso la selezione di  uno o più Stati, a cui segue la produzione di statistiche relative allo Stato o agli Stati scelti.
* filtraggio degli eventi, previsti in Australia e/o Nuova Zelanda, attraverso la selezione di uno o più generi, a cui segue la produzione di statistiche relative al genere o ai generi scelti.
* funzione di filtraggio avanzata degli eventi, che prevede l’introduzione di una sottostringa contenuta nel nome degli Stati come, ad esempio, A*, e che fornisce un suggerimento circa i possibili Stati da inserire.
* funzione di filtraggio avanzata delle statistiche, che prevede l’introduzione di un periodo ti tempo personalizzato, costituito da una data iniziale e da una data finale, entrambe nel formato yyyy-mm-dd, su cui effettuare il calcolo delle statistiche relative ad uno o più Stati selezionati.
In particolare, una volta scelto il periodo personalizzato, esso verrà ripetuto tante volte quanto è contenuto in un anno a partire dalla data iniziale scelta;
ad esempio, se il periodo è di 182 giorni (ovvero metà anno), allora esso può essere ripetuto solo due volte a partire dalla data iniziale scelta, mentre se il periodo è di 121 giorni (ovvero ⅓ di anno), allora esso può essere ripetuto tre volte a partire dalla data iniziale scelta, ecc;

e fornisce altresì le seguenti statistiche:
* numero totale di eventi in ogni Stato
* numero totale di eventi raggruppati per genere in ogni Stato
* numero minimo, massimo e media degli eventi mensili in ogni Stato

## Installazione
È possibile eseguire il download della Filter-App The Last of Events attraverso tre semplici passaggi:
* creare una cartella sul desktop che possa ospitare l’applicativo
* aprire il terminale nella cartella appena generata
* digitare:  `git clone https://github.com/KevinGiusti/progetto-OOP`

## Configurazione API Ticketmaster
Le API derivate dalla pagina TM Developer di Ticketmaster, impiegate per la definizione delle classi relative all’applicativo The Last of Events, presentano la seguente struttura:
![alt text](https://raw.githubusercontent.com/KevinGiusti/progetto-OOP/main/UML/readme%20images%231/mainn.jpg)
che può essere sintetizzata mediante il seguente grafico:

![alt text](https://raw.githubusercontent.com/KevinGiusti/progetto-OOP/main/UML/readme%20images%231/0.0.5-%23mappa%20uml%20classi.jpg)

## Configurazione API Ticketmaster
Non lo so, robe che mi deve dire Rocco circa la key che altrimenti l'Univpm vive di stracci e fagioli

## UML
### Use Case Diagram

![alt text](https://raw.githubusercontent.com/KevinGiusti/progetto-OOP/main/UML/readme%20images%231/UseCaseFinal.jpg)
Segue la descrizione di tutti i casi d'uso dello Use Case Diagram che esprime il comportamento dell'applicazione:
**Caso d'uso** | **Descrizione**
---- | ----
User | utente che utilizza l'applicazione The Last of Events impiegando diverse funzionalità
Scelta filtro di ricerca | l'utente sceglie uno o più dei filtri disponibili, tra cui: filtro Stati, filtro generi e filtro periodo personalizzato
Filtro Stati | il filtro Stati può essere utilizzato singolarmente o in combinazione con altri filtri, permette di scegliere un singolo Stato, tutti gli stati disponibili oppure una lista specifica di stati
Uno Stato | chiamata HTTP POST alle API dell'applicativo Ticketmaster che filtra le informazioni relative all'unico Stato inserito
Più Stati | chiamata HTTP POST alle API dell'applicativo Ticketmaster che filtra le informazioni relative agli Stati inseriti
Stati consigliati digitando una sottostringa | chiamata HTTP POST alle API dell'applicativo Ticketmaster che suggerisce il nome di uno o più Stati in base alla sottostringa inserita
Filtro generi | il filtro generi può essere utilizzato singolarmente o in combinazione con altri filtri, permette di scegliere un singolo genere, tutti i generi disponibili oppure una lista specifica di generi
Un genere | chiamata HTTP POST alle API dell'applicativo Ticketmaster che filtra le informazioni relative all'unico genere inserito; i risultati, ovviamente, sono gli eventi che corrispondono al criterio di ricerca
Più generi | chiamata HTTP POST alle API dell'applicativo Ticketmaster che filtra le informazioni relative ai generi inseriti; i risultati, ovviamente, sono eventi che corrispondono al criterio di ricerca
Ricerca Eventi | primo EndPoint del programma, mostra tutti gli eventi che soddisfano le condizioni imposte dai filtri di ricerca per Stati e per Generi
Visualizzare statistiche eventi | secondo EndPoint del programma, mostra tutte le statistiche inerenti ad ogni evento che soddisfa i filtri di ricerca
Numero totale eventi | statistica che indica il numero totale di eventi relativi agli stati che soddisfano i criteri di ricerca
Numero eventi raggruppati per genere | statistica che indica il numero totale di eventi relativi agli stati appartenenti ad un determinato genere
Numero minimo-massimo-media eventi in un mese o periodo | filtro sulle statistiche che consente di scegliere un periodo standard, ovvero il mese, o un periodo personalizzato, al fine di calcolare il numero minimo, massimo e la media degli eventi in ciascun mese/in ciascuna ripetizione del periodo personalizzato
Filtro periodo di tempo | filtro che consente di scegliere un periodo personalizzato; in caso l'utente non desideri inserire un periodo, verrà considerato il mese come unità di misura temporale per la produzione delle statistiche relative al numero minimo, massimo ed alla media degli eventi in un arco di tempo
Mese | statistica che mostra il numero minimo, massimo e la media degli eventi, che soddisfano i criteri di ricerca precedenti, in ciascuno dei 12 mesi dell'anno
Periodo personalizzato | statistica che mostra il numero minimo, massimo e la media degli eventi, che soddisfano i criteri di ricerca precedenti, in ciascuna delle ripetizioni del periodo personalizzato; l'ultima ripetizione del periodo scelto è quella che non supera il 364-esimo giorno dell'anno della data iniziale inserita dall'utente

### Class Diagram
inserisci il diagramma uml delle classi in HD

percorso e packages dell'applicativo:

![alt text](https://raw.githubusercontent.com/KevinGiusti/progetto-OOP/main/UML/ProjectClassDiagram/ProjectClassDiagram_jpeg/Package%20jpg/Package%20Structure0001.jpg)
