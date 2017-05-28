# Capitolo 1. Configurare il Raspberry

Questo capitolo è dedicato alla configurazione del Raspberry Pi per iniziare a sviluppare applicazione di Cloud Robotics utilizzando la piattaforma robotica di **HotBlack Robotics**.

## Scheda SD del Raspberry Pi

Il primo passo, consiste nel configurare la scheda SD che contiene il sistema operativo **HBrain**.  
La scheda SD è l'Hard Disk del Raspberry Pi. È il componente principale che abilita la parte software del Raspberry, ed è quindi essenziale per il funzionamento del sistema stesso. Un Raspberry Pi senza una scheda SD correttamente configurata semplicemente non funziona.

La procedura di configurazione della scheda permette, essenzialmente, ci copiare all'interno della SD un sistema operativo già configurato e funzionante, a partire da una copia digitale di tale sistema \(detta immagine\). Ovviamente nulla vieta di crearsi il proprio sistema operativo, ma è un'operazione molto sconsigliata in quanto richiede forti competenze Linux.

Quello che andremo a fare, sarà quindi scaricare e clonare all'interno della SD che andremo ad inserire nel Raspberry, l'immagine del sistema operativo HBrain, che è il sistema operativo sviluppato da HotBlack Robotics, già configurato per funzionare con ROS e la piattaforma **HBR**.

### Download dell'immagine della SD

Per scaricare l'immagine SD accedete a questo [link](https://sourceforge.net/projects/hbrain/) e scaricare l'ultima versione del'immagine cliccando sul tasto **Download**.

![Download Image SD](img/chapter1/download-hbrain.png)

Il download richiederà un po' di tempo, in quanto il file da scaricare pesa più di 1GB di dati.

Una volta scaricato, è necessario coinfigurarlo seguendo la guida relativa al vostro sistema operativo, seguendo le guide sotto.

### Donwload del programma **Etcher** per la scrittura della SD

