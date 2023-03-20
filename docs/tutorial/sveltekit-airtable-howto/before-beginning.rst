-----------------
Prima di iniziare
-----------------

La guida vuole guidare il lettore nella creazione di una applicazione
di esempio, utilizzata per lo più come istruzione per l'utilizzo del
framework SvelteKit nelle sue principali funzionalità.

Nasce come raccolta personale di appunti durante la mia attività di
studio dello strumento, quindi non vuole essere una guida completa, ma
un semplice punto di riferimento per l'utilizzo del framework.

Nella scrittura si presuppone che il lettore conosca i linguaggi base
dello sviluppo web, come HTML, CSS, JavaScript.

Predisposizione dell'ambiente di sviluppo
-----------------------------------------

Per poter utilizzare Sveltekit, dobbiamo avere una versione
di `node.js <https://nodejs.org/>`_ installata sul nostro computer.
In particolare dobbiamo avere la versione `v16.9` o superiore.

.. NOTE::
    La procedura di installazione di `node.js` non ricade nello
    scopo della presente guida.

    Per maggiori informazioni a riguardo si rimanda alla
    lettura della pagina dedicata al download del sito
    ufficiale: <https://nodejs.org/en/download/>.

Accertiamoci che `node.js` sia installato correttamente::

  $ node -v
  v16.16.0

Ovviamente il comando serve per verificare la versione installata,
e risponderà con la versione corrispondente.

IDE consigliato
---------------

Sebbene i file sorgenti siano rappresentati da file testuali,
facilmente editabili con un qualsiasi editor di testo, si consiglia
vivamente di utilizzare un *Ambiente di Sviluppo Integrato* (IDE).

In particolare mi sento di consigliare
`Visual Studio Code <https://code.visualstudio.com>`_
che, grazie alle funzionalità integrate ed alla vasta disponibilità
di estensioni dedicate, facilita enormemente la scrittura e la correzione
del codice. Tra le estensioni, ovviamente , consiglio di installare
`Svelte for VS Code <https://marketplace.visualstudio.com/items?itemName=svelte.svelte-vscode>`_


