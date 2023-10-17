Gestire gli `ambienti virtuali` e versioni multiple di Python
=============================================================

Una cosa la mettiamo subito in chiaro: se programmiamo in Python,
per evitare spiacevoli problemi di compatibilità tra le librerie
utilizzate **dobbiamo** utilizzare utilizzare gli `ambienti virtuali`,
normalmente identificati con il termine *"virtual environments"*.

Questo comporta che non si devono **mai** aggiungere librerie
necessarie per le nostra applicazioni all'installazione base del sistema.

Virtual Environments
--------------------

Un virtual environment in Python è un meccanismo utilizzato per
isolare l'ambiente di sviluppo e le dipendenze di un progetto
specifico. Questo consente agli sviluppatori di mantenere le
librerie e le versioni di Python utilizzate in un progetto
separato da quelle di altri progetti, evitando potenziali conflitti
tra le diverse versioni delle librerie.

venv
++++

Il modo più veloce per creare un virtual environment è mediante
il modulo :code:`venv` [#url]_ di Python:

.. code-block:: shell

    python -m venv env

Questo crea un ambiente virtuale nella directory 'env'.
In questa directory sono copiati gli eseguibili di Python e
in essa verranno anche installate tutte le librerie necessarie
per il nostro progetto.

Affinchè questo avvenga occorre istruire il nostro sistema di
utilizzare questo `virtual environment`:

.. code-block:: shell

    source env/bin/activate

.. note::

    Il comando per attivare l'ambiente può differire in base alla
    piattaforma ed alla shell utilizzate:

    +-------------+------------+-------------------------------------------+
    | Piattaforma | Shell      | Comando attivazione virtual environment   |
    +=============+============+===========================================+
    | POSIX       | bash/zsh   | :code:`$ source env/bin/activate`         |
    |             +------------+-------------------------------------------+
    |             | fish       | :code:`$ source env/bin/activate.fish`    |
    |             +------------+-------------------------------------------+
    |             | csh/tcsh   | :code:`$ source env/bin/activate.csh`     |
    |             +------------+-------------------------------------------+
    |             | PowerShell | :code:`$ env/bin/Activate.ps1`            |
    +-------------+------------+-------------------------------------------+
    | Windows     | cmd.exe    | :code:`C:\\>env\\Scripts\\activate.bat`   |
    |             +------------+-------------------------------------------+
    |             | PowerShell | :code:`PS C:\\> env\\Sripts\\Activate.ps1`|
    +-------------+------------+-------------------------------------------+

Dopo aver attivato l'ambiente qualunque installazione eseguita con
'pip install **package**' verrà fisicamente inserita all'interno della
directory *env*.

Per uscire dall'ambiente virtuale basta impartire il comando :code:`deactivate`

Poetry
++++++

**Poetry** [#poetry]_ è uno strumento per gestire il progetto, oltre alla
gestione di ambienti virtuali, ha anche la capacità di gestire le dipendenze
delle librerie, cosa non presente qualora si utilizzi la sola accoppiata
`venv/pip`.

Poetry non è parte della installazione nativa di Python ma deve essere
installato autonomamente seguendo le indicazioni presenti nel sito ufficiale.

Una volta installato poetry sono consigliate alcune modifiche alla
configurazione di default:

.. code-block:: shell

    poetry config virtualenvs.in-project true
    poetry config virtualenvs.options.always-copy true
    poetry config virtualenvs.prefer-active-python true

La prima modifica andrà a creare gli ambienti virtuali all’interno della
directory di progetto, la seconda farà una copia dei tool invece di creare
dei symbolic links, la terza utilizzerà la versione correntemente attivata
di Python invece di quella utilizzata per installare Poetry.

Per utilizzare Poetry occorre per prima cosa inizializzare il proprio
progetto : :code:`poetry init`.
Questo genererà il file pyproject.toml che contiene una descrizione del
progetto come definito durante il comando init.

Infine, :code:`poetry shell` creerà l’ambiente virtuale in una directory
nascosta (.venv) con gli eventuali pacchetti definiti durante
l’inizializzazione, e attiverà lo stesso ambiente virtuale.

L'installazione di librerie avviene tramite il comando
:code:`poetry add <package>`


Pyenv
+++++

`Pyenv` [#pyenv]_ in Linux e MacOS, e `pyenv-win` [#pyenvw]_ in Windows
sono gli strumenti utilizzati per installare versioni multiple di Python
sul sistema.

Ci sono molti tutorial sul web, qui è sufficiente dire che il tool viene
installato e si occupa di creare e gestire link simbolici e vari files
per gestire le versioni di Python installate localmente.

Installate localmente significa che Python viene installato sotto la
home directory, dentro ~/.pyenv/… e a questa directory si fa riferimento
dagli script. Per gli utenti Linux, Pyenv non tocca mai l’installazione
di sistema. Anche quando si legge di un Global Python Interpreter,
significa quello di default per i progetti.

Solo per esempio, :code:`pyenv versions` mostrerà le versioni installate
ed utilizzate attualmente:

.. TODO

    Inserire risultato del comando "pyenv versions"



:code:`pyenv local 3.10` installerà (se non già presente) Python 3.10
e la selezionerà come versione di default per la directory corrente.

Gestire il progetto con Poetry permette di impostare la versione di
Python per il progetto, ma non di gestire le versioni di Python installate.

La sequenza suggerita per gestire correttamente il tutto è la seguente:

.. code-block:: shell

    pyenv local 3.10 # Set the local version to 3.10
    poetry env use $(which python) # set the python version to the current one

Il primo comando imposta la versione locale di Python alla 3.10.
Il comando successivo imposta l’ambiente utilizzato da poetry alla
versione di python attiva al momento (ovvero la 3.10 per via del
comando precedente). Qui va fatta attenzione: l’ambiente virtuale non
deve essere attivo, altrimenti la versione di python impostata sarà
quella dell’ambiente virtuale, e la dipendenza python di poetry
(che viene evidenziata nella sezione `tool.poetry.dependencies`
nel file pyproject.toml) dovrebbe essere già corretta:

.. TODO

    Visualizzare contenuto del file "pyproject.toml"

Il risultato del comando poetry env use sarà il seguente, confermato
dal comando :code:`poetry env info` :

.. TODO

    Visualizzare il risultato del comando "poetry env info"

La versione di Python è stata cambiata, e viene confermato dal comando info.
Da notare che l’ambiente virtuale è stato ricreato.

Conclusioni
+++++++++++

Anche se questo setup può sembrare confusionario e complesso,
l’adozione di ambienti virtuali, poetry e pyenv permette isolamento
e distacco del progetto dal sistema locale, permettendo un notevole
grado di flessibilità e robustezza nello sviluppo Python.


.. [#url] https://docs.python.org/3/library/venv.html
.. [#poetry] https://python-poetry.org/
.. [#pyenv] https://github.com/pyenv/pyenv
.. [#pyenvw] https://github.com/pyenv-win/pyenv-win