[Etcher](https://etcher.io) è un programma multipiattaforma che semplifica la procedura di scrittura di una SD a partire da un'immagine! Etcher è multipiattaforma, e suporta Windows, Linux e macOS. Per scaricarlo, accedete al sito [etcher.io](https://etcher.io) e cliccate sul tasto download. Quindi eseguite l'installazione lanciando il file scaricato.

![Sito Etcher](img/chapter1/etcherio.png)

### Scrittura della SD

Avrete ora tutto il necessario per eseguire la procedura di scrittura, ovviamente servirà avere in possesso una scheda SD \(da almeno 4GB di spazio\).

Inserite la SD nel computer e aprite il programma Etcher.  
![Uso di Etcher](img/chapter1/etcher1.png)

Selezionate l'immagine della scheda SD scaricata precedentemente.

![Uso di Etcher](img/chapter1/etcher2.png)

Selezionate la scheda SD su cui scrivere l'immagine

> per evirare confusioni, scollegate tutti gli altri dispositivi connessi al computer.

A questo punto, potete flashare la SD. Il tempo di scrittura può durare da uno a 10 minuti in base alla velocità di scrittura della SD.

Una volta che la procedura sarà completa, estrarre la SD ed inserirla all'interno del Raspberry Pi 3 Model B. Siamo pronti per configurare il sistema.

## Configurazione del Raspberry Pi

Inserita la scheda SD all'interno del Raspberry Pi 3 model B, vediamo insieme come collegarci ad esso tramite la piattaforma di Cloud Robotics. Al primo avvio, è necessario attaccarsi al Raspberry fisicamente da Ethernet. Tuttavia, una volta configurato correttamente il Wifi, il Raspberry sarà in grado di connettersi autonomamente alla rete domestica quando acceso.

### Registrazione alla piattaforma di Cloud Robotics

Per accedere alla piattaforma di HBR, è necessario prima di tutto registrarsi gratuitamente. Per farlo, basta eccedere al sito [www.hotblackrobotics.com](http:://www.hotblackrobotics.com) e cliccare sul tasto **Resgister** in alto a sinistra.![](/assets/Schermata 2017-05-26 alle 11.52.00.png)Compilare il form con i dati richiesti ed inserire la vostra mail ed un password per collegarvi.![](/assets/Schermata 2017-05-26 alle 12.04.14.png)

### Prima connessione

Attacchiamo il Raspberry al nostro Router domestico \(con un cavo Ethernet\) e quindi colleghiamolo all'alimentazione.

Apriamo il browser da un computer collegato alla stessa rete a cui abbiamo connesso il Raspberry Pi, e accediamo alla piattaforma di cloud robotics **HBR**, dalla pagina [http://www.hotblackrobotics.com/cloud](http://www.hotblackrobotics.com/cloud).

Clicchiamo sul tasto **cerca robot**![](/assets/Schermata 2017-05-26 alle 14.06.33.png)Se tutto va bene, dovremmo vedere apparire, nella tabella sottostante, un robot chiamato **hotbot**. Clickiamo quindi sul tasto **connect** accanto al nome del robot.

![](/assets/Schermata 2017-05-26 alle 14.08.00.png)Una volta connessi al robot, refreshamo la pagina, in alto a sinistra apparirà un nuovo pulsante chiamato **Robot**. Clickando sul pulsante accederemo ad una nuova pagina di informazioni sul robot stesso. Siamo finalmente riusciti a connetterci al Robot.![](/assets/Schermata 2017-05-26 alle 14.08.07.png)

### Configurare una rete WiFi

Per poter utilizzare il Raspberry Pi senza il cavo Ethernet, è importante configurare correttamente la rete WiFi. Per farlo, una volta connessi al robot, accediamo al tab **Robot **e poi premiamo sul tasto **Configure Wifi**.![](/assets/Schermata 2017-05-26 alle 16.16.03.png)Nella schermata che vi appare, vedrete che esiste già la configurazione per la rete **dotbot**, che è una rete WiFi a cui i nuovi robot si collegano di default. Potete tranquillamente cancellare la rete, premendo sul tasto **clean**, o decidere di tenerla attiva.

A questo punto, premente sul pulsante **configure** di uno dei blocchi liberi \(di default, il sistema può memorizzare fino ad un massimo di 5 wifi\).![](/assets/Schermata 2017-05-26 alle 16.17.27.png)Vi apparirà, quindi, una nuova schermata che eseguirà automaticamente la scansione delle reti wifi disponibili. Selezionate la rete alla quale volete connettervi cliccando sul tasto **select** accanto al nome della rete.![](/assets/Schermata 2017-05-26 alle 16.17.37.png)Vi verrà quindi chiesto di inserire la password della rete. Inseriamola e premiamo sul tasto **Submit**.![](/assets/Schermata 2017-05-26 alle 16.17.50.png)

Il robot verificherà che la password inserita sia corretta, e quindi ritorneremo alla pagina iniziale in cui potrete vedere che la nuova rete wifi è stata inserita correttamente.

![](/assets/Schermata 2017-05-26 alle 16.17.59.png)A questo punto, ritorniamo sul tab Robot e riavviamo il Robot premendo sul tasto **Reboot**. Durante il riavvio, staccate il cavo Ethernet: il robot si connetterà automaticamente alla rete configurata.

### Settare un nome del Raspberry \(opzionale\)

Se si prevede di lavorare in ambienti con più di un robot connessi alla stessa rete, è importante cambiare nome al robot stesso in modo da poterlo distinguere dagli altri. È inoltre possibile cambiare nome al robot solo per gusto personale e per personalizzarlo.

Per fare questo, dal pannello **Robot**, digitiamo il nome desiderato nell'apposito pannello, e premiamo il tasto **Set Name**.

> Attenzione: il nome deve contenere solo lettere e numeri, non deve contenere caratteri speciali o spazi

 ![](/assets/Schermata 2017-05-26 alle 14.08.26.png)A questo punto, riavviate il robot! Dalla prossima accensione, il nome del robot sarà quello settato da voi!



### 



