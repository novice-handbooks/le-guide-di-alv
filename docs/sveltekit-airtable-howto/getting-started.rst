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

  npm create svelte@latest my-bookshelf
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

Ci sono due concetti base da tenere conto:

- Ogni pagina dell'applicazione è un *componente* `Svelte <https://svelte.dev>`_
- Ogni pagina creata sarà un file aggiunto alla directory ``src/routes``.

Capiremo più avanti il significato intrinseco di questi concetti.

Analizziamo insieme i file che sono stati generati dai comandi utilizzati
precedentemente, evidenziando quelli che sono parte dei sorgenti del
progetto e non artefatti della compilazione.

Nella cartella principale di progetto troviamo:

package.json
~~~~~~~~~~~~

Il codice generato dovrebbe essere molto simile a quello riportato
di seguito, con eventuali differenze sulle versioni delle dipendenze.

.. code-block:: json

  {
    "name": "my-bookshelf",
    "version": "0.0.1",
    "private": true,
    "scripts": {
      "dev": "vite dev",
      "build": "vite build",
      "preview": "vite preview",
      "lint": "eslint ."
    },
    "devDependencies": {
      "@sveltejs/adapter-auto": "next",
      "@sveltejs/kit": "next",
      "eslint": "^8.16.0",
      "eslint-plugin-svelte3": "^4.0.0",
      "svelte": "^3.44.0",
      "vite": "^3.1.0"
    },
    "type": "module"
  }

Si tratta del file di dipendenze del progetto **Node**, e si può notare
che allo stato attuale esistono solo dipendenze di sviluppo (``devDependencies``)
e nessuna dipendenza di "produzione" (``dependencies``). Questo è una caratteristica
basiliare di **Svelte** che, per quanto possibile trasforma tutto il codice
in *javascript* nativo rendendo il progetto portabile e ottimizzato.

Il file ``package.json`` deve includere ``@sveltejs/kit``, ``svelte`` e
``vite`` come dipendenze di sviluppo.

Voglio farti notare che il file ``package.json`` creato contiene la
configurazione ``"type": module``. Questo fa si che i file ``.js``
sono interpretati come moduli nativi JavaScript in fase di
``import`` e ``export``.

svelte.config.js
~~~~~~~~~~~~~~~~

File di configurazione di **Svelte** e **SvelteKit**

vite.config.js
~~~~~~~~~~~~~~

Un progetto **SvelteKit** in realtà si tratta di un progetto `Vite <https://vitejs.dev/>`_
che usa il plugin `@sveltejs/kit/vite` assieme a qualsiasi altra configurazione
inserita in questo file.

static
~~~~~~

In questa cartella sono inseriti gli asset statici che vengono pubblicati
dal server in modo diretto; è qui che metteremo file tipo ``favicon.png``
o ``robots.txt``.


src
~~~

È in questa cartella che troviamo tutti i fale che definiscono la nostra
applicazione.

.. code-block:: shell

  src/
  ├ routes/
  │ └ +page.svelte
  └ app.html

Per ora il nostro progetto vuooto contiene solo due file:

- ``app.html`` la pagina template - un documento HTML, vedremo in \
  seguito da cosa è composto
- ``+page.svelte`` all'interno della cartella ``routes`` che rappresenta \
  la pagina iniziale del nostro progetto.

