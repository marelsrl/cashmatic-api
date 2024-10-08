# CASHMATIC-API


## Api Javascript per interfacciarsi con i sistemi cashmatic
### 3 classi principali:
1. *CashmaticDeviceInfo* : Serve per ottenere i dati della macchina
2. *CashmaticOperations* : Serve per svolgere tutte le operazioni necessarie, come il refill o il prelievo
3. *Utility*: questa contiene alcune funzioni extra come reboot(per riavviare la cassa) e report, per ottenere un report dettagliato del sistema in formato JSON

### Utils.js
Questo file esporta alcune funzioni "composte" utili: **startWithdrawKeepAlive** Questa funzione rimane in sospeso fin quando non termina la riscossione, **startPaymentKeepAlive** questa funzione rimane sospesa fin quando il pagamentyo non termina o va in timeout e **downloadReport** per scaricare il report in formato JSON

## UTILIZZO
```js
git clone https://github.com/marelsrl/cashmatic-api
npm install
```


## METODI

### CashmaticDeviceInfo
* allLevels: ritorna tutti i livelli monetari

* activeTransaction: per ottenere le informazioni della transazione corrente 
* activeTransactionPercentage: per ottenere lo stato della transazione corrente in percentuale
* lastTransaction: per le informazioni sull'ultima transazione svolta
* activeOperation: per ricevere una stringa che descrive lo stato della macchina "idle" di default
* userData: questa funzione serve per ottenre le informazioni sull'utente corrente della cassa

* info: per leeggere le informazioni di base della cassa, come versione, modello, numero seriale ecc..


### CashmaticOperations
* login: per accedere e ottenere il Bearer token
* renewToken: per aggiornare il token della sessione (scade ogni 10 minuti)
* startRefill: per avviare il refill (non rimane in sospensione)
* stopRefill: per arrestare il refill corrente
* startPayments: per avviare un pagamento (non rimane in sospensione)
* cancelPayments: per cancellare il pagamento in corso
* commitPayments: per accettare il pagamento corrente, anche se non si è raggiunta la somma richiesta
* startWithdrawal: per avviare un prelievo
* emptyCashbox: per svuotare il cashbox




### CashmaticUtility
* report: per ottenere il report della macchina in JSON
* powerOff: per spegnere la cassa
* reboot: per riavviare la cassa

<br/>

** Ps. 
Per quasi tutte le operazioni è necessario il token, per qualsiasi dato obligatorio che non sia stato fornito l'api lancia un Errore.

L'api è documentata anche internamente, quindi cercando di accedere ai metodi delle classi vengono consigliati tramite i suggerimenti compresi i parametri richiesti e il dato di ritorno.

Per la configurazione, come porte, ip ecc.. modificare il file .env