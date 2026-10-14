---
title: Larghezza di banda e latenza
---

:::{hint} Dibattito...
:class: dropdown
Cosa consideri quando decidi di utilizzare un tipo di connessione anziché un altro (ad esempio rete cablata anziché rete senza fili)?
:::

Diversi *mezzi fisici* permettono diverse *velocità* di trasferimento dati, ma cosa si intende per velocità? Quando si parla di velocità si pensa al tempo che serve per trasferire qualche cosa, ma non a *quanto* si trasferisce. Nella trasmissione dati, quindi, dobbiamo sia considerare con che velocità riusciamo a trasmettere l'informazione sia quanta informazione riusciamo a trasmettere. 

Le due caratteristiche dei mezzi fisici che si collegano a quantità e velocità sono la **larghezza di banda** (**bandwidth**) e la **latenza** (**latency**). Spesso si usa l'analogia tra trasmissione dati e trasporto di qualcosa di fisico, ad esempio dell'acqua all'interno di un tubo:
* Un tubo può portare tanta più acqua quanto più è largo, questa *portata* è l'analogo della *larghezza di banda*;
* Un tubo più lungo richiede più tempo ad essere percorso, questo *tempo di percorrenza* è l'analogo della *latenza*.

(larghezza-di-banda)=
## Larghezza di banda (*bandwidth*)
La *larghezza di banda* $B$ indica la quantità di bit che possono attraversare il collegamento in un tempo prestabilito (ad esempio in un secondo). La banda si misura quindi in *bit al secondo* `bps` (*bit per second*, attenzione alla `b` minuscola) e suoi multipli: kilobit al secondo `kbps` ($10^3$ bps), megabit al secondo `Mbps` ($10^6$ bps), gigabit al secondo `Gbps` ($10^9$ bps). 

```{caution} Attenzione
L'unità di misura `bps` è in realtà l'unità $bit/s$ (*bit* diviso *secondi*), simile alla misura in $m/s$ (o $Km/h$) per la velocità di cambiamento della posizione.
```

La larghezza di banda misura la *portata* (in bit) cioè  *quanto “liquido” è in grado di trasportare il nostro “tubo”*.

### Tempo di trasmissione
La larghezza di banda può essere utilizzata per stimare il tempo necessario a trasferire una determinata quantità di bit. Supponiamo di dover spedire un messaggio di dimensione $D$ **misurata in bit**. Il tempo *minimo* $t$ necessario a trasferire $D$ bit su un mezzo con banda $B$ è

$$ t [sec] = \frac{D [bit]}{B [bit/s]}$$

dove abbiamo indicato all'interno di parentesi quadre le unità di misura.

```{attention} Attenzione
Quando la dimensione *non è espressa in bit* (come spesso accade), prima di applicare la formula sopra, è necessario convertire la dimensione in bit. Normalmente si tratta di una conversione da *byte* (o multipli) in *bit*, nel qual caso la dimensione va moltiplicata per 8

$$ D [bit] = 8 \cdot D [byte] $$

Va inoltre ricordato che in informatica i multipli dei byte sono espressi come potenze di 2 anziché potenze di 10:
- $ 1 kB = 2^{10} \ byte = 1024 \ byte $
- $ 1 MB = 2^{20} \ byte = 1048576 \ byte $
- ...

Tuttavia ricordiamo che **la banda in bit al secondo usa le potenze di 10**. Per distinguere i multipli potenza di due, a volte si usa indicare iB ad indicare il byte
- $1 kiB = 2^{10} \ byte$
- $1 MiB = 2^{20} \ byte$
- $1 GiB = 2^{30} \ byte$
- ...
```

:::{prf:example}
Su un collegamento a $1 Gbps$ viene trasferito un file, quanto tempo è necessario?
* Se il file ha una dimensione di $1$ kiB?
* Se il file ha una dimensione di $100$ kiB?
:::

## Latenza (*latency*)
La *latenza* indica il tempo che un bit impiega ad attraversare il collegamento, questo tempo non è mai zero, quindi **non esiste comunicazione istantanea**, ma dipende dal mezzo fisico. Tuttavia, possiamo dire che *per ogni mezzo fisico* la velocità di trasmissione di un bit non può superare quella della luce che è circa 300 mila chilometri al secondo.

