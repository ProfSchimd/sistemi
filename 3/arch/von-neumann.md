# Architettura di von Neumann

Nell'immagine sotto si vede uno schema dell'architettura di von Neumann. Essa è composta dalla **CPU** (*Central Processing Unit*) la quale è collegata alla **memoria** (chiamata anche **RAM** - *Random Access Memory*) ed ai dispositivi di **I/O** (*Input/Output*) tramite il **Bus di sistema** che possiamo immaginare come un insieme di “cavi” di collegamento. 

:::{figure} /3/img/von-neumann.svg
Schema generale dell'architettura di von Neumann. Un *bus di sistema* connette i tre componenti fondamentali *CPU*, *memoria RAM* e *I/O*.
:::

Una caratteristica importante dell'architettura di von Neumann è che le **istruzioni del programma da eseguire sono memorizzate nella stessa memoria (la RAM) che contiene i dati**. Si parla quindi di architettura a **programma memorizzato** (*stored program*) che differisce da architettura a **programma fisso** (*fixed memory*). Le architetture a programma fisso sono utilizzate in dispositivi che fanno una cosa specifica quali: calcolatrici (non programmabili), lavatrici, ... Le architetture a programma memorizzato (come l'architettura di von Neumann) sono utilizzate in quasi tutti i dispositivi programmabili: computer, smartphone, tablet, Arduino, console, ...

## Come funziona l'architettura di von Neumann

Un sistema basato sull'architettura di von Neumann utilizza il **fetch-and-execute** (recupera ed esegui) per eseguire un programma. Le istruzioni che compongono il programma si trovano in sequenza nella RAM (il sistema operativo le *carica* quando il programma il programma viene avviato). Ogni programma ha una prima *istruzione* (in Java questo è l'inizio del metodo `Main`). La CPU, partendo da questa *prima istruzione*, procede nel seguente modo

1. Recupera (*fetch*) dalla RAM la prossima istruzione da eseguire
2. Legge (*decode*) questa istruzione per capire cosa deve fare
3. Se necessario, carica gli operandi (*operands*) dalla memoria
4. Esegue l'istruzione (*execute*)
5. Ritorna al punto 1.

Questo funzionamento prosegue fino a che la CPU non viene *interrotta*. Il funzionamento sarà più chiaro quando parleremo di [CPU e Assembly](cpu.md).

## Le componenti dell'architettura di von Neumann
Vediamo ora in dettaglio qual'è il compito delle quattro componenti principali dell'architettura di von Neumann: CPU, memoria, I/O e bus.

### CPU
La **CPU** (*Central Processing Unit*) è il "cervello" di un calcolatore. Si tratta di un sistema molto complesso in grado di eseguire istruzioni relativamente semplice (ad esempio somma di numeri, spostamento di numeri, confronto tra numeri, ...) ad una velocità elevatissima. Ad esempio, una CPU moderna può fare 1 miliardi di somme tra interi in un secondo. L'insieme delle istruzioni che una CPU è in grado di eseguire viene detto **Instruction Set Architecture (ISA)** e rappresenta i mattoni con i quali *tutti i programmi* vengono eseguiti. La sequenza di istruzioni che una CPU deve eseguire rappresenta il *programma* che deve essere memorizzato da qualche parte. Nell'architettura di von Neumann il programma è memorizzato nella *memoria centrale* (la RAM) sotto forma di *codice macchina*, una dell idee rivoluzionarie dell'architettura di von Neumann è quella di tenere sulla stessa memoria sia il programma sia i dati che questo elabora.

### Memoria centrale
La **memoria centrale** è un "contenitore" di informazioni (*bit*). Nell'architettura di von Neumann la memoria centrale contiene i **dati** (ad esempio una sequenza di numeri da sommare) e le **istruzioni**. Le istruzioni sono le operazioni fondamentali che la CPU è in grado di eseguire. Mettendo tante istruzioni uno dopo l'altra si crea un programma.

### Bus
Siccome la CPU deve prendere dati e istruzioni dalla memoria, queste due componenti devono essere collegate. Il "filo" che le collega di chiama **bus di sistema**. Si tratta di un vero e proprio collegamento (visibile anche nel parte inferiore di una scheda madre) che permette a CPU e memoria di scambiarsi informazione (*bit*). È importante ricordare che la CPU può sia leggere che scrivere sulla memoria. Ad esempio la CPU legge dalla memoria due variabili $x$ ed $y$, le somma e poi scrive sulla memoria il risultato $x+y$.
Nei sistemi di elaborazione moderni, il bus di sistema è composto di tre bus.

1. **Bus indirizzi** che viene usato dalla CPU per indicare l'indirizzo di memoria a cui si vuole accedere (in lettura o in scrittura)
2. **Bus dati** che viene usato dalla CPU e dalla memoria per scambiarsi i dati
3. **Bus di controllo** che serve alla CPU, alla memoria ed ai dispositivi di I/O per gestire e coordinare le varie operazioni che fanno funzionare il sistema.

### I/O
Quanto abbiamo visto finora (CPU, memoria e bus) basta per creare una calcolatore. In pratica, però, è necessario leggere input (ad esempio dalla tastier) e/o mostrare output (ad esempio sullo schermo). Questo operazioni di **Input/Output** o **I/O** sono gestite da dei *controller* che sono collegati alla CPU e alla memoria attraverso il bus di sistema.