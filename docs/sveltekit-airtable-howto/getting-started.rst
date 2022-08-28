--------
Iniziamo
--------

Come per praticamente tutti i programmi basati su framework, il modo più
semplice per iniziare è quello di partire da un progetto base di esempio.


Creiamo il codice di esempio
----------------------------
A questo scopo gli sviluppatori di `SvelteKit` hanno predisposto un comando
dedicato per la creazione della struttura di programma da cui partire:

.. code-block:: shell
  :emphasize-lines: 1

  npm create svelte my-bookshelf
  cd my-bookshelf
  npm install
  npm run dev

Il primo comando crea il vero e proprio progetto di esempio nella cartella
*my-bookshelf*. Nel farlo richiede alcune informazioni di configurazione
del progetto, come ad esempio l'utilizzo o meno di Typescript come
linguaggio di programmazione.

Noi procediamo scegliendo le seguenti opzioni:

- "*Skeleton project*" come template:
  vogliamo partire da un progetto vuoto
- "*No*" all'utilizzo di *Typescript* per il controllo dei tipi
- "*Yes*" per l'utilizzo di *ESLint* per il controllo del codice
- "*No*" per l'uso di *Prettier* per la formattazione automatica del codice
- "*No*" all'uso di *Playwright* per il testing su multi browser

.. hint::
  La attivazione della funzionalità di controllo del codice
  tramite `ESLint`_, integrato correttamente nell'editor utilizzato
  obbliga a mantenere una coerenza di scrittura. È anche stato scelto
  di evitare l'uso del formattatore automatico `Prettier`_ obbligando
  così a scrivere il codice corretto fin dall'inizio.

.. _ESlint: https://eslint.org
.. _Prettier: https://prettier.io

I comandi successivi installano le dipendenze necessarie per il
funzionamento del progetto e lo avviano in modalità di sviluppo.

In particolare l'ultimo comando : ``npm run dev`` avvia il server di
sviluppo e rende disponibile l'applicazione web su
`localhost:5173 <http://127.0.0.1:5173>`_.

Analizziamo il progetto
-----------------------
*SvelteKit* è un progetto attualmente ancora in fase di sviluppo e
durante il processo di progettazione ha subito differenti modifiche anche
significative.

.. note::
  Questa guida fa riferimento alla versione disponibile al momento della
  scrittura (agosto 2022) che raccoglie modifiche sostanziali rispetto
  alle versioni precedenti.
  Per maggiori informazioni fare riferimento alla guida ufficiale
  di conversione :
  `Migration guide #5774
  <https://github.com/sveltejs/kit/discussions/5774>`_.