:::{tip} Londra - New York
:class: dropdown
Quanto è il minimo tempo necessario a trasferire un bit tra Londra e New York?
:::

La latenza si può calcolare anche su percorso con diversi collegamenti fisici e diversi *dispositivi intermedi* (switch, router, ...). In questo caso ci sono diversi fattori che possono far aumentare la latenza:
* numero e lunghezza dei vari collegamenti;
* traffico presente lungo il percorso;
* livello di *congestione* nei dispositivi intermedi;
* ...

:::{note} Congestione
Con il termine *congestione* si indica un sovraccarico dovuto all'eccesso di traffico. Si parla anche di congestione del traffico stradale quando troppe auto sono presenti ed il traffico si blocca.
:::

### Round Trip Time (RTT)
Spesso è utile conoscere il tempo impiegato da un pacchetto per l'intero percorso di *andata e ritorno*, questo valore viene chiamata **Round Trip Time (RTT)**. 

Il valore del RTT è stimato dal programma `ping`, ad esempio eseguendo comando `ping google.com`:

```shell
64 bytes from 142.251.143.142: icmp_seq=0 ttl=114 time=28.905 ms
64 bytes from 142.251.143.142: icmp_seq=1 ttl=114 time=29.224 ms
64 bytes from 142.251.143.142: icmp_seq=2 ttl=114 time=33.102 ms
64 bytes from 142.251.143.142: icmp_seq=3 ttl=114 time=54.332 ms
```

vediamo i valori in *millisecondi* dell'RTT stimato per ognuno dei pacchetti spediti. Come si vede è normale misurare valori di RTT diversi tra loro, anche per uno stesso percorso. In questi casi può convenire calcolare la media dei valori di misurati. 


Quando il valore della latenza non è disponibile, è possibile utilizzare il RTT ipotizzando che andata e ritorno richiedano lo stesso tempo

$$ \textrm{Latency} = \frac{\textrm{RTT}}{2} $$

Ovviamente si può usare la formula inversa nel caso sia disponibile la latenza, ma non il RTT

$$ \textrm{RTT} = 2 \cdot \textrm{Latency} $$


