<!--
Modellizzare la struttura di una tabella per memorizzare tutti i dati riguardanti una università:
- sono presenti diversi Dipartimenti (es.: Lettere e Filosofia, Matematica, Ingegneria ecc.);
- ogni Dipartimento offre più Corsi di Laurea (es.: Civiltà e Letterature Classiche, Informatica, Ingegneria Elettronica ecc..)
- ogni Corso di Laurea prevede diversi Corsi (es.: Letteratura Latina, Sistemi Operativi 1, Analisi Matematica 2 ecc.);
- ogni Corso può essere tenuto da diversi Insegnanti;
- ogni Corso prevede più appelli d'Esame;
- ogni Studente è iscritto ad un solo Corso di Laurea;
- ogni Studente può iscriversi a più appelli di Esame;
- per ogni appello d'Esame a cui lo Studente ha partecipato, è necessario memorizzare il voto ottenuto, anche se non sufficiente.
Pensiamo a quali entità (tabelle) creare per il nostro database e cerchiamo poi di stabilirne le relazioni. Infine, andiamo a definire le colonne e i tipi di dato di ogni tabella.
-->

## Table Name: University

- departements:
    - id: BIGINT | AUTO_INCREMENT, UNIQUE, NOTNULL
    - name: VARCHAR(255) | NOTNULL
    - chief: VARCHAR(50) | NOTNULL
    - description: TEXT| NULL

- degree_course:
    - id: BIGINT | AUTO_INCREMENT, UNIQUE, NOTNULL
    - name: VARCHAR(255) | NOTNULL
    - teachers: SMALLINT | NULL
    - students: SMALLINT | NULL
    - course: TINYINT | NULL
    - description: TEXT| NULL

- course:
    - id: BIGINT | AUTO_INCREMENT, UNIQUE, NOTNULL
    - name: VARCHAR(255) | NOTNULL
    - teacher: TINYINT | NULL
    - students: SMALLINT | NULL
    - exams: TINYINT | NULL
    - description: TEXT| NULL

- exam:
    - id: BIGINT | AUTO_INCREMENT, UNIQUE, NOTNULL
    - name: VARCHAR(255) | NOTNULL
    - date: DATE | NULL
    - students: SMALLINT | NULL
    - teacher_id: BIGINT | NOTNULL
    - votes: TINYINT | NOTNULL
    - description: TEXT| NULL

- teachers:
    - teacher_id: BIGINT | AUTO_INCREMENT, UNIQUE, NOTNULL
    - full_name: VARCHAR(50) | NOTNULL
    - subject: VARCHAR(255) | NOTNULL
    - course: VARCHAR(255) | NULL

- students:
    - id: BIGINT | AUTO_INCREMENT, UNIQUE, NOTNULL
    - full_name: VARCHAR(50) | NOTNULL
    - degree_course: VARCHAR(255) | NOTNULL
    - course: VARCHAR(255) | NULL
    - exams: VARCHAR(255) | NULL
    - vote: VARCHAR(20) | NULL