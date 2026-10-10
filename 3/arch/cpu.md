# Central Processing Unit (CPU)

La **CPU** (**Central Processing Unit** - *unità centrale di elaborazione*) rappresenta il "cervello" di un calcolatore ed esegue le **istruzioni** che compongono un *programma*. Tali istruzioni sono molto semplici ad esempio: 
* somma due numeri,
* salva un numero in memoria,
* leggi un carattere dalla tastiera.

L'insieme delle istruzioni che una CPU è in grado di eseguire si chiama **Instruction Set Architecture ISA** (ISA) (*repertorio di istruzioni*), tale insieme dipende dal come la CPU è organizzata internamente (**micro-architettura**). Ad esempio, se una CPU non ha un circuito per dividere due numeri, la CPU non ci sarà l'istruzione di divisione. In questo caso si dovrà scrivere una sequenza di istruzioni (un *algoritmo*) per fare la divisione usando solo operazioni presenti nell'ISA.

Anche se CPU diverse (es. Intel vs Apple Silicon) hanno micro-architetture diverse, tutte contengono tre componenti fondamentali:
1. Una spazio di memoria interno composto da **registri** (**register file**);
2. Una sparte che opera il **controllo** (**control**) della CPU;
3. Un componente per operazioni aritmetiche e logiche (**Arithmetic Logic Unit, ALU**).

Il controllo della CPU comanda tutti i circuiti interni per eseguire l'*istruzione corrente*. Il controllo comprende:
* un registro chiamato **Program Counter** (**PC**) che contiene *l'indirizzo di memoria delle prossima istruzione che la CPU deve eseguire*;
* un registro chiamato **Instruction Register** (**IR**) che contiene l'istruzione da *decodificare*;
* Un circuito di decodifica (**decode**) che configura i circuiti per l'esecuzione dell'istruzione presente nell'IR;
* Altri registri e circuiti per accedere alla memoria e all'I/O.

:::{figure} /3/img/cpu-internal.svg
Schema interno della CPU. Lo schema evidenzia la presenza all'interno della CPU troviamo il *control* che si occupa del recupero e decodifica delle istruzioni, il *register file* per la memoria interna della CPU (i registri) e la Arithmetic Logic Unit (ALU) per l'esecuzioni delle operazioni aritmetico-logiche.
:::

## Ciclo di funzionamento della CPU
Durante il suo funzionamento, la CPU esegue continuamente il ciclo di **fetch-and-execute** (*recupera ed esegui*). Questo ciclo prevede le seguenti operazioni
1. Recupera (*fetch*) il codice della prossima istruzione da eseguire
2. Decodifica (*decode*) il codice recuperato per determinare quale operazione eseguire
3. Recupera gli operandi (*operand fetch*) se questi sono necessari per l'esecuzione dell'istruzione
4. Esegue (*execute*) l'istruzione decodificata nel passaggio 2
5. Scrive (*write*) il risultato dell'operazione se richiesto dall'istruzione

Possiamo rappresentare questo ciclo di funzionamento utilizzando un *automa a stati finiti* dove ciascuno stato rappresenta una delle fasi di esecuzioni dell'istruzione. Una *transizione* da uno stato ad un altro esiste se, durante l'esecuzione, si passa direttamente da una fase ad un altra.

:::{figure} /3/img/cpu-finite-control.svg
Schema che rappresenta l'*automa a stati finiti* che descrive il ciclo *fetch-and-execute* della CPU. Lo stato *instruction fetch* (evidenziato in blu) rappresenta l'inizio dell'esecuzione di una istruzione.
:::

```{tip} Osserva
Lo schema sopra permette che un'istruzione possa essere eseguita anche saltando la fase *operand read* e/o saltando la fase *write*. Notiamo anche che le fasi *instruction fetch*, *decode* e *execute* non possono essere saltate.
```

Vediamo più in dettaglio come la CPU esegue il *fetch-and-execute* attivando opportunamente i componenti che sono stati descritti sopra. Negli esempi si userà istruzione assembly 
```asm
add R1, [0x3D] # Somma a R1 il valore in MEM[0x3D] scrivendo il risultato in R1
```
presa da un'ISA inventata. L'istruzione svolge la seguente operazione:

> somma il valore nel registro `R1` al valore nella cella di memoria di indirizzo `0x3D` e metti il risultato di questa somma nel registro `R1`.

