<H1 align="center">The Last of Events</H1>
<H2 align="center">an OOP-Java project made with Spring</H2>
<H4 align="center">Repository progetto programmazione OO febbraio 2021</H4>

## Sommario:
- [Introduzione](#introduzione)
- [Installazione](#installazione)
- [Struttura API Ticketmaster](#struttura-api-ticketmaster)
- [Considerazioni Generali](#considerazioni-generali)
- [Considerazioni Necessarie](#considerazioni-necessarie)
- [UML](#uml)
  - [Use Case Diagram](#use-case-diagram)
  - [Class Diagram](#class-diagram)
  - [Sequence Diagram](#sequence-diagram)
  - [Sequence Diagram Rotta “/eventi”](#sequence-diagram-rotta-eventi)
- [Rotte](#rotte)
  - [Filtri e Stats Richiesti](#filtri-e-stats-richiesti)
  - [Body della rotta e risposta JSON](#body-della-rotta-e-risposta-json)
  - [Chiavi e Valori](#chiavi-e-valori)
- [JUnit Test](#junit-test)
- [Documentazione JavaDoc](#documentazione-javadoc)
- [GUI: Premesse](#gui-premesse)
- [Software Utilizzati](#software-utilizzati)
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

## Considerazioni Generali

In primo luogo, è necessario osservare che la Filter-App 'The Last of Events' propone due tipi diversi di interazione tra utente ed applicativo;
Infatti, il servizio proposto dal software, in esecuzione sul server locale alla porta `8080`, è accessibile sia mediante un tool di testing delle Application Programming Interface, comunemente note come `API`, come, ad esempio, Postman, e sia mediante una Graphic User Interface, ovvero tramite `GUI`, che rende User Friendly la componente `Front-End` dell'applicazione e che gestisce, tramite Spring ed Eclipse, la parte di `Back-End`.

Inoltre, è altresì importante considerare che, poichè l'intero programma è stato pensato, scritto, ideato e sviluppato su `Windows 10` per `Windows 10`, è preferibile che l'applicativo stesso venga eseguito su tale Sistema Operativo; tuttavia, nonostante questa propensione, sarà comunque possibile accedere all'applicazione mediante `SO` quali `Linux` e `Mac OS` semplicemente avviando la `GUI` direttamente da `Eclipse` piuttosto che da file eseguibile;

In particolare, la predilezione del Sistema Operativo `Windows 10` rispetto agli altri possibili `SO` è dovuta non solo alla possibilità di avviare direttamente il file eseguibile `The Last Of Events.jar` della parte `Front-End` dell'intero Software, ma è dovuta anche ad un miglior rendimento grafico della `GUI` poichè, su piattaforme quali `Linux` e `Mac OS`, alcuni caratteri speciali non sono leggibili a causa delle `ASCII-table` ed i contorni degli elementi dell'interfaccia User-Friendly sono meno definiti rispetto alla finestra generata su `Windows 10`.

Dal punto di vista tecnico, l'impossibilità di eseguire direttamente il file di lancio della parte `Front-End` del software 'The Last of Events' su piattaforme quali `Linux` e `Mac OS` è dovuta a motivi di sicurezza, relativi all'origine dell'App, imposti dai suddetti Sistemi Operativi; tuttavia, tale impedimento è facilmente superabile dal momento che, per utilizzare la `GUI`, sarà sufficiente avviare il programma dalla classe `main` sita internamente al codice del programma.

Per concludere, nel caso si dovesse preferire l'esecuzione di 'The Last of Events' mediante `GUI` su piattaforma `Windows 10` , affinchè le finestre dell'App vengano visualizzate nel modo corretto  su schermi con elevati `DPI` (Dot Per Inches), è necessario ridimensionare lo schermo al valore `100%` attraverso i seguenti passaggi:
`Impostazioni > Schermo > Ridimensionamento e Layout > Modifica la dimensione di testo, app e altri elementi`, ed è altresì consigliata l'installazione del`font` `Press Gothic.otf`, reperibile accedendo al percorso `progetto-OOP > GUI > resources > 'Press Gothic.otf'`

**Nota:** l'installazione del `font` viene eseguita, senza impedimenti di alcun genere, su ogni `SO`.


## Considerazioni Necessarie

**IMPORTANTE:** Per motivi legati all'impossibilità, da parte degli sviluppatori, di divulgare una chiave ottenuta mediante previa registrazione, prima di poter impiegare l'Applicativo 'The Last of Events', indipendentemente dal fatto che si favorisca l'approccio tramite `Postman` o tramite `GUI`, è necessario accedere alla cartella `resources`, reperibile attraverso il percorso `progetto-OOP > ticketmaster > resources`, e modificare il file `APIKey.txt`, inizialmente vuoto per ogni utente che esegue l'operazione di `clone` del progetto, inserendo la propria `key` gratuita ottenuta mediante registrazione presso il sito [TM Developers](https://developer.ticketmaster.com/products-and-docs/apis/discovery-api/v2/);

Una volta completata tale operazione, è sufficiente avviare l'`IDE Eclipse` ed eseguire il comando di `Refresh` selezionando la cartella principale del progetto, nota come `ticketmaster`, attraverso il tasto destro del mouse o touchpad.
In questo modo, una volta avviato il software, la `key` inserita dall'utente verrà letta mediante uno scanner e, se risulterà accettabile, l'applicazione sarà completamente fruibile.

**Osservazioni Finali**
Nel caso si utilizzi il Sistema Operativo `Windows 10`, il file eseguibile della `GUI`, noto come `The Last Of Events.jar`, reperibile nel percorso `progetto-OOP > GUI`, permette di evitare di importare in `Eclipse` la cartella `GUI`; infatti, selezionando tale file, è possibile avviare la parte `Front-End` dell'App semplicemente lanciando l'eseguibile che, tuttavia, per funzionare correttamente, dovrà sempre essere interconnesso alla parte `Back-End` del software rappresentata mediante applicazione `Spring` in esecuzione nell'`IDE Eclipse`. 

Infine, quando si impiega la Graphic User Interface per l'esecuzione di 'The Last of Events', è possibile che, nella prima finestra dell'applicativo, ovvero nella schermata Home, non compaiano i campi selezionabili o il logo dell'App; per risolvere questo tipo di inconveniente, è sufficiente scorrere, con il cursore del mouse, lungo l'intera pagina in modo che tutti i pulsanti, venendo selezionati, possano attivarsi nuovamente;
Alternativamente, è possibile riavviare il programma oppure selezionare la schermata successiva, tramite il pulsante `entra`, per poi tornare nuovamente nella `Home`.

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
`"stati"` | `:[]` | EventiException |  `"Attenzione": "Non è stato specificato nessuno stato. Lista stati: [New South Wales, Queensland, South Australia, Tasmania, Victoria, Western Australia, New Zealand]"`
`"stati"` | `:["Victoria, "]` | EventiException | `"Errore": "Il formato consentito nel vettore 'stati' è il seguente: 'Stato, Paese'"`
`"stati"` | `:[" , AU"]` | EventiException | `"Attenzione": "Nessuno stato inizia per  . Lista stati: [New South Wales, Queensland, South Australia, Tasmania, Victoria, Western Australia, New Zealand]"`
`"stati"` | `:["Victoria, IT"]` | EventiException | `"Errore": "Lo stato IT non è disponibile"`
`"stati"` | `:["Victoria, NZ"]` | EventiException | `"Errore": "Lo stato Victoria non appartiene al paese NZ"`
`"generi"` | `:["123"]` | EventiException | `"Attenzione": "Nessun genere inizia per 1. Lista generi: [Accounting/General, Action/Adventure,`ecc...
`"periodo"` | `:["2021-01-01"]` | EventiException | `"Attenzione": "è possibile inserire solo due date, ovvero la data di inizio e la data di fine"`
`"periodo"` | `:["2021-01-01","2021-03-01", "2021-07-01"]` | EventiException | `"Attenzione": "è possibile inserire solo due date, ovvero la data di inizio e la data di fine"`
`"periodo"` | `:["2021-12-01","2021-03-01"]` | EventiException | `"Errore": "la prima data deve essere minore della seconda data inserita"`
`"periodo"` | `:["2021-00-01","2021-03-01"]` | EventiException | `"Errore": "Il formato consentito per il mese nel vettore 'periodo' è il seguente: da 01 a 12"`
`"periodo"` | `:["2021-01-75","2021-03-01"]` | EventiException | `"Errore": "Il formato consentito per il giorno nel vettore 'periodo' è il seguente: da 01 a 31 a seconda del mese"`
`"periodo"` | `:["Shrek","2021-03-01"]` | EventiException() | `"Errore": "Il formato consentito nel vettore 'periodo' è il seguente: 'yyyy-mm-dd'"`

## JUnit Test
Per facilitare la lettura e la comprensione del discorso intorno al testing dell'applicativo, è utile considerare il seguente Class Diagram:
![alt text](https://raw.githubusercontent.com/KevinGiusti/progetto-OOP/main/UML/readme%20images%231/uuuuuu.jpg)

Per verificare la correttezza dei risultati prodotti da alcuni metodi del software 'The Last of Events', sono stati implementati i seguenti **unit test** mediante l'utilizzo del framework JUnit:
___
### Test Metodi Della Classe MinMaxAverageFilter.java
Per il testing dei metodi della classe MinMaxAverageFilter.java sono stati implementati i seguenti JUnit Test Case, reperibili nel percorso
`ticketmaster > src/test/java > it.univpm.progetto.studenti.ticketmaster.minmaxav_junit_test`:

**1) dateConverterTest**

La JUnit Test Case 'dateConverterTest' contiene due test methods, rispettivamente noti come 'testDateConverter' e 'testDateConverterException', che verificano il corretto funzionamento del metodo dateConverter() dedito alla conversione di una stringa di testo in un oggetto della classe localDate;
in particolare:
* **testDateConverter():** Metodo per testing del metodo dateConverter(), relativo al controllo della stringa inserita nel convertitore, che, fornita una stringa rappresentante una data, ed un oggetto della classe LocalDate che rappresenta la medesima data, controlla se il risultato della conversione sia pari all'oggetto LocalDate;
in sintesi, testDateConverter() invoca il metodo assertEquals(), i cui parametri sono il risultato della conversione tramite il metodo dateConverter e l'oggetto di tipo LocalDate ante introdotto.
* **testDateConverterException():** Metodo per testing del metodo dateConverter(), relativo al controllo della stringa inserita nel convertitore, che, fornita una stringa rappresentante una data errata, generi un'eccezione di tipo `DateTimeParseException`;
in sintesi, testDateConverter() invoca il metodo assertThrows(), i cui parametri sono il risultato della conversione tramite il metodo dateConverter e la classe `DateTimeParseException.class` della libreria `java.time.format`

**2) MaxRipetizioneDelPeriodoTest**
La JUnit Test Case 'MaxRipetizioneDelPeriodoTest' contiene un unico test method, rispettivamente noto come 'maxRipetizioneDelPeriodoTest', che verifica il corretto funzionamento del metodo maxRipetizioneDelPeriodo() che, a sua volta, è dedito al calcolo del numero di volte in cui il periodo personalizzato inserito dall'utente può essere ripetuto nell'arco di un anno;
in particolare:
* **maxRipetizioneDelPeriodoTest()** Metodo per testing del metodo maxRipetizioneDelPeriodo, che confronta il numero di ripetizioni corretto con il risultato prodotto dal metodo maxRipetizioneDelPeriodo; in sintesi, maxRipetizioneDelPeriodoTest() invoca il metodo assertEquals(), i cui parametri sono il risultato del metodo maxRipetizioneDelPeriodo() ed il numero di volte in cui, effettivamente, il periodo personalizzato si ripete nel corso di un anno.

**3) MinMaxAverageFilterFunctionTest**
La JUnit Test Case 'MinMaxAverageFilterFunctionTest' contiene un unico test method, rispettivamente noto come 'testMinMaxAerageFilterFunction', che verifica il corretto funzionamento del metodo minMaxAverageFilterFunction() che, a sua volta, è dedito al calcolo del numero totale di eventi, relativi ad uno specifico Stato, che si svolgono in una specifica ripetizione del periodo di tempo personalizzato scelto dall'utente;
in particolare:
* **testMinMaxAerageFilterFunction()** Metodo per testing del metodo minMaxAverageFilterFunction che controlla se il metodo testato assegna, in maniera corretta, ogni evento dello Stato considerato alla relativa ripetizione del periodo di tempo personalizzato; in sintesi, testMinMaxAerageFilterFunction() invoca il metodo assertEquals(), i cui parametri sono il risultato del metodo minMaxAverageFilterFunction() ed il corretto raggruppamento di eventi-periodo
---
### Test Metodi Della Classe DatesStatistics.java
Per il testing dei metodi della classe DatesStatistics.java è stato implementato il seguente JUnit Test Case, reperibile nel percorso
`ticketmaster > src/test/java > it.univpm.progetto.studenti.ticketmaster.datesstatistics_junit_test`:

**1) DatesStatisticsTest**
La JUnit Test Case 'DatesStatisticsTest' contiene due test methods, rispettivamente noti come 'datesStatisticsTest' e 'datesStatisticsTestNotNull', che verificano il corretto funzionamento del metodo numeroEventi() che, a sua volta, è dedito al calcolo del numero totale di eventi, relativi ad uno specifico Stato, che si svolgono in uno specifico mese;
in particolare:

* **datesStatisticsTest():** Metodo per testing del metodo numeroEventi() che controlla se numeroEventi() assegna, in maniera corretta, ciascun evento, relativo ad uno specifico Stato selezionato dall'utente, al relativo mese in cui sarà svolto;
in sintesi, datesStatisticsTest() invoca il metodo assertEquals(), i cui parametri sono il risultato del metodo numeroEventi() ed il corretto raggruppamento di eventi-mese
* **datesStatisticsTestNotNull():** Metodo che accerta che il vettore contenente gli eventi da raggruppare mensilmente non sia sia vuoto, in modo da poter eseguire correttamete il metodo numeroEventi(); sintesi, datesStatisticsTestNotNull() invoca il metodo assertNotNull(), il cui unico parametro è il vettore di eventi da analizzare
---
### Test Metodi Della Classe MinMaxAverage.java
Per il testing dei metodi della classe MinMaxAverage.java è stato implementato il seguente JUnit Test Case, reperibile nel percorso
`ticketmaster > src/test/java > it.univpm.progetto.studenti.ticketmaster.minmaxaverage_junit_test`:

**1) SortSelectedEventsTest**
La JUnit Test Case 'SortSelectedEventsTest' contiene un'unico test Method, rispettivamente noto come 'sortSelectedEventsTest', che verifica il corretto funzionamento del metodo sortSelectedEvents() che, a sua volta, è dedito all'ordinamento dell'array contenente il numero di eventi di uno Stato, svoltisi in un determinato mese, disponendoli dal più piccolo al più grande;
in particolare:

* **sortSelectedEventsTest():** Metodo per testing del metodo sortSelectedEvents che controlla se il sorting di un array di interi è svolto nel modo corretto
in sintesi, datesStatisticsTest() invoca il metodo assertEquals(), i cui parametri sono il risultato del metodo sortSelectedEvents ed un array ordinato nel modo corretto

## Documentazione JavaDoc
Ogni package, classe, attributo e metodo che costituisce il software 'The Last of Events' è interamente e completamente documentato attraverso l'utilizzo della JavaDoc;

In particolare, per accedere alla documentazione tramite pagina HTML, è necessario seguire il percorso:
`ticketmaster > doc > index-files > index-1.html`.

Una volta aperta la pagina `index-1.html`, è possibile accedere alla documentazione dell'intero codice selezionando:
* la voce `OVERVIEW` che descrive ogni package del progetto
* la voce `TREE` che descrive la gerarchia delle classi del progetto
* la voce `INDEX` che permette di cercare packages, classi, attributi e metodi in base al carattere iniziale selezionato
* la voce `INDEX > All Classes` che descrive ogni classe del progetto
* la voce `INDEX > All Classes > Exception Summary` che descrive la classe di gestione eccezioni del progetto

Ovviamente, cliccando il nome di una qualsiasi classe nella pagina `index-1.html`, sarà possibile accedere ad informazioni quali metodi, attributi, package di appartenenza, metodo costruttore, autore della classe, ecc...

## GUI: Premesse

<H1>
La Filter-App 'The Last of Events' prevede due tipi diversi di interazione tra utente ed applicativo;
In particolare, la prima metodologia di interazione prevede che l'utente inoltri delle richieste al software mediante un file JSON, che costituisce il `Body` della rotta `localhost:8080/eventi`, in cui inserisce i parametri desiderati;
La seconda metodologia, al contrario, prevede un tipo di interazione utente-sistema mediante una Graphic User Interface(`GUI`);

Affinchè l'esperienza proposta dalla `GUI` sia la migliore possibile è necessario che, su schermi ad alti DPI (Dot Per Inch), si effettui un ridimensionamento dello schermo dal valore predefinito al 100%, poichè, altrimenti, le immagini risulterebbero sgranate;
SCRIVERE PATH
</H1>

<H1>
(tutto il progetto e non solo gui) Il programma è stato pensato, ideato e sviluppato su e per Windows 10 (per questo motivo, è preferibile che l'applicativo venga eseguito su win 10); tuttavia, nonostante la premessa, il programma funziona (per grazia di Javaeh) anche su Linux (mac da provare)
tuttavia, il programma, su linux, presenta le seguenti limitazioni: 
1) difetti grafici quali: ad esempio, cursore più grande del consueto, caratteri non leggibili e sostituiti con <?>
2) l'eseguibile della gui non funziona perchè, essendo generato su win, per motivi di sicurezza su Linux, non viene riconosciuto come eseguibili; la gui deve essere importata in eclipse e lanciata da Eclipse attraverso la classe main
3) si saprà se dio vorrà...
4) 
</H1>
</br>
</br>
</br>
</br>
<H1>
(tutto il progetto e non solo gui)  nella folder resources (contenente i due file scannerizzati stati e generi .csv letti dallo Dalla classe scanner e passati ad i vari metodi) è stato aggiunto un file .txt APIKey che sarà inizialmente vuoto PER TUTTI coloro che eseguono il clone del progetto dall'indirizzo...
per motivi di sicurezza relativi all'impossibilità di divulgare una key ottenuta mediante registrazione presso il sito ticketmaster, ogni utente che vorrà impiegare l'intero progetto (gui o meno) dovrà registrarsi su tm developers, richiedere la propria key gratuita, ed inserirla nel file APIKey.
La key inserita in APIKey verrà letta mediante uno scanner nel progetto ed, una volta letta, viene sostituita nella chiamata (simil postman) (ai prof la inviamo noi)
</H1>
</br>
</br>
</br>
</br>
<H1>
(solo gui) è stato generato l'eseguibile della gui, noto come 'The Last Of Events.jar' (con loghino java), che si trova nel percorso 
progetto-OOP > GUI > 'The Last Of Events.jar'
la creazione di questo eseguibile permette di evitare di importare in Eclipse la cartella (progetto) GUI;
in questo caso, l'applicazione parte semplicemente lanciando l'eseguibile; PERò sarà comunque necessario avviare l'applicazione Spring mediante Java per la parte di BackEnd.
L'eseguibile funziona solo su windows, su linux ci sono restirizioni, su mac boh.
</H1>
</br>
</br>
</br>
</br>
<H1>
(solo gui) Potrebbe succedere che, quando si avvia la GUI, nella prima finestra (Home) potrebbero sparire i campi selezionabili o il logo; tuttavia, se si passa con il mouse sui pulsanti invisibili, questi riappaiono.
Per risolvere, o si spegnene e riaccende oppure si passa alla schermata successiva tramite il pulsante 'entra' e poi si torna indietro ed è tutto a posto (priblema in fase di sviluppo della gui, ora pare che funziona)
</H1>
</br>
</br>
</br>
</br>
<H1>
(solo gui) Per visualizzare correttamente la gui è necessario installare il font 'Press Gothic.otf', accessibile al percorso
progetto-OOP > GUI > resources > 'Press Gothic.otf'
l'installazione è corretta sia su win che su linux, da vedere su mac.
</H1>
</br>
</br>
</br>
</br>
<H1>
(solo gui) ROTTE
3 rotte get
1) copia di quella post ma in get con relativi accorgimenti (creata per essere passata alla gui)
2) rotta GET /stati :non prende parametri ma ritorna un vettore di stringhe contenente i valori presi dalla lettura, in scanner, del file Stati.csv
3) rotta GET /generi :non prende parametri ma ritorna un vettore di stringhe contenente i valori presi dalla lettura, in scanner, del file Generi.csv
queste due rotte sono utili per passare i valori nella GUI
</H1>
</br>
</br>
</br>
</br>
<H1>
(solo gui) 
1) La prima cosa che l'utente vede quando esegue l'eseguibile è la schermata Home
2) DUE PULSANTI PRINCIPALI: il pulsante ENTRA che permette di passare alla seconda schermata, nota come Filtraggio, ed il pulsante Exit che termina l'esecuzione del programma
(ovviamente, se si preme exit il prigramma spring in backend continua a runnare)
IMMAGINE 1 SCHERMATA HOME
3) Nella seconda pagina, che è la schermata di filtraggio, è possibile richiedere al programma di trovare gli eventi filtrati per: Stati e Generi, ed ottenere statistiche relative ad un periodo (opzione mensile non implementata); in questa schermata è possibile utilizzare il pulsante 'CERCA' che passa, alla schermata responso, i risultati filtrati mediante i paramentri inseriti
4) il pulsante 'Svuota' resetta tutte le scelte compiute 
5) il pulsante exit termina l'esecuzione del programma
6) il pulsante 'Home' torna alla prima schermata dell'app
IMMAGINE 2: SCHERMATA FILTRAGGIO IN GENERALE

7)in Stati: di default, la sezione 'Stati' presenta una comboBox in cui è possibile scegliere/inserire il nome dello Stato di Australia o New Zealand su cui si vuole fare la ricerca; 
8)è possibile scegliere anche più di uno Stato attraverso il pulsante + che aggiunge, ogni volta che lo si clicca (fino ad un massimo di 7), una comboBox tesa ad ospitare un'altro stato da filtrare.
9)è possibile scegliere tutti gli stati in un unico colpo scegliendo l'opzione 'tutti gli stati'
10) se si prova a fare la ricerca lasciando la combobox 'Stato' vuota, compare un popup di errore che ti impone di inserire tutti i campi(ovvero, di inserire almeno un valore in ogni combobox relativa ad ogni sezione: le sezioni sono stati, generi e periodo)
IMMAGINE 3: PIù COMBOBOX STATI
IMMAGINE 4: WARNING

