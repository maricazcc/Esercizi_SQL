# Esercizi_SQL

Il database UNIVERSITA è formato dalle seguenti tabelle:

Tabella Dipartimenti
- id_dipartimento INT AUTO_INCREMENT PRIMARY KEY
- nome VARCHAR(100) NOT NULL UNIQUE

Tabella Docenti (many-to-one Dipartimenti )
- id_docente INT AUTO_INCREMENT PRIMARY KEY
- nome VARCHAR(50) NOT NULL
- cognome VARCHAR(50) NOT NULL
- email VARCHAR(100) NOT NULL UNIQUE
// FK
- id_dipartimento INT NOT NULL 

Tabella Corsi (many-to-one Docenti)
- id_corso INT AUTO_INCREMENT PRIMARY KEY
- nome VARCHAR(100) NOT NULL,
// FK 
- id_docente INT NOT NULL 

Tabella Aule
- id_aula INT AUTO_INCREMENT PRIMARY KEY
- nome VARCHAR(50) NOT NULL,
- capienza INT NOT NULL

Tabella Studenti
- id_studente INT AUTO_INCREMENT PRIMARY KEY
- nome VARCHAR(50) NOT NULL
- cognome VARCHAR(50) NOT NULL
- email VARCHAR(100) NOT NULL UNIQUE
- data_nascita DATE
- telefono VARCHAR(20)
- indirizzo VARCHAR(100)
- citta VARCHAR(50)

Tabella Iscrizioni (Tabella ponte realizza many-to-many Studenti-Corsi)
- id_iscrizione INT AUTO_INCREMENT PRIMARY KEY
- data_iscrizione DATE NOT NULL DEFAULT (CURRENT_DATE)
// FK
id_studente INT NOT NULL
// FK
id_corso INT NOT NULL
// UNIQUE composta: è la combinazione id_studente, id_corso
UNIQUE (id_studente, id_corso)

Tabella Esami (one-to-one Studenti-Corsi)
- id_esame INT AUTO_INCREMENT PRIMARY KEY
// FK
- id_studente INT NOT NULL
// FK
- id_corso INT NOT NULL
- voto INT CHECK(voto BETWEEN 18 AND 30)
- data_esame DATE NOT NULL DEFAULT (CURRENT_DATE)
- UNIQUE (id_studente, id_corso)

Tabella Calendario_Lezioni (many-to-one Corsi)
- id_lezione INT AUTO_INCREMENT PRIMARY KEY
// FK
- id_corso INT NOT NULL
// FK
- id_aula INT NOT NULL
// FK
- id_docente INT NOT NULL,
- giorno_settimana ENUM('Lunedi','Martedi','Mercoledi','Giovedi','Venerdi') NOT NULL
- orario_inizio TIME NOT NULL
- orario_fine TIME NOT NULL
