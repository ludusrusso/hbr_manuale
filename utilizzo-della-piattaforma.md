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
* I **Topic **sono** **i principali canali di comunicazione all'interno della rete ROS. Grazie ai topic, i nodi possono mandare e ricevere messaggi in modo da sincronizzarsi e sviluppare l'applicazione robotica in modo modulare. I **Topic**, in ROS, sono molto simili a dei canali TV \(o Radio\): un nodo può inviare contenuti tramite un topic \(in questo caso è detto **pubblicatore**\) come fanno le emittenti televisive sui vari canali TV. Allo stesso modo, un nodo può sintonizzarsi su uno topic e ricevere questi dati \(questo nodo è detto **subscriber**\).

I Nodi, quindi, si scambiano informazioni tramite topic. Queste informazioni sono impacchettate all'interno di messaggi pre definiti: ogni topic è in grado di trasportare solo messaggi di un determinato **tipo**.

* I **Tipi di messaggio** descrivono le strutture dati in cui vengono impacchettati i messaggi scambiati tramite 



