# Descrizione:

Create un nuovo progetto utilizzando Vite e Vue 3 e definite i componenti necessari per strutturare il layout come da screenshot allegato.

Al caricamento della pagina, effettuate una chiama ajax all'API di Yu Gi Oh: https://db.ygoprodeck.com/api/v7/cardinfo.php
e con i dati restituiti, stampate una card per ogni carta.

## ATTENZIONE:

l'api restituisce tutti i risultati in un colpo solo. Per evitare attese e/o rallentamenti nelle richieste, potete diminuire il numero di risultati sfruttando i parametri num e offset
https://db.ygoprodeck.com/api/v7/cardinfo.php?num=20&offset=0

## Bonus:

Creare un componente loader da visualizzare fintantoché i risultati non sono pronti.
Documentazione: https://ygoprodeck.com/api-guide/

### Svolgimento:

#### inserisco nel progetto anche la tanto amata bootstrap

per inserire bootstrap devo installare con il comando npm che trovo sul sito

- devo importare in main.js il file di mio interesse dalla cartella di bootstrap in node_modules

#### per prova inserisco anche font awesome

seguendo i passaggi suggeriti dal sito alla sezione "get started"

- installo il core
- installo i pacchetti di icone che mi interessano (free, ovvio)
  -installo i componenti
  -in main.js comincio a creare la mia libreria

#### per chiamare una API online devo usare Axios

axios server per leggere le api da dei siti interner e quindi ricavarne i dati che mi servono per la mia applicazione

- sul sito npmjs.com trovo il link per installare axios nel mio progetto (npm i axios)
- npm install axios

secondo filmato. dal minut0n 13.00
