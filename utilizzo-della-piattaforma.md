# Utilizzo della piattaforma per la programmazione in ROS

Questo capitolo è dedicato all'introduzione di ROS \(Robot Operating System\) con la piattaforma di **HotBlack Robotics**.

> Questo capitolo suppone che is abbia già un Raspberry Pi correttamente

## Introduzione a ROS

ROS \(the Robot Operating System\) è uno dei framework più utilizzati ed apprezzati a livello mondiale per lo sviluppo di applicazioni di robotica di Servizio. Vanta una vastissima community di scienziati e sviluppatori in tutto il mondo, ed è diventato, in poco tempo, uno standard di fatto sia nella ricerca che nel mondo industriale.

Da un punto di vista puramente tecnologico, ROS non è un sistema operativo, ma una serie di componente software \(framework\) che fornisce funzionalità simili a quelle di un sistema operativo ma in un ambiente multi-macchina, rendendo trasparente al programmatore la parte di comunicazione tra programmi che si trovano sulla stessa macchina o su macchine diverse. In parole più semplici, quando si sviluppa un programma \(**nodo**\) in ROS, il programmatore non deve fare assunzioni sull'hardware su cui il nodo stesso verrà lanciato. Questa caratteristica di ROS abilita due importanti concetti della **Cloud Robotics**:

* **Astrazione dell'Hardware**: uno stesso **nodo** ROS può controllare \(con alcune limitazioni\) Hardware molto diversi tra loro, come un Robot bipede o un drone;
* **Intelligenza Remota**: è possibile sviluppare applicazioni la cui intelligenza \(capacità di calcolo\) non è completamente allocata sul robot stesso, ma gira \(in parte o completamente\) su un server remoto.

### Architettura e componenti base di ROS

Il sistema di comunicazione ROS si basa su due componenti principali: i **nodi** e i **topic**, che insieme formano un'applicazione robotica, anche detta **ROS graph**.

* I **Nodi **sono i processi che girano all'interno di un'applicazione ROS. Essi sono dei singoli programmi che girano all'interno di un'applicazione, e svolgono solitamente dei compiti ben determinati. I nodi possono essere classificati in due tipologie: **driver**, che comunicano direttamente con l'hardware \(come sensori e attuatori\), e **nodi di computazione**, che si occupano di implementare algoritmi per dare intelligenza al Robot. Ogni nodo è identificato tramite un nome all'interno della rete.
* I **Topic **sono** **i principali canali di comunicazione all'interno della rete ROS. Grazie ai topic, i nodi possono mandare e ricevere messaggi in modo da sincronizzarsi e sviluppare l'applicazione robotica in modo modulare. I **Topic**, in ROS, sono molto simili a dei canali TV \(o Radio\): un nodo può inviare contenuti tramite un topic \(in questo caso è detto **publisher**\) come fanno le emittenti televisive sui vari canali TV. Allo stesso modo, un nodo può sintonizzarsi su uno topic e ricevere questi dati \(questo nodo è detto **subscriber**\).

I Nodi, quindi, si scambiano informazioni tramite topic. Queste informazioni sono impacchettate all'interno di messaggi pre definiti: ogni topic è in grado di trasportare solo messaggi di un determinato **tipo**.

I **Tipi di messaggio** descrivono le strutture dati in cui vengono impacchettati i messaggi scambiati tramite topic. Questi sono predefiniti da ROS all'interno di pacchetti che raggruppano tipi di varia natura, di seguito alcuni esempi:

