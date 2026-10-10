# Protocolli e Modelli di Riferimento

## Protocolli

Una delle caratteristiche delle reti è quella di essere composta di numerosi dispositivi, di diversi produttori, con hardware e software non omogeneo. Ad esempio sulla rete Internet pubblica troviamo oggi smartphone prodotti da Apple, lampadine intelligenti della Phillips, router e switch Cisco o Netgear e decine di altri tipi di dispositivi prodotti da centinaia di aziende diverse. Chiaramente **serve un insieme di regole condivise che permettano a questi dispositivi diversi di comunicare tra di loro**.

Alla base di questa *interoperabilità* ci sono i **protocolli di rete** cioè insieme di regole che specificano il comportamento di hardware e software di rete.

:::{prf:definition} Protocollo
Un **protocollo** è un insieme di regole che descrivono come un hardware e/o un software devono gestire le comunicazioni.
:::

:::{tip} Esempio
Anche nelle conversazioni tra persone si seguono dei “protocolli” (regole) di comunicazione. Ad esempio, si cerca di non parlare contemporaneamente, per non creare interferenza. Un altra regola riguarda la lingua parlata che deve essere condivisa altrimenti non sarebbe comprensibile.
:::

Per il funzionamento delle complesse reti moderne sono necessari decine di protocolli, ciascuna con degli scopi ben specifici. La suddivisione dei protocolli sulla base dei loro scopi può essere fatta utilizzando i *modelli di riferimento* discussi nella prossima sezione.

## Modelli di riferimento
I numerosissimi protocolli utilizzati nelle reti moderne coprono una vasta varietà di ruoli e problematiche, è quindi utile suddividere i protocolli sulla base del loro ruolo e dell'ambito a cui si applicano. Due sono i principali **modelli** di organizzazione dei protocolli
- il modello **OSI (Open Interconnected System)** proposto dall'ISO (International Standardization Organization) e
- il modello **TCP/IP**.[^1]

Entrambi i modelli ISO/OSI e TCP/IP sono modelli *a strati* suddivisi in **livelli**, ciascun livello si occupa di un ambito specifico e comprende protocolli che svolgono funzioni relative a quell'ambito. Nella [Figura sotto](#fig-models-compared) si possono vedere i due modelli affiancati e confrontati dove sono stati messi in corrispondenza i livelli nei modelli, che contano un numero diverso di livelli (sette per il modello ISO/OSI e quattro per il modello TCP/IP).

```{figure} /4/img/models-compared.svg
:align: center
:height: 500 px
:label: fig-models-compared

Corrispondenza tra i livelli del modello ISO/OSI (a sinistra) e del modello TCP/IP (a destra). Fonte [Wikimedia](https://commons.wikimedia.org/wiki/File:OSI_Application_Layer.svg)
```

### Chi definisce i protocolli

## Incapsulamento

[^1]: Il modello TCP/IP non è ufficialmente promosso da un ente specifico, ma risulta dall'insieme dei protocolli proposti dall'IETF negli RFC. I principali protocolli IP e TCP danno il nome al modello stesso.