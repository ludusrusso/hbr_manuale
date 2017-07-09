# Costruire l'Hardware O|Robot101

In questa guida, vedremo come costruire il robot O|Robot 101 base.

## Componenti

![Componenti](assets/hw/IMG_2536.JPG)

I componenti del robot sono suddivisi in 3 categorie:

 - Intelligenza
 - Elettromeccanica
 - Meccanica

### Intelligenza

Comprende i seguenti componenti, già presenti nel Kit:

 - Raspberry Pi 3 Model B
 - micro SD Card con OS Preinstallato
 - Battery Bank USB

![Componenti](assets/hw/IMG_2539.JPG)


### Elettromeccanica

Comprende i seguenti componenti, già presenti nel Kit:

 - 2 Motori DC con Ruote
 - Breadboard (scheda di sperimentazione)
 - Portabatterie (richiede 4 pile stilo AA)
 - Ruotino pivotante
 - Driver Motor

![Componenti](assets/hw/IMG_2537.JPG)

### Meccanica

Comprende i seguenti componenti, da stampare in 3D:

 - Case Robot
 - porta Breadboard
 - porta Raspberry Pi

![Componenti](assets/hw/IMG_2538.JPG)

## Montaggio

Vediamo come montare il robot.

### 1. Porta batterie

Insieriamo 4 pile stilo tipo AA all'interno del porta batterie.

![Componenti](assets/hw/IMG_2540.JPG)

Chiudiamo il portabatterie.

![Componenti](assets/hw/IMG_2541.JPG)

Incastriamo il portabatterie nell'apposito spazio all'interno del case del robot.

![Componenti](assets/hw/IMG_2542.JPG)

Facciamo passare i fili di alimentazione all'interno dell'apposito foro.

![Componenti](assets/hw/IMG_2543.JPG)

### 2. Motori

Inseriamo i motori nel case, stando attenti a far passare i fili di alimentazione dall'apposito foro.

![Componenti](assets/hw/IMG_2544.JPG)

![Componenti](assets/hw/IMG_2545.JPG)

### 3. Battery Pack

Facciamo scivolare il battery pack all'interno dello spazio circolare nel case del robot. Il lato con i fori per l'ingresso USB deve essere rivolto verso sinistra. (si veda foto). Il cavo USB deve essere fatto passare attraverso l'apposito foro.

![Componenti](assets/hw/IMG_2546.JPG)

**Attenzione**: posizionate l'interruttore su OFF.

![Componenti](assets/hw/IMG_2547.JPG)

### 3. Ruota Pivotante

Adagiamo l'alloggiamento della ruota pivotante nello spazio a lei predisposto del case.

![Componenti](assets/hw/IMG_2548.JPG)

Con l'aiuto di un cacciavite a stella, avvitiamo l'alloggiamento con le due vite in dotazione, anchè sia ben saldo al case del robot.

![Componenti](assets/hw/IMG_2549.JPG)

Incastriamo quindi il ruotino di metallo all'interno dell'alloggiamento.

![Componenti](assets/hw/IMG_2551.JPG)

![Componenti](assets/hw/IMG_2552.JPG)

### 4. Ruote Motori

Incastriamo le due ruote motori agli alberi dei motori DC.

![Componenti](assets/hw/IMG_2553.JPG)

Una volta girato, il robot dovrebbe essere stabile.

![Componenti](assets/hw/IMG_2554.JPG)

### 5. Breadboard

Incastriamo la breadboard all'interno del proprio alloggiamento.

![Componenti](assets/hw/IMG_2555.JPG)

![Componenti](assets/hw/IMG_2556.JPG)

Incastriamo quindi la breadboard e il proprio alloggiamento all'interno dell'apposita scalanatura nel case del robot.

![Componenti](assets/hw/IMG_2557.JPG)

### 5. Raspberry

Incastriamo l'alloggiamento del raspberry Pi all'interno dell'apposita scalanatura sul case del robot.

![Componenti](assets/hw/IMG_2558.JPG)

Inseriamo la scheda micro SD all'interno del Raspberry Pi

![Componenti](assets/hw/IMG_2559.JPG)

![Componenti](assets/hw/IMG_2560.JPG)

Adagiamo il Raspberry Pi all'interno dell'alloggiamento.

![Componenti](assets/hw/IMG_2561.JPG)

![Componenti](assets/hw/IMG_2562.JPG)

### 5. Driver Motori

Inseriamo il driver motori sul Raspberry Pi, incastrandolo (come in figura) nei GPIO.  

![Componenti](assets/hw/IMG_2563.JPG)

![Componenti](assets/hw/IMG_2564.JPG)

Colleghiamo i due cavi di alimentazione dei motori all'interno dei morsetti del driver, i fili rossi devono essere interni, quelli neri esterni.

![Componenti](assets/hw/IMG_2565.JPG)

Colleghiamo quindi i fili di alimentazione della batteria ai due morsetti interne del driver. **ATTENZIONE**, il cavo nero deve essere collegato al morsetto **GND**, il cavo rosso al morsetto **VIN**.

![Componenti](assets/hw/IMG_2566.JPG)

## Accensione

Per accendere il raspberry pi, collegate l'USB al Raspberry!

![Componenti](assets/hw/IMG_2567.JPG)