* **std\_msgs** è un pacchetto che raccoglie tipi standard. Al suo interno troviamo i tipi base, come **Bool**, **Int16**, **Float32**, **String**, i relativi Array e altri messaggi di questo tipo. Ognuno di questi messaggi è definito come struttura dati con all'interno un campo **data** del tipo specifico.
* **geometry\_msgs** raccoglie messaggi di tipo geometrico, come **Vector3 **\(che contiene all'interno tre campi: x, y, z\), **Twist**, che rappresenta la coppia velocità lineare e angolare in un mondo 3D, eccetera.

Ogni tipo di messaggio si indica con la seguente notazione `<nome pacchetto>/<nome tipo>` ad esempio `std_msgs/Uint16` .

## Scriviamo il nostro primo programma

Accediamo alla [piattaforma HBR](http://www.hotblackrobotics.com/cloud/index) e apriamo il tab **Sketches**. Creiamo quindi un nuovo programma chiamato **first\_sketch** ed editiamolo.

All'interno del file ci sarà un codice pre impostato che può essere usato come scheletro di partenza.

```py
import dotbot_ros
from sys import stdout

class Node(dotbot_ros.DotbotNode):
    node_name = 'node'

    def setup(self):
        print 'starting'
        stdout.flush()
        self.loop_rate = dotbot_ros.Rate(10)

    def loop(self):
        print 'loop'
        stdout.flush()
```

Di seguito analizziamo il codice in dettaglio.

Le prime due righe servono per importare moduli all'interno del programma. In particolare, importiamo interamente il modulo `dotbot_ros` e importiamo l'oggetto `stdout` dal modulo `sys` .

```py
import dotbot_ros
from sys import stdout
```

In seguito definiamo la classe `Node` ereditando da `dotbot_ros.DotbotNode` . Questa classe è il punto di partenza della codice ROS, ed, al suo interno, devono essere definite le funzioni `setup` e `loop`.

```py
class Node(dotbot_ros.DotbotNode):
    node_name = 'node'

    def setup(self):
        #...

    def loop(self): 
        #...
```

La variabile di classe `node_name = 'node'` definisce il nome \(univoco\) del nodo all'interno del mondo ROS. Vedremo in seguito qual è l'effetto di questa variabile.

La funzione `setup`, come per **Arduino**, è una funzione di inizializzazione che viene eseguita all'avvio del programma. Lo scopo di questa funzione è inizializzare le variabili e gli oggetti che verranno poi eseguiti durante il programma.

```py
    def setup(self):
        print 'starting'
        stdout.flush()
        self.loop_rate = dotbot_ros.Rate(10)
```

In questo caso, la funzione si occupa di stampare su shell la stringa _starting_ e di inizializzare la frequenza a cui eseguire la funzione loop. In questo caso, `loop` viene eseguita ciclicamente ad una frequenza di 10Hz `self.loop_rate = dotbot_ros.Rate(10)`. Attenzione, la variabile `self.loop_rate` deve essere definita, altrimenti la funzione `loop` non verrà mai eseguita.

La funzione `loop`, invece, viene eseguita ciclicamente \(se la variabile `self.loop_rate`è correttamente definita\). Questa si occupa di stampare su shell la stringa _loop_.

```py
    def loop(self):
        print 'loop'
        stdout.flush()
```

Notate che la funzione `print` è sempre accoppiata con la riga `stdout.flush()`, questo è necessario per forzare l'interprete python a flushare a video \(remoto\) il testo di print, altrimenti il testo viene visualizzato a video solo dopo la fine dell'esecuzione del programma.

#### Eseguire il programma

> Prima di eseguire un qualsiasi programma, dobbiamo essere collegati al robot.

Per eseguire il nodo, premiamo il tasto **Run** all'interno dell'applicazione, avendo cura di essere già connessi ad un robot.![](/assets/Schermata 2017-06-01 alle 12.00.172.png)Se tutto va a buon fine, si aprirà una finestra con l'output del programma. Come potete vedere, il programma scriverà sulla shell la stringa \_starting \_seguita poi dalle stringe \_loop \_ad una frequenza di 10Hz.

asd![](/assets/Schermata 2017-06-01 alle 12.00.20.png)Apriamo quindi un'altra finestra sul tab ROS \(in alto\) per accedere alla ROS console. Da qui possiamo notare che è apparso un nuovo nodo, chiamato `/<nome del vostro robot>/node`. Per stoppare il nodo, potete premere il tasto **kill node** riferito al nodo in questione.

![](/assets/Schermata 2017-06-01 alle 12.00.28.png)Una volta stoppato, ritornando alla finestra del programma, vedrete che il nodo ha finito di stampare a video, e che è apparsa la linea **shutdown request: user request**, che indica il fatto che il nodo è stato stoppato dall'utente.![](/assets/Schermata 2017-06-01 alle 12.00.39.png)

> Prima di rieseguire un programma, assicuratevi di aver stoppato il programma in esecuzione.

#### Esercizi

* Modificate la frequenza di esecuzione del programma, eseguitelo a 1Hz, 0.5Hz, 2Hz, 30Hz;
* Modificate il nome del nodo \(attenzione, in ROS i nomi non possono avere spazi e caratteri speciali\);
* Modificate il testo stampato a video.

### Miglioriamo il primo programma

Una volta verificato il funzionamento, andiamo a migliorarlo in modo da creare una variabile contatore che viene incrementata ad ogni ciclo, e stampare a video il valore di tale variabile.

Per far questo, all'interno della funzione `setup`, definiamo una variabile `self.cnt` inizializzata a 0

```py
    def setup(self):
        #...
        self.cnt = 0
```

Notare che abbiamo definito tale variabile all'interno dell'oggetto `self`. In questo modo, abbiamo reso tale variabile visibile anche alle altre funzioni all'interno della classe `Node`, e quindi anche alla funzione `loop`.

A questo punto, utilizziamo tale variabile nella funzione `loop`.

```py
    def loop(self):
        print 'loop, cnt =', self.cnt
        stdout.flush()
        self.cnt += 1
```

Questa funzione stampa la stringa _loop, cnt = _ concatenata al valore attuale di `self.cnt`, \(ricordarsi della chiamata di `stdout.flush()` dopo la chiamata di `print`\). Alla fine della funzione, il valore di `self.cnt` viene incrementato di 1.

#### Eseguire il programma

Come per il punto precedente, eseguiamo il programma. Noteremo che, a differenza di prima, il loop stamperà una stringa diversa ad ogni ciclo, in base al valore del contatore.![](/assets/Schermata 2017-06-01 alle 13.55.06.png)Ricordiamoci di killare il nodo prima di passare ai punti successivi del tutorial.

#### Esercizi

* Modificare il programma in modo che, ad ogni ciclo, `self.cnt` venga incrementato di 5;
* Modificare il programma in modo che, ad ogni ciclo, `self.cnt` venga decrementato di 2.

### Implementiamo un semplice Publisher

Siamo ora pronti ad implementare un nodo publisher, cioè un nodo che pubblica su un topic ROS. Per farlo, dobbiamo fare 3 operazioni:

1. Importare all'interno del programma il tipo di messaggio che andremo ad utilizzare;
2. Creare un oggetto publisher, che si occupa di gestire la comunicazione con il topic;
3. Pubblicare i dati nel loop.

Avendo già a disposizione la variabile `self.cnt`, usiamo questa per generare i dati da pubblicare nel topic. Pubblicheremo quindi dati di tipo intero nel topic e, per questo motivo, useremo il tipi `std_msgs/Int32`.

Per importare questo tipo, aggiungiamo la seguente riga all'inizio del programma \(cove ci sono gli altri import\):

```py
from std_msgs.msg import Int32
```

A questo punto, siamo pronti a creare il pubblicatore: infatti la costruzione di questo oggetto richiede due parametri:

* il nome del topic su cui deve pubblicare i dati;
* il tipo di messaggi che questo topic gestisce.

All'interno della funzione setup, quindi, creiamo la variabile `self.pub_cnt` nel seguente modo:

```py
    def setup(self): 
        #... 
        self.pub_cnt = dotbot_ros.Publisher('counter', Int32)
```

Si noti che, anche in questo caso, utilizzo l'oggetto `self` per poter utilizzare il pubblicatore anche all'interno della funzione `loop`.

A questo punto, non ci resta che pubblicate la variabile `self.cnt` all'interno di ogni ciclo, andando ad aggiungere questa linea di codice all'interno della funzione `loop` \(prima di incrementare il valore di `self.cnt`\):

```py
    def loop(self): 
        #...
        self.pub_cnt.publish(self.cnt)
        self.cnt += 1
```

#### Eseguire il programma

Eseguendo il programma, l'output su shell sarà esattamente identico a quello precedente. Tuttavia, accedendo al tab **ROS** \(dopo aver aggiornato la pagina\), noteremo la presenza di un nuovo topic chiamato `/<nome robot>/couter` , Il cui tipo è `std_msgs/Int32`. Cliccando sul tasto **echo** in corrispondenza di questo topic, apparirà un tab che farà vedere i messaggi scambiati all'interno del topic stesso.![](/assets/Schermata 2017-06-01 alle 13.58.56.png)Si noti che i messaggi inviati non contengono direttamente il numero, ma sono una struttura con all'interno un elemento \(data\) in cui viene inserito il valore del numero inviato. La maggior parte dei messaggi nel pacchetto `std_msgs` sono definiti in questo modo.

### Implementiamo un semplice Subscriber

A questo punto, sappiamo come inviare dati all'interno del mondo ROS. Vediamo ora il task complementare, cioè la ricezione dei dati per mezzo dell'oggetto subscriver.

Creiamo quindi un altro programma, chiamato simple\_subscriber, all'interno della piattaforma HBR. Andiamo quindi a lavorare all'interno del programma.

Questo programma dovrà semplicemente sottoscriversi al topic `couter` e stampare a video il valore dei messaggi ricevuti. Per questo motivo, possiamo rimuovere la funzione `loop`  \(e di conseguenza la variabile `self.loop_rate`\) dal codice.

Cambiamo inoltre il nome del nono in `simple_pub`, in modo da evitare conflitti con il nodo precedente.

```py
import dotbot_ros
from sys import stdout
class Node(dotbot_ros.DotbotNode):
    node_name = 'simple_pub'

    def setup(self):
        print 'starting'
        stdout.flush()
```

Dobbiamo quindi implementare una funzione che si arriva solamente nel momento in cui un nuovo messaggio viene inviato sul topic. Per far questo, ci viene in aiuto una tecnica di programmazione chiamata **callback**.

Definiziamo una nuova funzione \(all'interno dell'oggetto `Node`\) chiamata coutner\_cb, come segue

```py
   def counter_cb(self, msg):
        print 'ho ricevuto', msg.data
        stdout.flush()
```

Questa funzione prende due parametri. Il primo \(obbligatori in python\) è `self`, e serve semplicemente per permettere a questa funzione di accedere a variabili definite in altre funzioni. Il secondo argomento, `msg`, sarà riempito automaticamente da ROS con il messaggio inviato attraverso il topic. 

L'ultimo passaggio è quello di connettere questa funzione al topic `counter` per mezzo di un **Subscriber**.

Per far questo, all'interno della funzione setup, definiamo un oggetto **Subscriber **come segue:

```py
#...
from std_msgs.msg import Int32

class Node(dotbot_ros.DotbotNode):
    node_name = 'simple_pub'

    def setup(self):
        #...
        self.sub_cnt = dotbot_ros.Subscriber('counter', Int32, self.counter_cb)
```

Il costruttore di `Subscriber` prende 3 argomenti:

* il nome del topic a cui si deve sottoscrivere
* il tipo di messaggio del topic
* la funzione da chiamare quando un messaggio viene ricevuto.

Ricordiamoci di importare il tipo `Int32`, come visto precedentemente.

Il codice completo del programma è quindi il seguente:

```py
import dotbot_ros
from sys import stdout

from std_msgs.msg import Int32

class Node(dotbot_ros.DotbotNode):
    node_name = 'simple_pub'

    def setup(self):
        print 'starting'
        stdout.flush()
        self.sub_cnt = dotbot_ros.Subscriber('counter', Int32, self.counter_cb)

    def counter_cb(self, msg):
        print 'ho ricevuto', msg.data
        stdout.flush()
```

#### Eseguire il programma

Assicurandoci che il programma precedente sia in esecuzione, eseguiamo anche questo secondo programma appena implementato.

Noterete che, quando il programma riceve un dato, viene stampato tale dato sulla console.![](/assets/Schermata 2017-06-01 alle 14.17.46.png)Inoltre, se provate a killare il nodo precedente, vi accorgerete che il secondo programma non farà più niente, in quanto nessuno gli invierà messaggi.

