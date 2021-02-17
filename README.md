<H1 align="center">The Last of Events</H1>
<H2 align="center">an OOP-Java project made with Spring</H2>
<H4 align="center">Repository progetto programmazione OO febbraio 2021</H4>

## Sommario:
- [Introduzione](#introduzione)
- [Installazione](#installazione)
- [Struttura API Ticketmaster](#configurazione-api-ticketmaster)
- [Configurazione](#configurazione)
- [UML](#uml)
  - [Use Case Diagram](#use-Case-diagram)
  - [Class Diagram](#class-diagram)
  - [Sequence Diagram](#sequence-diagram)
  - [Sequence Diagram Rotta “/eventi”](#sequence-diagram-rotta-eventi)
- [Rotte](#rotte)
  - [Filtri e Stats Richiesti](#filtri-e-stats-richiesti)
  - [Body della rotta e risposta JSON](#body-della-rotta-e-risposta-json)
  - [Chiavi e Valori](#chiavi-e-valori)
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
* aprire il terminale nella cartella appena generata (si consiglia l'uso di GitBash)
* digitare:  `git clone https://github.com/KevinGiusti/progetto-OOP`

Alternativamente, è possibile impiegare l'ambiente di sviluppo Eclipse operando come segue;
* creare un nuovo account su GitHub (in allegato, l'indirizzo web https://github.com/)
* creare una cartella sul desktop che ospiti l'applicazione The last of Events
* avviare il software Eclipse
* selezionare la voce `Window > Show View > Other... > Git > Git Repositories`
* una volta selezionata la voce `Git Repositories`, cliccare su `Clone a Repository...'
* inserire, poi, l'indirizzo `https://github.com/KevinGiusti/progetto-OOP` nella voce `URI`(Uniform resource Identifier)
* una volta inserito l'`URI`, inserire le credenziali di accesso GitHub alle voci `User` e `Password` e selezionare `next` assicurandovi che, alla voce `Connection`, la casella `Protocol` sia impostata su `https`
* dopo aver cliccato `next`, assicuratevi che il Branch `main` sia auto-selezionato e, alla voce `Tag fetching strategy`, impostare `When fetching a commit, also fetch his tags`
* infine, alla voce `Destination` cliccare su `browse` e selezionare la cartella, precedentemente creata, che ospiterà il software
* per concludere, selezionare `Finish` ed il download del progetto sarà concluso.

## Struttura API Ticketmaster
Le API derivate dalla pagina TM Developer di Ticketmaster, impiegate per la definizione delle classi relative all’applicativo The Last of Events, presentano la seguente struttura:
![alt text](https://raw.githubusercontent.com/KevinGiusti/progetto-OOP/main/UML/readme%20images%231/mainn.jpg)
che può essere sintetizzata mediante il seguente grafico:

![alt text](https://raw.githubusercontent.com/KevinGiusti/progetto-OOP/main/UML/readme%20images%231/0.0.5-%23mappa%20uml%20classi.jpg)

## Configurazione
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
--------------------------------------------------------------------------inserisci il diagramma uml delle classi in HD

percorso e packages dell'applicativo:

![alt text](https://raw.githubusercontent.com/KevinGiusti/progetto-OOP/main/UML/ProjectClassDiagram/ProjectClassDiagram_jpeg/Package%20jpg/Package%20Structure0001.jpg)

### Sequence Diagram
--------------------------------------------------------------------------inserisci il diagramma uml delle sequenze

### Sequence Diagram Rotta “/eventi”
--------------------------------------------------------------------------inserisci il diagramma uml delle sequenze

## Rotte
Nel caso in cui l'interazione tra l'utente ed il software 'The last of Events' non avvenga tramite GUI, ovvero tramite Graphic User Interface, è possibile impiegare un qualsiasi tool per il testing delle Application Programming Interface come, ad esempio, Postman , reperibile all'indirizzo https://www.postman.com/downloads/, per effettuare delle chiamate API.

In particolare, le richieste che l'utente può effettuare tramite Postman devono essere all'indirizzo: `localhost:8080`, dove `localhost` è l'interfaccia di loopback necessaria per indirizzare verso se stessi i dati e `8080` è la porta di accesso del server locale;

Inoltre, all' indirizzo `localhost:8080` inserito nella barra delle richieste di Postman, è necessario specificare metodo di trasferimento dati e rotta.
### Filtri e Stats Richiesti
Poichè, nel documento descrittovo del progetto, è esplicitamente richiesto che:
>L'applicazione deve permettere all'utente finale di: cercare gli eventi di un determinato stato, visualizzare delle statistiche per ogni stato di 
Australia e Nuova Zelanda **con un'unica richiesta**

allora **l'unica** rotta definita per l'applicativo 'The Last of Events' è: `/eventi`, ovvero:
Metodo | Rotta | Descrizione
---- | ---- | ----
`POST` | `/eventi` | restituisce un JSONArray contenente le informazioni relative ad eventi, che possono essere filtrati per uno o più stati e/o per uno o più generi, e statistiche relative a numero totale di eventi per ogni stato, numero totale di eventi raggruppati per genere e massimo, minimo e media eventi mensili o in un periodo personalizzato

### Body della rotta e risposta JSON
Dal punto di vista tecnico, i parametri, inseriti per effettuare una ricerca relativa agli eventi, devono essere passati all'applicazione Spring, che è in esecuzione sul server locale,  tramite il **body** della rotta `localhost8080/eventi` che , a sua volta, deve essere configurato sottoforma di **file JSON** (JavaScript Object Notation), in formato `raw`, contenente   tutte le coppie "key":"value" necessarie per il filtraggio delle informazioni.
Di seguito, è riportato un esempio grafico di quanto appena descritto:
```json
{
    "stati": ["Victoria, AU","Queensland, AU"],
    "generi": [],
    "periodo": ["2021-01-01","2021-03-01"]
}
```
Alla richiesta appena specificata otteniamo, in risposta dal software 'The Last Of Tickets', il seguente file JSON:
```json
{
    "numero totale eventi": {
        "in Victoria": 2,
        "in Queensland": 1
    },
    "statistiche periodiche di eventi": {
        "in Victoria": {
            "minimo": 0,
            "massimo": 2,
            "media": 0.29
        },
        "in Queensland": {
            "minimo": 0,
            "massimo": 1,
            "media": 0.14
        }
    },
    "numero eventi per il genere": {
        "Pop": 3
    },
    "eventi": [
        {
            "nome": "Backstreet Boys",
            "url": "http://resale.ticketmaster.com.au/Resale/Tickets/2797641",
            "citta": "Melbourne",
            "stato": "Victoria",
            "paese": "Australia",
            "data": "2021-05-03",
            "ora": "19:30:00",
            "genere": "Pop",
            "sottoGenere": "Pop Rock"
        },
        {
            "nome": "Backstreet Boys",
            "url": "http://resale.ticketmaster.com.au/Resale/Tickets/2805221",
            "citta": "Melbourne",
            "stato": "Victoria",
            "paese": "Australia",
            "data": "2021-05-04",
            "ora": "19:30:00",
            "genere": "Pop",
            "sottoGenere": "Pop Rock"
        },
        {
            "nome": "Backstreet Boys",
            "url": "http://resale.ticketmaster.com.au/Resale/Tickets/2797640",
            "citta": "Boondall",
            "stato": "Queensland",
            "paese": "Australia",
            "data": "2021-05-01",
            "ora": "19:30:00",
            "genere": "Pop",
            "sottoGenere": "Pop Rock"
        }
    ]
}
```

### Chiavi e Valori
Le coppie "key":"value" che devono essere specificate, in formato JSON, nel `Body` della richiesta `localhost8080/eventi` sono:
key | value | descrizione
---- | ---- | ----
`"stati"` | `: ["nome Stato, nome Paese", "...", ..]` | la key `"stati"` è un JSONArray che ha, come elementi, la coppia 'nome Stato' e 'sigla' del Paese in cui è contenuto lo stato come, ad esempio, "Victoria, AU"
`"generi"` | `: ["nome genere", "...", ..]` | la key `"generi"` è un JSONArray che ha, come elementi, il nome di ciascun genere specificato dall'utente come, ad esempio, "Pop"
`"periodo"` | `: ["data iniziale, data finale"]` | la key `"periodo"` è un JSONArray che ha, come unico elemento, la coppia 'data iniziale - data finale' inserita dall'utente come, ad esempio, "2021-01-01","2021-03-01"

**Valori accettabili per ogni key**
key | valori accettabili
---- | ----
`"stati"` | New South Wales, AU; Queensland, AU; South Australia, AU; Tasmania, AU; Victoria, AU; Western Australia, AU;  New Zealand, NZ;
`"generi"` | Accounting/General, Action/Adventure, Actor, Added Value Vouchers, Alternative, Amusement Park, Animation, Aquarium, Aquatic Park, Aquatics, Arthouse, Artist, Athlete, Athletic Races, Audio Tour, Audio/Visual, Award Show, Badminton, Ballads/Romantic, Band, Bandy, Baseball, Basketball, Biathlon, Blues, Body Building, Boxing, CD, Campsite, Casino/Gaming, Ceremony, Chanson Francaise, Character, Charity/Benefit, Children's Festival, Children's Music, Children's Theatre, Choir, Choreographer, Chorus, Circus & Specialty Acts, Classical, Clothing, Club, Club Access, Comedian, Comedy, Community/Civic, Community/Cultural, Competition, Concert, Concession Voucher, Conductor, Convention, Country, Cricket, Cruise, Cultural, Curling, Cycling, Dance, Dance/Electronic, Dancer, Demo, Designer, Dinner Packages, Director, Documentary, Donation, Drama, Driver, Ensemble, Equestrian, Especiales, Espectaculo, Exchange, Exhibit, Expo, Extreme, Fairs & Festivals, Family, Fan Experiences, Fashion, FastLane Access, Festival, Field Hockey, Fine Art, Fitness, Floorball, Folk, Food & Drink, Football, Foreign, Gift Card, Gift Certificate, Golf, Graduation/Commencement, Group, Guide, Gymnastics, Handball, Health/Wellness, Hip-Hop/Rap, Hobby/Special Interest Expos, Hockey, Holiday, Horror, Hotel Package, Ice Rink, Ice Shows, Ice Skating, In-Store Pickup, Individual, Indoor Soccer, International Online Order, Jazz, Lacrosse, Latin, Lawn Chair Rental, League, Lecture/Seminar, Lockers, Magazine Mail Merchandise, Magic & Illusion, Magician, Martial Arts, Meal Package, Medieval/Renaissance, Membership, Merch 3rd Party Delivered, Merchandise, Merchandise Voucher, Metal, Miscellaneous, Miscellaneous Theatre, Motorsports/Racing, Mucisian, Multimedia, Museum, Music, Netball, New Age, Nonticket, Opera, Orchestra, Other, Other (inc. RV, oversized), Parade, Parking, Party/Gala, Performance Art, Performer, Pop, Premier, Priority Mail, Psychics/Mediums/Hypnotists, Puppetry, Quartet, RB, Race, Reggae, Religious, Reserved Lawn Access, Rock, Rodeo, Roller Derby, Roller Hockey, Room Package, Rugby, Science Fiction, Sightseeing/Facility, Singer/Vocalist, Ski Jumping, Skiing, Soccer, Softball, Speaker, Special Entry, Special Interest/Hobby, Spectacular, Squash, Student Festival, Subscription, Surfing, Swap Meet/Market, Swimming, TM Gift Card, TM Gift Certificate, TVN, Table Tennis, Team, Tennis, Test Event, Theatre, Ticketfast Order, Toros, Tour, Touring Show/Production, Track & Field, Transportation, Tribute Band, Troupe, UPS, Undefined, Upsell, Urban, VIP Club Access, Variety, Virtual, Volleyball, Voucher, Waterpolo, World, Wrestling, Writer, Zoo, eSports, iTunes Download
`periodo` | ogni periodo di tempo desiderato

**Eccezioni e bad-values**
Quando si effettua una richiesta alla Filter-App 'The Last of Events' mediante un tester di API quale Postman, è possibile che, nel `Body` della richiesta stessa, ad una o più `key` vengano associati dei `value` che generano delle eccezioni nel programma;

in questi casi, l'applicazione gestisce l'eccezione occorsa e restituisce un JSON con un'unica `key`, nota come `Attenzione` o come `Errore`, ed un unico `value`, che descrive all'utente sia l'errore commesso e sia eventuali soluzioni al problema. 
Key | Bad-value | Eccezione | Risposta dell'applicazione
---- | ---- | ---- | ----
`"stati"` | `:[]` | EventiException() |  `"Attenzione": "Non è stato specificato nessuno stato. Lista stati: [New South Wales, Queensland, South Australia, Tasmania, Victoria, Western Australia, New Zealand]"`
`"stati"` | `:["Victoria, "]` | EventiException() | `"Errore": "Il formato consentito nel vettore 'stati' è il seguente: 'Stato, Paese'"`
`"stati"` | `:[" , AU"]` | EventiException() | `"Attenzione": "Nessuno stato inizia per  . Lista stati: [New South Wales, Queensland, South Australia, Tasmania, Victoria, Western Australia, New Zealand]"`
`"stati"` | `:["Victoria, IT"]` | EventiException() | `"Errore": "Lo stato IT non è disponibile"`
`"stati"` | `:["Victoria, NZ"]` | EventiException() | `"Errore": "Lo stato Victoria non appartiene al paese NZ"`
`"generi"` | `:["123"]` | EventiException() | `"Attenzione": "Nessun genere inizia per 1. Lista generi: [Accounting/General, Action/Adventure,`ecc...
`"periodo"` | `:["2021-01-01"]` | EventiException() | `"Attenzione": "è possibile inserire solo due date, ovvero la data di inizio e la data di fine"`
`"periodo"` | `:["2021-01-01","2021-03-01", "2021-07-01"]` | EventiException() | `"Attenzione": "è possibile inserire solo due date, ovvero la data di inizio e la data di fine"`
`"periodo"` | `:["2021-12-01","2021-03-01"]` | EventiException() | `"Errore": "la prima data deve essere minore della seconda data inserita"`
`"periodo"` | `:["2021-00-01","2021-03-01"]` | EventiException() | `"Errore": "Il formato consentito per il mese nel vettore 'periodo' è il seguente: da 01 a 12"`
`"periodo"` | `:["2021-01-75","2021-03-01"]` | EventiException() | `"Errore": "Il formato consentito per il giorno nel vettore 'periodo' è il seguente: da 01 a 31 a seconda del mese"`
`"periodo"` | `:["Shrek","2021-03-01"]` | EventiException() | `"Errore": "Il formato consentito nel vettore 'periodo' è il seguente: 'yyyy-mm-dd'"`
