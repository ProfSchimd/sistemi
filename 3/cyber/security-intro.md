---
abbreviations:
    CSO: Chief Security Officer
---

# Introduzione alla Cybersecurity

In questa lezione introduciamo i concetti base e le prime, importanti definizioni nell'ambito della *cybersecurity*. Questi fondamenti ci serviranno successivamente per trattare l'argomento sicurezza in modo chiaro e avendo ben presente quali sono gli aspetti importanti.

```{tip} AmanoZ
:label: desc-amanoz
La tuq società di vendita online **AmanoZ** serve clienti in tutta Europa attraverso i propri magazzini presenti in ciascuna nazione. Inoltre, l'azienda possiede due data center, uno a Milano e uno a Dublino, che gestiscono tutta la parte informatica: portale, App, gestionale interno e tutto il necessario. Quale *Chief Security Officer (CSO)* dell'azienda devi tenere monitorato tutti gli *asset* dell'azienda e proteggerli da attacchi.
```

## Asset
La prima domanda che ci poniamo è *cosa dobbiamo mettere in sicurezza?* Dal momento che si parla di **cyber sicurezza**, è chiara l'importanza di questa domanda. 

:::{prf:definition} Asset
Un **asset** è una qualsiasi risorsa (hardware, software, dati, ...) che abbia un valore per l'organizzazione o la persona. 
:::

Con il termine risorsa qui si deve intendere sia hardware che software. Anche i dati sono degli asset (spesso fondamentali). Infine, sono asset anche le persone, i brevetti, la reputazione, il brand, ...  In altre parole, tutto ciò che ha un valore è un asset che va protetto e *messo in sicurezza*.

```{tip} Gli asset di AmanoZ
L'azienda @desc-amanoz ha diversi asset the il suo CSO deve proteggere.
- I dati dei propri clienti: indirizzo, dati pagamento, dati su acquisiti, ...
- I propri magazzini fisici e le merci immagazzinate al loro interno.
- I data center e tutti gli appari in essi presenti (server, dispositivi di rete, batterie per UPS, ...).
- La fiducia dei clienti (reputazione dell'azienda) è anche un asset, scoprire che l'azienda ha problemi di sicurezza può far perdere tale fiducia e quindi il cliente.

Questi sono alcuni degli **asset aziendali** di AmanoZ. Si noti come gli asset sono beni informatici materiali (es. server) o immateriali (dati, software, ...); gli asset possono essere beni non informatici materiali (magazzini, merci, ...) o immateriali (fiducia, clienti, ...).
```

```{figure} /3/img/asset-aziendali.svg
Gli asset aziendali possono essere materiali e immateriali.
```

## Minaccia, Vulnerabilità e Attacco

:::{prf:definition} Minaccia
Una **minaccia** (**threat**) è la possibilità che si portino a termine operazioni dagli esiti potenzialmente dannosi per un'entità (azienda, persona, ente, ...). 
:::

Una minaccia rappresenta la *possibilità* che un'azione dannosa si compia, questo fatto introduce il concetto di **rischio** inteso come la *probabilità* che un evento si verifichi combinata con l'*impatto* che tale evento può causare. Possiamo indicare matematicamente questa relazione
$$
\textrm{Rischio} = \textrm{Impatto} \times \textrm{Danno}
$$ 

In ambito di *cybersecurity* (come in altri) una minaccia deve essere messa in relazione al rischio ad essa associato. Ad esempio il rischio che un telefono aziendale venga rubato o smarrito è *medio*, ma se tale furto non permette l'accesso ai dati al ladro (impatto basso), il rischio associato all'evento può risultare basso. 

La classificazione di minacce secondo il livello di rischio permette di assegnare priorità alle contromisure da adottare partendo con l'affrontare minacce ad elevato rischio per poi proseguire con le minacce a rischio via via più basso.

```{figure} /3/img/risk-assessment-matrix.svg
:label: fig-risk-assessment-matrix
Un esempio di *risk assessment matrix* per l'identificazione del livello di rischio (da basso ad elevato) sulla base del livello di impatto e della probabilità.
```

