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