7)in gENERI: di default, la sezione 'gENERI' presenta una comboBox in cui è possibile scegliere/inserire il nome genere su cui si vuole fare la ricerca; 
8)è possibile scegliere anche più di uno genere attraverso il pulsante + che aggiunge, ogni volta che lo si clicca (fino ad un massimo di 9), una comboBox tesa ad ospitare un'altro genere da filtrare.
9)è possibile scegliere tutti i generi in un unico colpo scegliendo l'opzione 'tutti i generi'
10) se si prova a fare la ricerca lasciando la combobox 'Genere' vuota, compare un popup di errore che ti impone di inserire tutti i campi(ovvero, di inserire almeno un valore in ogni combobox relativa ad ogni sezione: le sezioni sono stati, generi e periodo)
IMMAGINE 5: PIù COMBOBOX Generi
IMMAGINE 4: WARNING

11) in Periodo: la sezione 'Periodo' consente di scegliere (obbligatoriamente) una data iniziale ed una data finale, nel formato yyyy-mm-dd, attraverso delle combobox
12) ABBIamo il cazzo immenso perchè l'anno si aggiorna a seconda dell'anno corrente.
13) sono stati effetuati controlli sui giorni in relazione ai mesi (nel senso che, se si sceglie febbraio, è possibile andare dal giorno 1 al giorno 28; il software, poichè auto considera l'anno corrente, riconosce se l'anno è bisestile, ovvero riconosce se Febbraio ha 29 giorni piuttosto che 28)
14) sulle date è stato effettuato un controllo che visualizza un Warning nel caso in cui data iniziale >= data finale
IMMAGINE 6: DATE
IMMAGINE 7: WARNING DATE

