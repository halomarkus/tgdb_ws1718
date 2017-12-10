# Tutorium - Grundlagen Datenbanken - Blatt 10

## Vorbereitungen
* Für dieses Aufgabenblatt wird die SQL-Dump-Datei `tutorium.sql` benötigt, die sich im Verzeichnis `sql` befindet.
* Die SQL-Dump-Datei wird in SQL-Plus mittels `start <Dateipfad/zur/sql-dump-datei.sql>` in die Datenbank importiert.
* Beispiele
  * Linux `start ~/Tutorium.sql`
  * Windows `start C:\Users\max.mustermann\Desktop\Tutorium.sql`

## Datenbankmodell
![Datenbankmodell](./img/datamodler_schema.png)

### Aufgabe 1
Was macht der folgende SQL-Code?

```sql
WITH vehicles AS (
    SELECT COUNT(*) Anzahl, accv.account_id
    FROM acc_vehic accv
    GROUP BY accv.account_id
)
SELECT CONCAT(a.forename, CONCAT(' ', a.surname)) AS "Benutzer" , v.Anzahl AS "Anzahl"
FROM vehicles v
    INNER JOIN account a ON (v.account_id = a.account_id)
WHERE v.Anzahl = (
    SELECT MAX(Anzahl)
    FROM vehicles
);
```

#### Lösung
WITH vehicles AS //Gibt temporäres resultat wird abgeleitet von ausführungsbereich einer select/insert/update oder delete
SELECT COUNT(*) Anzahl, accv.account_id //COUNT(*) zählt alle Zeilen zusätzlich wird die ID ausgegeben
FROM acc_vehic accv //von der Tabelle account_vehicle
GROUP BY accv.account_id //gruppiert nach dem acc_id
)// with geschlossen
SELECT CONCAT(a.forename, CONCAT(' ', a.surname)) AS "Benutzer" , v.Anzahl AS "Anzahl"// returnt strings zwei oder mehr werte
FROM vehicles v //von der tabelle vehicle
INNER JOIN account a ON (v.account_id = a.account_id)//verknüpfe die Tabellen
WHERE v.Anzahl = ( //wo in der Tabelle vehicle die Anzahl
SELECT MAX(Anzahl)//der maximalen anzahl von oben
 FROM vehicles); //aus der Tabelle vehicle selektiert wird.

### Aufgabe 2
Die folgende Aufgabe bezieht sich auf das Datenbankmodell der Vorlesung.
Geben Sie mit einem SQL Befehl alle Klausuren aus, zu denen sich Personen angemeldet haben, aber bei **ALLEN** angemeldeten Personen fehlt die Note.

#### Lösung
```sql
Deine Lösung
`select * from studentische_person sp
  2  INNER JOIN anmeldung a ON sp.matrikelnr=a.matrikelnr
  3  WHERE a.note IS NULL;`
`
WITH anmeld as
  2  (select name
  3  from studentische_person sp
  4  INNER JOIN anmeldung a ON sp.matrikelnr=a.matrikelnr)
  5  select note from anmeldung
  6  WHERE note IS NULL;

### Aufgabe 3
Finde mit der Option `EXISTS` herraus, wie viele Hersteller in der Datenbank hinterlegt sind ohne mit einem Auto verknüpft zu sein.

#### Lösung
```sql
Deine Lösung
`select producer_name from producer
  2  WHERE NOT EXISTS
  3  (select * from vehicle WHERE vehicle_ID IS NULL);`
`select producer_name from producer
  2  WHERE EXISTS
  3  (select * from vehicle WHERE vehicle_ID IS NULL);
select producer_name from producer p
  2  LEFT JOIN vehicle v ON p.producer_ID=v.producer_ID;
select producer_name from producer p
  2  RIGHT JOIN vehicle v ON p.producer_ID=v.producer_ID;