```{tip} Minacce in AmanoZ
Il tuo primo compito come CSO di AmanoZ è individuare quali minacce hanno un gradi rischio `Alto` facendo riferimento alla [matrice di valutazione del rischio](#fig-risk-assessment-matrix) presentata sopra. Per effettuare questa analisi si devono considerare le varie minacce una ad una e valutarne il livello di rischio. 
- **Furto di dati sensibili:**[^sensible] si tratta di un evento “possibile” (probabilità media di accadere) il cui impatto sarebbe significativo se non severo. Secondo la nostra classificazione il rischio associato è `Medio-Alto`.
- **Furto di merce:** non è raro che i magazzini siano presi di mira da ladri è quindi `Probabile` che si verifichi tale evento il cui impatto può essere `Significativo` (dipende dal valore della merce che potrebbe essere rubata), quindi il rischio è da ritenersi `Alto` e si rendono necessarie contromisure e prevenzione (ad esempio un servizio di vigilanza 24 ore).
- **Calamità naturale:**[^calamita] la probabilità di tale evento dipende dalla zona in cui si trovano le nostre risorse (magazzini, data center, ...). In generale si dovrebbe costruire in zone in cui tale probabilità è molto bassa (evento `Molto improbabile`). D'altro canto l'impatto di un incendio o di una alluvione possono essere `Severo`, l'intero patrimonio potrebbe essere distrutto. Nella nostra matrice di valutazione, tale evento ha rischio `Medio`.

Ora continua tu a valutare il rischio dei seguenti eventi.
- **Sabotaggio dell'infrastruttura IT da dipendenti**
- **Attacco informatico di tipo ransomware**[^ransomware]
- **Interruzione di fornitura di energia elettrica**
- **Campagna di *diffamazione* nei confronti del brand**
```

:::{prf:definition} Vulnerabilità
Una **vulnerabilità** (**vulnerabilità**) è un *punto debole* del sistema che può essere sfruttato (*exploited*) per portare a termine un *attacco*.
:::

Le vulnerabilità sono i varchi che permettono a malintenzionati di accedere al sistema per compiere operazioni potenzialmente dannose (attacchi ai server, ransomware[^ransomware] dei dati, ...).

Le vulnerabilità possono essere legate a *bug* o malfunzionamenti software, ma possono anche essere legate agli individui, ad esempio una password debole o una chiavetta dimenticata.

Per ridurre il numero di vulnerabilità di tipo software è consigliabile:
- mantenere aggiornati tutti i software
- utilizzare solo software sicuri e fidati
- evitare il più possibile l'uso dei dispositivi personali


:::{prf:definition} Attacco
Un **attacco** (**attack**) è l'azione (tipicamente volontaria) che sfrutta una *vulnerabilità* per concretizzare una *minaccia* e recare un qualche danno agli *asset* di un'entità (aziende, persone, governi, ...).
:::

:::{prf:definition} Mitigazione
Un intervento di **mitigazione** (**mitigation**) è una qualsiasi azione che abbia lo scopo di diminuire gli effetti dannosi di un attacco.
:::

:::{prf:definition} Superficie di Attacco
La **superficie di attacco** (**attack surface**) è l'insieme di tutte le vulnerabilità che sono sfruttabili da un attaccante.
:::

[^sensible]: I **dati sensibili** sono quei dati che appartengono ad una persona e che rappresentano informazioni importanti, tipicamente private. Dati sensibili sono nome, cognome, indirizzo numero di telefono, dati medici, dati di pagamento, ... 

[^calamita]: Le calamità naturali sono eventi quali terremoti, alluvioni, incendi, ... Non sempre le calamità naturali sono fenomeni naturali, ad esempio un esempio potrebbe essere stato appiccato di proposito all'edificio o anche ad un bosco limitrofo.

[^ransomware]: Il **ransomware** è un attacco informatico in cui attori malintenzionati riescono a rendere indisponibili i dati di un ente (ad esempio cifrandoli) chiedendo un riscatto (*ransom*) per la loro restituzione.