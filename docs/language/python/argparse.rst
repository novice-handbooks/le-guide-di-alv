argparse - Parser per opzioni da linea di comando, argomenti e sottocomandi.
============================================================================

.. note::
  I contenuti che seguono prendono forte ispirazione dalla documentazione
  ufficiale relativa della versione 3.11 di Python

  Link alla documentazione ufficiale: https://docs.python.org/3.11/library/argparse.html

Introduzione alla libreria
--------------------------

La libreria `argparse` in Python è utilizzata per analizzare gli argomenti
della riga di comando passati a uno script Python. Essa semplifica la
gestione degli argomenti forniti dall'utente, consentendo agli script di
essere eseguiti con opzioni specifiche o argomenti obbligatori.
L'utilizzo di `argparse` rende più facile per gli utenti interagire con
lo script senza dover modificare il codice sorgente.

Ecco alcune delle principali funzionalità e scopi di `argparse`:

1.  **Definizione degli argomenti**:
    `argparse` permette di definire quali argomenti e opzioni il tuo
    script può accettare. Puoi specificare argomenti obbligatori, opzionali,
    flag booleani e altro ancora.

2.  **Parsificazione degli argomenti**:
    `argparse` analizza gli argomenti passati dalla riga di comando e li
    rende disponibili nel tuo programma come oggetti Python.
    Puoi accedere a questi argomenti e utilizzarli nel tuo codice.

3.  **Gestione degli errori e messaggi di aiuto**:
    `argparse` fornisce un modo semplice per gestire errori, visualizzare
    messaggi di aiuto e documentazione sull'uso del tuo script.
    Gli utenti possono richiedere informazioni sull'uso degli argomenti
    attraverso l'opzione :code:`--help`.

4.  **Validazione degli argomenti**:
    `argparse` ti consente di definire regole di validazione per gli
    argomenti, come limiti di valore o scelte consentite.

5.  **Generazione automatica della documentazione**:
    Può generare automaticamente la documentazione basata sugli
    argomenti specificati, facilitando la creazione di una guida
    utente per il tuo script.

Concetti base
-------------

Di seguito vengono spiegate con piccoli esempi applicativi le funzionalità
che la libreria mette a disposizione del programmatore.

Partiamo con l'esempio più semplice di utilizzo di `argparse`. In questo
non richiediamo alcuna funzione specifica, ma come vedremo, la libreria
implementa automaticamente alcune funzionalità basilari.

.. code-block:: python
    :caption: prog.py
    :linenos:

    import argparse
    parser = argparse.ArgumentParser()
    parser.parse_args()

Tre righe di codice: la prima per importare la libreria, con la seconda
si instanzia un oggetto di classe  `ArgumentParser`, che mette a disposizione
il metodo :code:`parse_args()` richiamato nella terza riga.

Quindi alla fine questa semplice chiamata cosa fa?

Eseguimo il programma usando alcune combinazioni di parametri:

.. code-block:: shell
    :caption: assenza di argomenti

    $ python prog.py

Il programma esegue il *parsing* della linea di comando che non restituisce
nulla.

Ora proviamo a passare un argomento nella linea di comando:

.. code-block:: shell
    :caption: passando un argomento sconosciuto (foo)
    :emphasize-lines: 2-

    $ python prog.py foo
    usage: prog.py [-h]
    prog.py: error: unrecognized arguments: foo

Ecco che entra in gioco il metodo :code:`parse_args()` e non essendo istruito
a riconoscere alcun argomento ci presenta un messaggio di errore e termina
il programma.

Notare che il messaggio si compone di due parti:

- una spiegazione di utilizzo del programma con la presenza di
  una opzione :code:`-h`
- il messaggio di errore specifico per il non riconoscimento dell'argomento
  passato

Ecco quindi un primo automatismo messo a disposizione da `argparse`.

Ma abbiamo appena iniziato. Ora proviamo l'opzione :code:`-h`

.. code-block:: shell
    :caption: passando l'opzione -h
    :emphasize-lines: 2-

    $ python prog.py -h
    usage: prog.py [-h]

    options:
      -h, --help  show this help message and exit

In automatico `argparse` implementa la visualizzazione
dell'help della linea di comando. Di seguito andremo a vedere come
aggiungere informazioni, ma ora facciamo un ultimo esperimento e
proviamo a utilizzare una opzione sconosciuta

.. code-block:: shell
    :caption: passando un'opzione sconosciuta (--baz)
    :emphasize-lines: 2-

    $ python prog.py --baz
    usage: prog.py [-h]
    prog.py: error: unrecognized arguments: --baz

A questo punto c'era da aspettarselo, un bel messaggio di errore.

Con questi esempi abbiamo visto il comportamento della libreria in
assenza di una configurazione specifica. Ma noi vogliato sfruttare
la libreria per implementare la gestione di specifici argomenti della
linea di comando.

Argomenti posizionali
---------------------

Partendo dall'esempio precedente iniziamo ad aggiungere la gestione di
un nuovo argomento

.. code-block:: python
    :caption: prog.py
    :linenos:
    :emphasize-lines: 3-

    import argparse
    parser = argparse.ArgumentParser()
    parser.add_argument("message")
    args = parser.parse_args()
    # di seguito le funzioni dell'applicazione
    print(args.message)

Come evidenziato nel codice abbiamo aggiunto:

- chiamata la metodo :code:`add_argument()` con cui aggiungiamo la
  gestione del nuovo argomento `message`
- il risultato del metodo `parse_args()` viene memorizzato localmente
  con nome `args`
- linee della nostra, che in questo caso si limita a stampare
  a console il parametro `message` ricevuto

Abbiamo istruito `argparse` che la nostra applicazione **si aspetta**
di ricevere l'argomento `message` sulla linea di comando.

Proviamo come prima a lanciare la nostra app in tre condizioni: senza
argomenti, con l'argomento corretto, con l'opzione :code:`-h` per
visualizzare l'help.

.. code-block:: shell
    :caption: test con varie condizioni
    :emphasize-lines: 2-3, 5, 7-

    $ python prog.py
    usage: prog.py [-h] message
    prog.py: error: the following arguments are required: message
    $ python prog.py "Questo è il mio messaggio"
    Questo è il mio messaggio
    $ python prog.py -h
    usage: prog.py [-h] message

    positional arguments:
    message

    options:
      -h, --help  show this help message and exit

Nel primo caso il codice si interrompe con chiamata al metodo
:code:`parse_args()`, se righe che seguono non sono eseguite.

Utilizziamo l'applicazione come è stata pensata, e cioè passando correttamente
l'argomento, il codice prosegue e i valori passati come argomenti sono
restituiti dal metodo :code:`parse_args()`.

La visualizzazione dell'help relativamente al parametro `message` non fornisce
informazioni particolari. Nel codice seguente vediamo come aggiungere
queste informazioni.

.. code-block:: python
    :caption: prog.py
    :linenos:
    :emphasize-lines: 3

    import argparse
    parser = argparse.ArgumentParser()
    parser.add_argument("message", help="messaggio da stampare")
    args = parser.parse_args()
    # di seguito le funzioni dell'applicazione
    print(args.message)

