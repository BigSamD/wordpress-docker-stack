# Configurazione Docker Compose per WordPress, MySQL e PhpMyAdmin

Questa configurazione di Docker Compose ti permette di avviare facilmente un sito WordPress affiancato da un database MySQL e PhpMyAdmin per la gestione del database.

## Versione

Versione Docker Compose: `3.3`

## Servizi

### 1. Database (MySQL)

- **Immagine**: `mysql:5.7`
- **Variabili d'ambiente**:

  - Password Root: `password`
  - Database: `wordpress`
  - Utente: `wordpress`
  - Password: `wordpress`
- **Rete**: `wpsite`
- **Volume Dati**: `db_data` in `/var/lib/mysql`

### 2. PhpMyAdmin

- **Immagine**: `phpmyadmin/phpmyadmin`
- **Porte**: `8080` sull'host mappato su `80` nel container
- **Variabili d'ambiente**:

  - Host: `db`
  - Password Root: `password`
- **Rete**: `wpsite`
- **Dipendenze**: Dipende dal servizio `db` per essere operativo

### 3. WordPress

- **Immagine**: `wordpress:latest`
- **Porte**: `8000` sull'host mappato su `80` nel container
- **Variabili d'ambiente**:

  - Host DB: `db:3306`
  - Utente DB: `wordpress`
  - Password DB: `wordpress`
  - Nome DB: `wordpress`
- **Rete**: `wpsite`
- **Dipendenze**: Dipende dal servizio `db` per essere operativo
- **Volume**: Mappa la directory corrente su `/var/www/html` nel container

## Reti

- `wpsite`

## Volumi

- `db_data`: Un volume nominato per rendere persistenti i dati del database MySQL

## Utilizzo

1. Assicurati di avere Docker e Docker Compose installati sulla tua macchina.
2. Clona questa repository o scarica il file `docker-compose.yml`.
3. Esegui il comando `docker-compose up -d` dalla directory che contiene il file.
4. Accedi a WordPress su `http://localhost:8000` e PhpMyAdmin su `http://localhost:8080`.

## Arresto dei Servizi

Per fermare i servizi, esegui il comando `docker-compose down`. Se desideri rimuovere anche i volumi (dati), esegui `docker-compose down -v`.
