# How to - use cases

- Test eseguiti su singola vm, lanciati da dentro la vm

    \+ massimo isolamento

    \+ il piu' vicino possibile al 'utonto che inserisce comandi nella shell'

    \+ buone prestazioni

    \- alcune limitazioni su cio' che possono fare i test. e.g.: azioni distruttive che impattano sull'esecuzione
    dei test stessi (o i relativi file) o dell'os. l'intera test suite potrebbe fallire male

    \- il guest os deve poter installare ssh (per la connessione di ansible), python3.x, pip, python3-venv

    \- i test possono includere solamente la singola vm

- Test eseguiti su singola vm, lanciati all'esterno e connessi alla vm via ssh o seriale (grazie a libvirt)

    \+ buon isolamento (introduce la dipendenza dei tool utilizzati per connettersi alla vm)

    \+ buone prestazioni

    \+ la test suite resiste a azioni distruttive, fallendo al massimo dei test, poiche' esegue
    fuori dalla vm stessa

    \- se viene usato come metodo di connessione, il guest os deve avere ssh installato

    \- i test possono includere solamente la singola vm

    \- i test stessi devono gestire anche la connessione alla vm (forse si riesce a delegare ed astrearre questa
    parte ad una libreria ad-hoc)

- Test eseguiti su multiple vm annidate dentro una vm radice, dentro la quale vengono lanciati i test che si attaccano alle vm annidate via ssh/seriale

    \+ permettono di scrivere test che fanno interagire macchine diverse

    \+ buon isolamento, poiche' le vm internet e la rete tra di esse e' completamente sotto il controllo del test

    \- prestazioni accettabili solo se in paravirtualizzazione

    \- se viene usato come metodo di connessione, il guest os deve avere ssh installato

    \- i test stessi devono gestire anche la connessione alla vm (forse si riesce a delegare ed astrearre questa

- Test eseguiti su multiple vm, lanciati all'esterno e connessi alle vm via ssh/seriale

    \+ permettono di scrivere test che fanno interagire macchine diverse

    \+ isolamento accettabile, anche se ridotto rispetto alle altre opzioni, poiche' la rete e le vm sono
    gestite dall'os della farm

    \+ prestazioni accettabili (anche se le vm multiple sono in qemu)

    \- se viene usato come metodo di connessione, il guest os deve avere ssh installato

    \- i test stessi devono gestire anche la connessione alla vm (forse si riesce a delegare ed astrearre questa