13) Se non ci sono eventi per i filtri specificati (ovvero Stati e generi), viene visualizzato un popup con scritto 'Errore, non ci sono eventi disponibilo'
IMMAGINE 8: NON CE N'è EVENTI

14) uLTIMA SCHERMATA: permtte di visualizzare il responso relativo ai filtri inseriti nella schermata orecedente e presenta il pulsante 'Nuova Ricerca' che permette di tornare alla schermata filtraggio per effettuare una nuova ricerca
IMMAGINE 9: RESPONSO
</H1>

























## Software Utilizzati
La lista di software & tools impiegati per realizzare la Filter-App è la seguente:
* L'IDE [Eclipse](https://www.eclipse.org/downloads/), pacchetto [JDK](https://www.eclipse.org/downloads/download.php?file=/technology/epp/downloads/release/2020-12/R/eclipse-java-2020-12-R-win32-x86_64.zip), per la scrittura del codice dell'intero applicativo
* Il tool [Postman](https://www.postman.com/downloads/), strumento per il testing delle API, impiegato per gestire le chiamate `GET` e `POST` delle rotte 
* Il software [StarUML](https://staruml.io/), per la produzione dei Class Diagram e degli Use Case Diagram
* La piattaforma [GitHub](https://github.com/), per il versioning del codice, dell'UML e dell'interfaccia 
* La shell [Git Bash](https://git-scm.com/downloads), per eseguire il versioning del codice mediante terminale direttamente dalla cartella del progetto
* Il framework [JUnit 5](https://junit.org/junit5/), per lo Unit Testing dei metodi dell'applicativo
* L'applicativo [Javadoc](https://docs.oracle.com/javase/8/docs/technotes/tools/windows/javadoc.html), incluso nel pacchetto [JDK](https://www.eclipse.org/downloads/download.php?file=/technology/epp/downloads/release/2020-12/R/eclipse-java-2020-12-R-win32-x86_64.zip), utilizzato per la generazione automatica della documentazione del codice sorgente scritto in Java
* Il software [Excel](https://chrome.google.com/webstore/detail/excel-online/iljnkagajgfdmfnnidjijobijlfjfgnb?hl=it), per la scrittura dei file contenenti gli Stati ed i generi  che verranno letti dall'applicazione mediante Scanner in input
* L'editor [Adobe Photoshop](https://www.adobe.com/it/products/photoshop.html?mv=search&sdid=F89JZPN9&ef_id=CjwKCAiAmrOBBhA0EiwArn3mfP_7kq1glefG8WG81535fX8ZbsEgZssDK_qhCZf7tlCIY75OqgbsthoCLx0QAvD_BwE:G:s&s_kwcid=AL!3085!3!394417421007!e!!g!!photoshop%20download!1457478710!56999190912&gclid=CjwKCAiAmrOBBhA0EiwArn3mfP_7kq1glefG8WG81535fX8ZbsEgZssDK_qhCZf7tlCIY75OqgbsthoCLx0QAvD_BwE), per la produzione della grafica della GUI
* Il software [TeamViewer](https://www.teamviewer.com/it/?utm_source=google&utm_medium=cpc&utm_campaign=it|b|pr|20|jun|broad-brand-only-sn|free|t0|0&utm_content=broad_brand_only&utm_term=%2Bteamviewer&gclid=CjwKCAiAmrOBBhA0EiwArn3mfAkI6nkkj6gMzEJ_uzxCNLuNy9bJ_nA59-ERNvfdHMCxNi5W5pNjphoCUigQAvD_BwE), per la produzione e discussione del codice Java in team ed in contemporanea
* La piattaforma Voip [Discord](https://discord.com/download), per confronti di idee, comunicazioni e scambio materiale propedeutico allo sviluppo del codice (materiale che non è stato opportuno pubblicare su GitHub poichè di natura esclusivamente teorica)
* La piattaforma [Stack Overflow](https://stackoverflow.com/), per la risoluzione di alcune problematiche legate al coding dell'app o all'impiego di alcuni metodi o classi
* Il tool [Spring Inizializr](https://start.spring.io/), per la generazione del progetto 
* Il toolkit [JSON.simple](https://www.tutorialspoint.com/json_simple/json_simple_quick_guide.htm), per la decodifica, lettura e parsing dei file [JSON](https://www.json.org/json-it.html)
* Il framework [Spring](https://spring.io/), per l'esecuzione e sviluppo dell'applicazione Java
* Il progetto [Spring Boot](https://spring.io/projects/spring-boot), che consente di avviare l'applicazione attraverso un metodo main che, a sua volta, lancia il web server integrato
* L'IDE [Spring Tool Suite 4](https://spring.io/tools), per lo sviluppo di applicazioni Spring
* Il tool [Spring Web](https://spring.io/guides/gs/serving-web-content/), affinchè l'applicazione possa accettare richieste `HTTP` all'indirizzo `localhost:8080`
* Il tool [Apache Maven](https://maven.apache.org/), per la definizione della struttura del progetto mediante il file `pom.xml` 
* Il web server locale [Apache Tomat](https://spring.io/blog/2014/03/07/deploying-spring-boot-applications), per la gestione delle richieste `HTTP`

## Autori
La Filter-App 'The Last of Events' è stata sviluppata da:
* [Rocco Anzivino](https://github.com/RoccoAnzivino)
* [Kevin Giusti](https://github.com/KevinGiusti)
* [Kejvin Skiti](https://github.com/Kejvin)

**Contributi e ruoli**
Autore | Ruolo 
---- | ---- 
Rocco Anzivino | Sviluppo filtro Stati, sviluppo statistica relativa al numero massimo degli eventi in ciascuno Stato, sviluppo Scanner Stati, sviluppo eccezioni e controlli, produzione JavaDoc, ottimizzazione ed estensione Parser e Controller, sviluppo della base del codice, sviluppo dell'intera GUI 
Kevin Giusti | Sviluppo filtro periodo personalizzato, sviluppo statistiche relative a minimo, massimo e media eventi in un mese o periodo personalizzato a seconda degli Stati selezionati, sviluppo eccezioni e controlli, produzione JavaDoc, estensione Parser e Controller, produzione dell'intero readme, diagramma uml delle classi dell'api e dei casi d'uso, test JUnit 5
Kejvin Skiti | Sviluppo filtro generi, sviluppo statistica relativa al numero massimo di eventi raggruppati per genere in ogni Stato, sviluppo Scanner generi, sviluppo eccezioni e controlli, estensione Parser e Controller, diagramma uml delle classi e intera produzione del diagramma uml di sequenza

**Nota:** il numero di `commit` effettuati da ciascun membro del team **non** è indice del contributo apportato allo sviluppo dell'applicativo poichè, impiegando il software TeamViewer, molto frequentemente è accaduto che l'operazione di `push` venisse effettuata dal pc ospitante la condivisione dello schermo anche se, effettivamente, lo sviluppo del codice fosse imputabile all'operato di più persone.

<p>
</br>
</br>
</p>

<p>
 Gli sviluppatori</br>
 <i>Rocco Anzivino</i></br>
 <i>Kevin Giusti</i></br>
 <i>Kejvin Skiti</i></br>
 </p>