## Throughput
La [larghezza di banda](#larghezza-di-banda) rappresenta la quantità massima di bit trasferibili nell'unità di tempo, tuttavia il picco di prestazioni non viene quasi mai raggiunto. 

Il numero **effettivo** di bit trasferiti nell'unità di tempo viene chiamato **throughput** $T$ che può essere misurato sperimentalmente. È bene osservare che il throughput non è costante nel tempo, fattori quali traffico, congestione ed altri hanno un impatto su questa misura che, quindi, può variare anche a distanza di poco tempo. D'altro canto, possiamo sempre affermare che *il throughput non può essere maggiore della banda*:

$$ T \leq B $$

### Goodput

Come è noto, i bit effettivamente spediti comprendono sia i *dati* sia l'*overhead* introdotto dagli header e trailer dei vari protocolli. La quantità di *bit di dati* trasferita (diversa dalla quantità di bit totali) viene indicato con **goodput**. Tale misura può risultare utile in fase di dimensionamento di una connessione, ma è raramente utilizzata.

## Calcolo di tempi di trasmissione
Avendo a disposizione i parametri (banda e latenza/RTT) per tutti i collegamenti della rete, è possibile ottenere una *stima* del tempo di trasmissione di una determinata quantità di informazione. 

Per avere una stima attendibile, bisogna anche conoscere il *comportamento* dei dispositivi intermedi che, in base al loro funzionamento, possono introdurre ritardi e/o rallentamenti della trasmissione.

### Tempo di trasmissione su singolo link
Su un link di banda $B$ e latenza $L$, un pacchetto di $D$ bit richiede tempo di trasmissione:

$$ t = L + \frac{D}{B} $$

Ad esempio spedire $1500 Byte$ su un link a $1 Mbps$ con latenza $5 ms $ richiede

$$ 5 [ms] + \frac{1500 \cdot 8 [bit]}{10^6 [bit/s]} = 17 [ms] $$

:::{caution} Unità di Misura
Controllare sempre che le unità di misura siano coerenti, nell'esempio sopra è stata implicitamente fatta la trasformazione da $5 [ms]$ a secondi ($0.005 [s]$), successivamente si è svolta la somma con il risultato della frazione ($0.012 [s]$) infine si è di nuovo convertito il risultato in millisecondi, ottenendo il valore finale $17 [ms]$.
:::

### Tempo di trasmissione con dispositivi intermedi
Quando nel percorso sono presenti dispositivi intermedi (quali switch e router), una stima dei tempi di trasmissione richiede di conoscere il comportamento di questi dispositivi. Normalmente i dispositivi intermedi utilizzano delle *code* di ingresso e uscita per ogni porta. I pacchetti si accodano in ingresso al dispositivo e vengono accodati in uscita. Ci sono due principali modi con cui i dispositivi “spostano” i pacchetti dalla coda di ingresso a quella di uscita.
* Modalità **store-and-forward**: il dispositivo riceve l'intero pacchetto e solo dopo che l'ha ricevuto per intero lo sposta nella coda di uscita.
* Modalità **cut-through**: il dispositivo sposta il pacchetto mano a mano che lo riceve.

Mentre nel primo caso **prima che inizi la ritrasmissione è necessario attendere l'intero tempo di ricezione**, nel secondo caso il dispositivo intermedio può iniziare la ri-trasmissione (accodamento in uscita) non appena riceve il primo bit anche se ancora sta ricevendo l'intero pacchetto.[^1]

Negli esercizi che seguono faremo riferimento solo al modello *store-and-forward* poiché i calcoli sono più semplici e, nella pratica, la differenza di tempi è minima.

### Esercizio
Consideriamo la topologia di rete presentata nella figura sottostante e corredata dalle informazioni sui dati

:::{figure} /4/img/ex-topology-bandwidth.svg
* Tutti i collegamento `PC <-> Switch` sono a $ 100~Mbps $ con latenza $ 15~ms $
* I collegamenti wireless sono a $ 50~Mbps $ con latenza $ 45~ms $
* I collegamento tra router e Switch e AP sono a $ 10~Gbps $ con latenza $ 15~ms $
* I collegamenti `SER <-> Router` sono a $ 1~Gbps $ con latenza $ 10~ms $
* Router, Access Point e switch sono *store and forward* (inoltrano dopo aver ricevuto l’intero pacchetto)
* Tutti i pacchetti hanno dimensione $ 1500~byte $ con header di $ 40~byte $.
:::

#### Domande
1. Quale è il Round Trip Time (RTT) tra `PC1` e `SER3` se messaggio e conferma sono pacchetti da 1500 Byte?
2. Quale è il Round Trip Time (RTT) tra `NB1` e `SER1` se messaggio e conferma sono pacchetti da 1500 Byte?
3. `PH1` deve trasferire 5840 Byte sul server `SER2`, quanti pacchetti deve spedire? `NB1` deve spedire 8760 Byte su `SER3`, quanti pacchetti deve spedire? `AP1` riceve contemporaneamente i pacchetti da `NB1` e `PH1` e li inoltra alternatamente (prima un pacchetto di `NB1` poi un pacchetto di `PH1` e così via) quanti pacchetti totali `AP1` inoltra verso `ROUTER1` e quanto tempo impiega complessivamente? Giustifica tutte le risposte.
4. Oltre ai pacchetti della domanda precedente, `ROUTER1` riceve altri pacchetti da `SWITCH1` per complessivi (header e dati) 12000 Byte (tutti direzionati a `SER1`). Quanti pacchetti complessivamente riceve `ROUTER1`? Tenendo conto del fatto che `ROUTER1` è *store-and-forward* e che esso può trasmettere in uscita (cioè verso i server) non appena riceve completamente un pacchetto. Se tutti i pacchetti iniziano ad arrivare allo stesso momento, quanto impiega `ROUTER1` a consegnare il primo pacchetto a `SER1`, `SER2` e `SE3`? Quanto impiega a consegnare tutti i pacchetti a `SER1`, `SER2` e `SER3`?

[^1]: In realtà è necessario conoscere la destinazione prima di re-indirizzare il pacchetto nella corretta porta di uscita. Per questo i dispositivi cut-through devono comunque ricevere almeno l'indirizzo di destinazione prima di procedere con l'inoltro alla porta d'uscita.
