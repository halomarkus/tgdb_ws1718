# Tutorium - Grundlagen Datenbanken - Blatt 9

## Vorbereitungen
* Für dieses Aufgabenblatt wird die SQL-Dump-Datei `tutorium.sql` benötigt, die sich im Verzeichnis `sql` befindet.
* Die SQL-Dump-Datei wird in SQL-Plus mittels `start <Dateipfad/zur/sql-dump-datei.sql>` in die Datenbank importiert.
* Beispiele
  * Linux `start ~/Tutorium.sql`
  * Windows `start C:\Users\max.mustermann\Desktop\Tutorium.sql`

## Datenbankmodell
![Datenbankmodell](./img/datamodler_schema.png)

### Aufgabe 1
Wo liegen die Vor- und Nachteile eines Trigger in Vergleich zu einer Prozedur?

#### Lösung
-trigger knüpfe ich auf tabelle und wenn dann wird ein event ausgeführt.
-Trigger hängt an einer tabelle.
-bei ereignissen wird der code gebraucht
VORTEIL
-procedur kann auch funktion nutzen
-function gibt einen wert zurück
-FOR EACH ROW für jede zeile zu prüfen
NACHTEIL
-procedur gibt keinen wert zurück
-trigger können sich gegenseitig auslösen führt zu probelemen
-Bei trigger soll es verzögert sein da es in überteil reingeht

-Procedure ist mit is
-TRIGGER geht mit DECLARE

### Aufgabe 2
Wo drin unterscheidet sich der `Row Level Trigger` von einem `Statement Trigger`?

#### Lösung
Ein ROW level Trigger wird mehrmals aktiviert.
EIn Statement Trigger wird nur einmal aktiviert.

### Aufgabe 3
Schaue dir den folgenden PL/SQL-Code an. Was macht er?

```sql
CREATE SEQUENCE seq_account_id
START WITH 1000
INCREMENT BY 1
MAXVALUE 99999999
CYCLE
CACHE 20;

CREATE OR REPLACE TRIGGER BIU_ACCOUNT
BEFORE INSERT OR UPDATE OF account_id ON account
FOR EACH ROW
DECLARE

BEGIN
  IF UPDATING('account_id') THEN
    RAISE_APPLICATION_ERROR(-20001, 'Die Account-ID darf nicht verändert oder frei gewählt werden!');
  END IF;

  IF INSERTING THEN
    :NEW.account_id := seq_account_id.NEXTVAL;
  END IF;
END;
/
```

#### Lösung
CREATE SEQUENCE seq_account_id: Um mehrere eindeutige Zahlen zu generieren
oder primärschlüssel anlegen.
START WITH 1000: Startwert
INCREMENT BY 1: Schrittgrösse beim hochzählen
MAXVALUE 99999999: Grösster Wert
CYCLE: Wieder bei Minvalue starten wenn MaxValue überschritten wurde
CACHE 20:Das ganze soll 20x durchgeführt werden.

CREATE OR REPLACE TRIGGER BIU_ACCOUNT: Ein Trigger wird angelegt
BEFORE INSERT OR UPDATE OF account_id ON account:bevor die ereignisse ausgeführt werden
ON ist die tabelle
FOR EACH ROW:werden pro geänderter Zeile ausgeführt
DECLARE: deklariere variablen
BEGIN: Starte
IF UPDATING('account_id') THEN:Hier wird die account_id verändert
RAISE_APPLICATION_ERROR(-20001, 'Die Account-ID darf nicht verändert oder frei gewählt werden!'): werfe einen fehler
END IF: Ende der Schleife
IF INSERTING THEN: es soll etwas eingesetzt werden
:NEW.account_id := seq_account_id.NEXTVAL:neue account id


### Aufgabe 4
Verbessere den Trigger aus Aufgabe 2 so, dass
+ wenn versucht wird einen Datensatz mit `NULL` Werten zu füllen, die alten Wert für alle Spalten, die als `NOT NULL` gekennzeichnet sind, behalten bleiben.
+ es nicht möglich ist, das die Werte für `C_DATE` und `U_DATE` in der Zukunkt liegen
+ `U_DATE` >= `C_DATE` sein muss
+ der erste Buchstabe jedes Wortes im Vor- und Nachnamen groß geschrieben wird
+ die Account-ID aus einer `SEQUENCE` entnommen wird

Nutze die Lösung der Aufgabe 2, Aufgabenblatt 8 um die Aufgabe zu lösen. Dort solltest du einige Hilfestellungen finden.

#### Lösung
```sql
Deine Lösung
```

### Aufgabe 5
Angenommen der Steuersatz in Deutschland sinkt von 19% auf 17%.
+ Aktualisiere den Steuersatz von Deutschland und
+ alle Quittungen die nach dem `01.10.2017` gespeichert wurden.

#### Lösung
```sql
Deine Lösung
```

### Aufgabe 6
Liste alle Hersteller auf, die LKW's produzieren und verknüpfe diese ggfl. mit den Eigentümern.

#### Lösung
```sql
Deine Lösung
```


























