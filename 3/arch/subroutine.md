---
title: Subroutine e gestione dello stack
abbreviations:
    SP: Stack Pointer
---

## Le subroutine
Spesso un programma deve eseguire la stessa sequenza di istruzioni più volte. Mentre un **loop** permette di eseguire più volte un gruppo di istruzioni in modo *consecutivo*, le **subroutine** permettono di eseguire più volte un gruppo di istruzioni, *anche non consecutivamente*.

Un esempio di subroutine è la sequenza di istruzioni per calcolare la *radice quadrata* di un numero $x$. Ogni volta che serva calcolare $\sqrt{x}$, si può utilizzare lo stesso “gruppo” di istruzioni, senza dover ogni volta riscriverle. Ad esempio in Java questo si può ottenere con il metodo statico `sqrt` della classe `Math`

```java
double y = Math.sqrt(x);
```

Quando serve utilizzare una subroutine che è già stata scritta, si dice che si esegue una **chiamata alla subroutine**. Questo modo di dire suggerisce una ”richiesta di aiuto” per funzioni speciali, ad esempio calcolare $\sqrt{x}$.

```{figure} /3/img/loop-vs-subroutine.svg
```


L'immagine sopra mostra la differenza di esecuzione tra un loop (a sinistra) e una subroutine (a destra), le frecce indicano i “salti” di istruzioni. Nel caso di un loop il salto ha la funzione di riportare all'inizio del ciclo il *program counter*, mentre nel caso di una subroutine la sequenza viene momentaneamente interrotta per “chiamare” (istruzione `jal`[^jalexplain]) una subroutine la quale, una volta terminata, restituirà[^return] (istruzione `ret`) il controllo al punto immediatamente successivo  alla chiamata; anche in questo ci sarà una modifiche al program counter.


Il concetto di subroutine è strettamente legato ai concetti di procedura e funzione nei linguaggi procedurali (ad esempio C e Python) ed al concetto di metodo nei linguaggi ad oggetto (ad esempio Java e Python). Infatti il *compilatore* (che traduce il codice in linguaggio macchina), trasforma ogni procedura ed ogni metodo in una chiamata a subroutine.

### I parametri delle subroutine
Nell'esempio della radice quadrata, il numero $x$ rappresenta l'*input* alla subroutine che calcola $\sqrt{x}$, si parla anche di **parametro** d'ingresso alla subroutine. Anche il risultato della subroutine (cioè il numero $\sqrt{x}$) è un parametro della subroutine, in particolare un parametro di uscita.

Una subroutine può o meno avere dei **parametri d'ingresso** cioè delle variabili il cui valore non si conosce nel momento in cui si scrive il programma, ma che sono importanti per l'esecuzione della subroutine. Ovviamente possono esistere subroutine senza o con più di un parametro d'ingresso.

Una subroutine può o meno avere dei **parametri d'uscita** cioè delle variabili il cui valore viene riempito dalla subroutine stessa e poi usato da chi ha fatto uso della subroutine. Come per i parametri d'ingresso, anche i parametri di uscita possono essere assenti o più di uno. 