:::{attention} Attenzione
Ricordiamo che `0x3D` è un numero *esadecimale* corrispondete al numero decimale `61`. Il prefisso `0x` si usa in molti linguaggio per indicare un numeri esadecimali (*hex*). Ad esempio 
```java
int a = 100;
int b = 0x100;
System.out.println(a + " " + b); // stampa "100 256"
```
:::

(fetch)=
### Fetch dell'istruzione
Per eseguire le istruzioni, la CPU le deve recuperare della memoria RAM. A questo scopo, la CPU utilizza i seguenti registri:
* il **Program Counter, `PC`**  (*contatore di programma*) e
* l'**Instruction Register, `IR`** (*registro di istruzione*).
* il **Memory Address Register `MAR`** e il **Memory Data Register, **Memory Data Register `MDR`** per l'accesso alla memoria.

Il *fetch* delle istruzioni si compone delle seguenti fasi.
1. Il valore che è nel `PC` viene copiato nel `MAR` e si attiva la linea `Read` sul bus controllo.
2. Il valore richiesto passa dalla RAM al bus dati e poi nel `MDR`.
3. Il valore nel `MDR` viene copiato nell'`IR`.
4. Il valore del PC viene incrementato in modo che sia pronto per la prossima istruzione (per ISA a 64 bit l'incremento è di 8).

```{note} Parola di memoria
La *parola di memoria* indica, tra le altre cose, di quanto deve essere incrementato il `PC`. Infatti il `PC` contiene il *byte* (indirizzo) della memoria in cui inizia la prossima istruzione. Per passare alla prossima istruzione incrementare il `PC` di tanti byte quanto è grande un'istruzione cioè tanti byte quanto è grande la parola di memoria. Per un'architettura a 64 bit la parola di memoria è di 8 byte, per un'architettura a 32 bit la parola di memoria è di 4 byte.
```

#### Esempio di fetch

:::{figure} /3/img/cpu-internal-fetch.svg
Esempio di esecuzione della fase di *fetch*.
1. Il `PC` contiene l'indirizzo `OxA0` che arriva alla RAM attraverso il `MAR` ed il bus indirizzi.
2. La RAM recupera il valore (in questo caso `0x04`) che viene copiato nel `MDR`.
3. Il valore dal `MDR` viene copiato nell'`IR`.
4. Il PC viene incrementato per il *fetch* della prossima istruzione.
:::

### Decodifica dell'istruzione
Dal momento che una CPU può eseguire diversi tipi di istruzione (somma, sottrazione, ...), è necessario “decidere” quale operazione eseguire sulla base dell'istruzione recuperata durante il [*fetch*](#fetch). 

La **decodifica** delle istruzioni si compone delle seguenti fasi.
1. Il valore presente nell'`IR` viene elaborato dal circuito di decodifica.
2. Il circuito di decodifica identifica l'operazione da eseguire.
3. Se necessario, attiva i circuiti per la lettura degli operandi dalla memoria.
4. Se necessario, attiva i registri (dal *register file*) coinvolti nell'istruzione.
5. Se necessario, attiva i circuiti della ALU per eseguire l'operazione *codificata* nell'istruzione.

#### Esempio di decodifica

:::{figure} /3/img/cpu-internal-decode.svg
Esempio di esecuzione della fase di *decode*.
1. Il circuito di Decode riceve l'istruzione dall'`IR`.
2. L'istruzione viene decodificata e tradotta in un'operazione. Nell'esempio l'istruzione aggiunge (`add`) al valore in `R1` il valore nella cella di memoria di indirizzo `0x3D` (nella pratica il codice sarebbe più lungo di `0x04`).
3. Dovendo recuperare *operandi* dalla memoria, viene messo nel `MAR` l'indirizzo `0x3D` ed attivata la linea `Read` del bus controllo.
4. La CPU sa che deve portare verso la ALU (dove verrà fatta l'addizione) il valore presente nel registro `R1`.
5. La CPU attiva il circuito dell'ALU per l'addizione.

A questo punto manca il valore proveniente dalla memoria che però viene recuperato nella successiva fase di *lettura degli operandi*.
:::

### Lettura degli operandi
Molte istruzioni hanno bisogno di **operandi** di input, ad esempio per sommare due numeri abbiamo bisogno proprio di questi numeri da sommare (gli *addendi*). Questi operandi possono trovarsi nei registri oppure nella memoria. L'operazione (non sempre necessaria) di recupero degli operandi dalla memoria, prende il nome di *lettura (read) degli operandi* ed avviene utilizzando i meccanismi di accesso alla RAM ed i registri `MAR` e `MDR`. È importante notare che questa operazione potrebbe non essere necessaria, ad esempio se gli operandi si trovano già nei registri.
Il *read* degli operandi si compone delle seguenti fasi (le prime due fasi sono già state svolte durante il decode).
1. L'indirizzo da dove prendere il primo operando viene messo nel `MAR`.
2. Viene attivata la linea `Read` del bus controllo.
3. Si attende che il dato arrivi al `MDR`.
4. Il valore nel `MDR` viene copiato nel registro di destinazione o all'ingresso della ALU.

Se un secondo operando va recuperato dalla memoria, si eseguono di nuovo le operazioni da 1.

#### Esempio di operand fetch

:::{figure} /3/img/cpu-internal-operands.svg
Esempio di esecuzione della fase di *read*.
1. Nel `MAR` viene scritto l'indirizzo della cella di memoria da cui va prelevato l'operando, `0x3D` nell'esempio.
2. Si attiva la linea `Read` del bus controllo.
3. Dopo le operazioni di accesso alla RAM, nel MDR, si trova il valore presente nella cella di memoria selezionata, `0x5E` nell'esempio.
4. Spesso, prima che il valore possa andare all'ALU, deve essere copiato in un registro. Nell'esempio si indica il registro `RT` (registro temporaneo) come il registro dove l'operando viene depositato prima di andare all'ALU.

A questo punto tutti gli operandi sono pronti e la CPU può procedere con l'*execute* dell'istruzione.
:::

### Esecuzione dell'istruzione
Una volta che la CPU ha decodificato l'istruzione presa dalla memoria, il suo compito è quello di eseguirla. Ad esempio, se si tratta di un'istruzione di somma, la CPU utilizzerà il suo circuito di somma. I circuiti per eseguire le operazioni aritmetiche (somma, sottrazione, ...) e logiche (and, or, ...) si trovano nel blocco **ALU** (*Arithmetic Logic Unit*) della CPU. Notiamo che alcune operazione potrebbero non richiedere l'utilizzo della ALU, ad esempio le istruzioni che copiano dalla memoria ai registri o viceversa.

L'esecuzione dell'istruzione si compone dei seguenti passi.
1. Per istruzioni che usano la ALU, si attende che il risultato sia calcolato.
2. Una volta pronto, il risultato viene scritto nel registro indicato dall'istruzione (alcune CPU usano un *registro di default* chiamato *registro accumulatore*).
3. Per operazioni di lettura e scrittura dalla memoria, l'esecuzione non fa nessuna operazione (la lettura avviene con il *fetch* degli operandi, la scrittura avviene nell'ultima fase).
4. Per operazioni di **salto** l'esecuzione cambia il valore del program counter.

#### Esempio di execute

:::{figure}  /3/img/cpu-internal-execute.svg
Esempio di esecuzione della fase *execute*.
1. La ALU esegue la somma degli operandi (che erano stati preparati durante il *read*)
2. Il risultato dell'operazione viene depositato nel registro di destinazione, `R1` nell'esempio.
:::

### Scrittura del risultato
Per le operazioni che producono un risultato, ad esempio la somma di due numeri, potrebbe essere necessaria la scrittura in RAM, questo avviene nella fase di *write*. In questa fase, la CPU utilizza i registri `MAR` e `MDR` per spostare il risultato dal registro dove lo ha messo la ALU alla memoria. Questa operazione potrebbe non essere necessaria, ad esempio se si sommano due registri mettendo il risultato ancora nei registri.

La scrittura del risultato si compone delle seguente fasi.
1. Se il risultato deve essere scritto in memoria, l'indirizzo della RAM viene scritto nel `MAR`.
2. Il risultato (scritto in un registro nella fase di *execute*) viene messo nel `MDR`.
3. Si attiva la linea `Write` del bus controllo.

#### Esempio di scrittura del risultato
    
:::{figure} /3/img/cpu-internal-write.svg
Esempio di esecuzione della fase di *write*.
1. Il circuito di decodifica imposta nel `MAR` l'indirizzo della cella di memoria dove scrivere il risultato
2. Il valore da scrivere viene copiato dal registro in cui si trova (`R1` nell'esempio) al `MDR`.
3. Si attiva la linea `Write` del bus di controllo.
:::

 


