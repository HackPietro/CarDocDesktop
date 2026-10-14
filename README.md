# CarDoc Desktop

Applicazione desktop in **Java e JavaFX** per l'acquisto online di ricambi e accessori per auto. L'utente cerca i prodotti per parola chiave o per categoria, li salva in una wishlist, li aggiunge al carrello e completa l'ordine usando il saldo del proprio account, che si ricarica con codici coupon. Ogni utente ha anche un **garage** con i propri veicoli.

Progetto universitario per il corso di **User Interfaces Design**, finalizzato all'apprendimento di **Java, FXML e CSS**.

---

## Funzionalità

### Navigazione e ricerca

- **Home** con una panoramica dei prodotti
- **Ricerca** per parola chiave, ad esempio "filtro olio panda"
- **Otto categorie**: ammortizzatori, filtri, freni, illuminazione, oli, pneumatici, pulizia, scarico
- **Scheda prodotto** con descrizione, venditore, disponibilità, prezzo e prodotti simili
- **Tema chiaro e scuro**, selezionabile dall'interfaccia
- Pagine informative su app, privacy, condizioni generali di vendita e upgrade a premium

### Account

- **Registrazione** con controllo dei campi: email valida e non già associata a un altro account, password di almeno 6 caratteri, conferma password uguale
- **Login** e logout, con password cifrate tramite BCrypt
- **Recupero password** dalla schermata di accesso
- Nella sezione **Account**: indirizzo di spedizione, cambio password, saldo, ricarica con coupon e **storico degli ordini**

### Acquisti

- **Carrello**: aggiunta dei prodotti con quantità, rimozione, totale aggiornato e svuotamento
- **Ordine**: viene completato solo se il saldo copre il totale, altrimenti l'app invita a ricaricare l'account; con carrello vuoto o senza login l'ordine non parte
- **Wishlist** personale, fino a 6 prodotti, senza duplicati
- **Garage**: scelta dell'auto tra marca e modello disponibili (Fiat Panda e Volkswagen Golf), senza duplicati. Altri veicoli saranno disponibili con l'upgrade a premium, presentato nell'app come funzione futura

---

## Codici coupon

I coupon aggiungono credito al saldo dell'account e **ciascun codice è utilizzabile una sola volta**. Quando viene usato, viene eliminato dal database.

| Codice | Valore |
|:---:|:---:|
| `1` | 100 € |
| `2` | 200 € |
| `3` | 300 € |
| `4` | 400 € |
| `5` | 500 € |

> Il `database.db` incluso nel repository contiene i codici da `2` a `5`: il codice `1` è già stato utilizzato.

---

## Tecnologie

| Ambito | Tecnologia |
|---|---|
| Linguaggio | Java 17 |
| Interfaccia | JavaFX 17.0.2, FXML, CSS, Ikonli (icone) |
| Database | SQLite (`sqlite-jdbc`) |
| Sicurezza | Password cifrate con BCrypt (`spring-security-crypto`) |
| Build | Maven (con Maven Wrapper) |
| Test | JUnit 5 |

---

## Struttura del repository

```
CarDocDesktop/
├── database.db                              # Database SQLite con dati di esempio
├── pom.xml
├── mvnw / mvnw.cmd                          # Maven Wrapper
└── src/main/
    ├── java/com/progetto/uid/progettouid/
    │   ├── Controller/                      # Controller JavaFX (home, carrello, garage, account...)
    │   │   └── Handler/                     # Stato condiviso (prodotto selezionato)
    │   ├── DataBase/                        # Connessione, autenticazione, validazione
    │   ├── Model/                           # Product, User
    │   ├── View/                            # SceneHandler: scene, alert e tema
    │   └── Message.java                     # Messaggi e testi informativi dell'app
    └── resources/com/progetto/uid/progettouid/
        ├── fxmls/                           # Schermate FXML
        ├── css/                             # Stili: base, tema chiaro, tema scuro, font
        ├── immagini/                        # Immagini dei prodotti
        └── fonts/Roboto/                    # Font
```

---

## Database

Il database è un file SQLite, `database.db`, con sei tabelle:

| Tabella | Contenuto |
|---|---|
| `utenti` | Nome, cognome, email (chiave primaria), password cifrata, indirizzo, saldo |
| `prodotti` | ID, nome, prezzo, venditore, descrizione, categoria, parole chiave per la ricerca |
| `carrello` | Prodotti nel carrello e ordini completati: la colonna `tipo` distingue i due casi, `numero` e `totale` identificano l'ordine |
| `wishlist` | Coppie utente e prodotto salvato |
| `utente_auto` | Veicoli del garage di ogni utente |
| `coupon` | Codici ricarica e relativo valore |

Il file incluso contiene 48 prodotti, 6 per ciascuna delle 8 categorie.

---

## Avvio del progetto

**Requisiti**: JDK 17 e Maven.

1. Clona il repository:

   ```bash
   git clone https://github.com/HackPietro/CarDocDesktop.git
   cd CarDocDesktop
   ```

2. Apri il progetto in un IDE (ad esempio IntelliJ IDEA) ed esegui la classe `com.progetto.uid.progettouid.Main`.

> Il database viene aperto con il percorso relativo `database.db`, quindi l'applicazione va avviata dalla cartella principale del repository, quella che lo contiene.

---

## Autori

**Pietro Cimino** · [@HackPietro](https://github.com/HackPietro), **Francesco Campagna**, **Cataldo Federico**
