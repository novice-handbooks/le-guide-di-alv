argparse
========

.. note::
  Link alla documentazione ufficiale: https://docs.python.org/3/library/argparse.html

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

Ecco un esempio semplice di come usare `argparse`:

.. code-block:: python
  :emphasize-lines: 0

  import argparse

  parser = argparse.ArgumentParser(description='Esempio di utilizzo di argparse')

  # Definizione di un argomento obbligatorio
  parser.add_argument('arg1', type=int, help='Un argomento obbligatorio di tipo intero')

  # Definizione di un argomento opzionale
  parser.add_argument('--opzionale', type=str, help='Un argomento opzionale di tipo stringa')

  # Parsificazione degli argomenti
  args = parser.parse_args()

  # Accesso agli argomenti
  print('Argomento obbligatorio:', args.arg1)
  print('Argomento opzionale:', args.opzionale)


In questo esempio, `argparse` viene utilizzato per definire un argomento
obbligatorio di tipo intero (`arg1`) e un argomento opzionale di tipo
stringa (`opzionale`).
Gli utenti possono passare questi argomenti dalla riga di comando quando
eseguono lo script.