#### Passaggio di parametri
La presenza di parametri d'ingresso e/o di uscita è così frequente nella
pratica che esistono dei registri della CPU dedicati (vedi sotto "Stack
Pointer") e delle istruzione apposite (`CALL` e `RET`). In pratica
i parametri vengono scritti in un'apposita zona della memoria, chiamata
*stack* (vedi [sotto](#lo-stack-di-programma)).


(lo-stack-di-programma)=
## Lo stack di programma

### La memoria di programma
Ad ogni programma in esecuzione, il sistema operativo assegna una zona della memoria che chiamiamo memoria di programma. Questa zona della memoria deve ospitare il codice e tutti i dati necessari all'esecuzione del programma. Per meglio gestire questi aspetti, la memoria di programma è suddivisa in varie parti come mostrato in @fig-program-memory.

```{figure} /3/img/program-memory.svg
:label: fig-program-memory
Rappresentazione della memoria di programma. Si può vedere che nella *parte basse* della memoria troviamo il codice (`.text`) e i dati statici (`.data`, `.bss`) mentre nella parte alta della memoria troviamo i dati allocati dinamicamente (heap e stack). Lo stack pointer (`SP`) punta alla prima posizione libera nello stack.
```

Codice (`.text`)
: La parte bassa della memoria contiene le istruzioni del programma (il codice macchina).

Dati statici inizializzati (`.data`)
: Dopo il codice vengono memorizzati i *dati statici inizializzati* cioè quei dati che sono noti durante la fase di compilazione del programma.

Dati static non inizializzati (`.bss`)
: Segue la parte di dati statici allocati di cui non sono noti i valori durante la compilazione del programma stesso

Memoria heap
: La parte bassa della memoria dinamica, contiene lo **heap** (in italiano *cumulo*) in cui vengono memorizzati i dati la cui dimensione e valore è nota solo in fase di esecuzione. 

Stack
: La parte alta della memoria dinamica, contiene lo **stack** (in italiano *pila*) in cui vengono memorizzati dati “temporanei“ la cui dimensione è tipicamente nota in fase di compilazione. Lo stack rappresenta una porzione importante della memoria perché permette l'implementazione delle chiamate a subroutine.

```{note} Memoria dinamica
Dalla @fig-program-memory si vede che stack e heap “condividono” la parte alta della memoria e che entrambe possono aumentare o diminuire di dimensione durante l'esecuzione del programma (indicato dalla frecce nell'immagine). 
```
## Gestione delle subroutine nella CPU
Vediamo ora come utilizzare lo stack per eseguire chiamate a subroutine con *passaggio di parametri*. Per tale scopo le CPU offrono uno o più registri, il più importante dei quali viene chiamata **Stack Pointer** (SP). 

### Stack Pointer (SP)
Per meglio gestire lo stack, ogni CPU possiede un registro speciale chiamato **Stack Pointer** `SP` nel quale si tiene traccia della *cima* dello stack (la prima zona “libera”).

```{figure} /3/img/stack-pointer.svg
```

Nell'immagine sopra è mostrato un momento intermedio nell'esecuzione di un programma. Lo `SP` sta puntando al byte `122`, nei byte con indirizzo maggiori indicano sono contenuti valori (ad esempio variabili) mentre i byte con indirizzo minori di `122` sono *liberi*. La freccia indica che lo memoria dello stack si riempie dagli indirizzi “alti” agli
indirizzi “bassi“ (come in @fig-program-memory).

```{note} Push e Pop
Le operazioni di inserimento ed eliminazione dallo stack hanno dei nomi specifici, **push** e **pop**, rispettivamente. In una struttura a stack è possibile solo fare push o pop, non inserire “in mezzo”.
```

### Chiamata a subroutine
I linguaggi assembly prevedono istruzioni particolari per la chiamata a subroutine,
normalmente queste istruzioni fanno alcune operazioni per preparare i registri
all'esecuzione della subroutine.

Chiamata a subroutine
* Salva il valore attuale del *program counter* prima del salto. In questo modo, alla
fine della subroutine, sarà possibile tornare "dove si era rimasti" (prima del salto).
* Salva il valore dello stack pointer. In questo modo la subroutine può modificare
lo stack pointer creando variabili o facendo a sua volte chiamate a subroutine.
* Prepara nello stack i parametri della subroutine. In questo modo i *parametri formali*
vengono riempiti con i valori dei *parametri attuali*.

Ritorno da subroutine
* Ripristina il vecchio valore dello stack pointer. In questo modo sarà possibile
riprendere l'esecuzione con lo stack come era prima della chiamata.
* Scrive i risultati (parametri di uscita) in modo che siano a disposizione dopo
che si ritorna all'esecuzione precedente.
* Ripristina il valore del *program counter* così il prossimo ciclo fetch-and-execute
recupera l'istruzione corretta (prima delle chiamata a subroutine).

Tutte le operazioni sopra coinvolgono lo stack e sono mostrate con un esempio nella figura
qui sotto.

```{figure} /3/img/subroutine-stack.svg
```

Nella precedente figura vediamo tre diversi "momenti" dell'esecuzione della
subroutine `SQRT(x)` per il calcolo di \\(\sqrt{x}\\). In questa figura la
memoria è divisa in *parole* perciò gli indirizzi sono tutti multipli di 4.

1. *Prima della chiamata* lo stack è riempito fino alla parola `132`. Lo 
stack pointer `SP` indica la prima parola di memoria che libera cioè la 
`128`.

2. Durante l'esecuzione della subroutine (dopo l'istruzione `CALL`), nelle
tre parole libere troviamo
    1. il valore del program counter `PC` prima della `CALL`
    2. il valore dello stack pointer `SP` prima della `CALL` (`128` nel nostro esempio)
    3. il parametro `x` della routine

3. Terminata l'esecuzione della subroutine (dopo l'istruzione `RET`), la situazione
ritorna quella presente prima dell'esecuzione di `CALL` con la differenza che da
qualche parte (all'indirizzo `128` puntato dallo `SP` nel nostro esempio) si
trova il risultato \\(\sqrt{x}\\) della subroutine. Va tenuto presente che nell'esempio
la parola `128` è considerata libera poiché `SP` indica sempre una parola libera.
Il programmatore che volesse usare questo valore, deve prima portarlo in un registro
o in un'altra zona di memoria (alcuni linguaggi usano dei registri prestabiliti
per il risultato di una subroutine).

## Esempio di subroutine 

Consideriamo ora un esempio di subroutine che, in Java, corrispondente ad un metodo con
la seguente *firma*.

```java
public int trova(int[] v, int k) 
```

Questo metodo restituisce un `int` che rappresenta l'indice della posizione di `k`
nell'array `v`. Se in `v` non esiste una posizione con il valore `k`, il metodo
restituisce `-1`.

Notiamo che

* Il metodo ha due parametri di ingresso
    1. il **riferimento** all'array `v`
    2. il numero `k` da cercare
* Il metodo restituisce un singolo valore di tipo `int`

Supponiamo, inoltre, che il metodo `trova` utilizzi una sola variabile locale,
 che chiamiamo `y`, di tipo `int` dichiarata con una riga di codice simile
 a quella sotto

```java
int y = -1; // inizializzo la posizione
```

I cambiamenti subiti dallo stack durante l'esecuzione del metodo `trova`, sono
mostrati nell'immagine qui sotto

```{figure} /3/img/local-variable-stack.svg


A differenza dell'immagine più in alto, notiamo che quando la variabile `y` viene
dichiarata, questa viene posizionata sullo stack mentre `SP` viene ulteriormente
decrementato come conseguenza.

[^jalexplain]: Nell'assembly RISC-V, la chiamata a subroutine avviene mediante l'istruzione Jump-And-Link: `jal`. L'istruzione semplicemente opera un *salto incondizionato* all'istruzione che gli viene indicata, ma prima salva nel registro `ra` (Return AddresS) il valore attualmente presente nel Program Counter.

[^return]: Si parla di *restituire* il controllo immaginando un programma scritto in un linguaggio ad alto livello in cui un'unità di codice (ad esempio il `main`) chiama una routine (ad esempio `sqrt`) alla quale *cede il controllo del processore* affinché svolga le proprie operazioni terminate le quali la routine (`sqrt`) *restituisce il controllo* all'unità chiamante (`main`).