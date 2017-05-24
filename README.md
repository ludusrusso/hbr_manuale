# Introduzione

Questo manuale fornisce un'introduzione all'utilizzo della piattaforma
Open Source di Cloud Robotics sviluppata da HotBlack Robotics.

La Cloud Robotics è un nuovo approccio alla robotica che è considerato da molti
come l'abilitatore della Robotica di Servizio. L'idea di base è quella di sfruttare
la potenza di internet per creare servizi robotici connessi, più intelligenti e più economici.

Pensate come esempio pratico alla piattaforma di Amazon per la consegna dei pacchi in modo autonomo utilizzando Droni. Ogni drone, per eseguire questo task, deve risolvere una serie di compiti complessi:

 -  conoscere la propria posizione e il punto di destinazione del pacco;
 - calcolare l'itinerario migliore per raggiungere il punto di consegna (considerando anche la presenza di palazzi, aree in cui è vietato volare, eccetera);
 - raggiungere il punto di destinazione in modo sicuro, quindi evitando possibili collisioni con ostacoli quali altri droni, palazzi alti non segnati nella mappa, eccetera;
 - atterare nel punto prestabilito senza far male a nessuno;
 - tornare al punto di partenza.

Tutto questo, come è facile immaginare, richiede una serie algoritmi molto complessi che, se messi sul drone, richiederebbero l'utilizzo di un server molto potente andando ad incidere sia sul peso del drone, che sulla batterie (che nei droni sono caratteristiche molto critiche).

Alternativamente, grazie alla Cloud Robotics, possiamo far girare sul drone solo quella parte processi critici, e remotizzare quelli più complessi. In questo modo
non avremo necessità di tantissime risorse sul robot e potremmo contare su una scheda di calcolo molto più semplice, economica, leggera e meno esosa di batteria.

## Cosa è una piattaforma di Cloud Robotics
Come per il Cloud Computing, per sviluppare Software di Cloud Robotics è necessario avere un framework di sviluppo ed un'infrastruttura basata su di esso.
