---
title: Codifica
---

## Il problema della codifica
Per un dato *mezzo di comunicazione* i dispositivi devono “concordare” su come misurare l'informazione (i bit). Ad esempio, sul cavo in rame si decide che la tensione +5V indica il bit 1 mentre la tensione di 0V indica il bit 0. Anche dopo aver fissato questa regola, rimane il problema di “quando” misurare la tensione sul cavo. Per vedere questo problema con un esempio concredo, si consideri il segnale dati riportato nella seguente figura.

:::{figure} /4/img/bit-signal.svg
Esempio d segnale binario. Senza una guida precisa su “quando” misurare i valori, non è possibile determinare univocamente che sequenza di bit è *codificata* dal segnale.
:::

Può sembrare naturale associare al segnale sopra la sequenza di bit `010110011`, tuttavia la “corretta” sequenza di bit dipende da “quando” il segnale viene misurato e quindi dal **clock** che viene usato per la sua *temporizzazione*. 

:::{figure} /4/img/bit-clocked-signal.svg
Quando un segnale è accompagnato da un *clock* sappiamo quando il segnale va letto (*campionato*), questo permette la corretta ricostruzione della sequenza di bit. Nella figura, usando il primo clock si ricostruisce la sequenza `010110010`, usando il secondo clock si ricostruisce la sequenza `00100`).
:::

Mentre il primo clock (secondo segnale in figura) porterebbe alla ricostruzione
sopra indicata (cioè `010110010`), il secondo clock darebbe come sequenza `00100`).

```{note} Il termine *Campionamento*
Spesso nei sistemi digitali si utilizza il termine **campionamento** che indica il processo con cui un segnale (normalmente continuo) viene letto (*campionato*) ad intervalli regolari. Il tempo che passa tra due campioni successivi è sempre uguale è viene chiamato *periodo di campionamento* $T_c$. L'inverso del periodo di campionamento viene chiamata *frequenza di campionamento* $f_c$. Nella teoria della trasmissione sviluppata da [Claude Shannon](https://it.wikipedia.org/wiki/Claude_Shannon) un risultato importante è noto come *teorema del campionamento* che ci permette di stabilire quale è la minima frequenza $f_c$ che permette una fedele ricostruzione del segnale continuo. Senza questo risultato, tutta la teoria dei segnali digitali (quelli utilizzati da sistemi moderni) non sarebbe possibile.
```

## Codifiche
Da quanto detto sopra, è chiaro che serve mettersi d'accordo su come *decodificare* i bit a partire dal *segnale* presente nel mezzo di comunicazione. Diverse tipologie di codifiche sono state proposte, ciascuno con vantaggi e svantaggi. Di seguito descriviamo alcune delle codifiche più importanti e più utilizzate.

### Non Return to Zero (NRZ)
Nella codifica *Non Return to Zero (NRZ)* il segnale viene letto ad intervalli periodici utilizzando un clock. Il segnale codifica i due bit con valori di segno opposto. Ad esempio si può usare il valore +5V per il bit `1` ed il valore -5V per il bit `0`. Ad ogni lettura il segnale codificato in NRZ rimane al livello corrispondente fino a che non cambia per il prossimo bit. Non è previsto che il segnale si posizione ad un livello intermedio (lo zero), da questa proprietà deriva il nome della codifica.

:::{figure} /4/img/codifica-nrz.svg
Codifica Non Return to Zero (NRZ)
:::

### Non Return to Zero Inverted (NRZI)
Anche se il nome ricorda la codifica NRZ, in realtà *Non Return to Zero Inverted
(NRZI)* è diversa da NRZ. Nella codifica NRZI, infatti, è importante il fatto
che ci sia o meno una *transizione* da un livello ad un altro (ad esempio da +5V
a -5V). Più nello specifico NRZI misura il segnale utilizzando un clock e sceglie
il bit con la seguente regola:
* se il segnale è cambiato di valore rispetto alla misura precedente, allora il bit
è `1`,
* altrimenti (segnale uguale alla misura precedente) il bit è `0`.

:::{figure} /4/img/codifica-nrzi.svg
Codifica Non Return to Zero Inverted (NRZI)
:::

```{important} Attenzione
Sia la codifica NRZ che la codifica NRZI funzionano solo se le due parti comunicanti condividono il *segnale di clock*. Questo è spesso un problema perché richiede l'utilizzo di un canale di comunicazione dedicato al clock aggiuntivo rispetto al canale dati. Inoltre vi è la necessità di *sincronizzazione* i clock. Per evitare la necessità di un clock condiviso, sono state proposte diverse codifiche tra cui la codifica Manchester presentata nel prossimo paragrafo.
```

### Manchester
Nella codifica Manchester, i valori `0` e `1` vengono associate alle *transizioni* del segnale da un livello ad un altro. In pratica il segnale viene interpretato nel seguente modo:
* il passaggio dal valore alto al valore basso viene associato al bit `1`,
* il passaggio dal valore basso al valore alto viene associato al bit `0`.

:::{figure} /4/img/codifica-manchester.svg
Codifica Manchester
:::

```{tip} Osserva
Nella codifica Manchester descritta sopra il passaggio da basso ad alto
si associa ad un valore `1`, tuttavia sarebbe possibile associare tale
transizione al bit `0` (e la transizione opposta al bit `1`). 

In questa lezione abbiamo scelto la prima convenzione che è quella
adottata dagli standard IEEE (ad esempio IEEE 802.3).
```