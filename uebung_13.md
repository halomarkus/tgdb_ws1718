A1)select * from artikel where INITCAP(bezeichnung) AND length(bezeichnung)=4;
ALTER TABLE artikel
ADD CONSTRAINT u_gas_name
CHECK (REGEXP_LIKE(bezeichnung, '^[A-Z](1,4).*$', 'c'));


A2)select artikelnr from artikel;
ALTER TABLE artikel
ADD CONSTRAINT u_gas_name
CHECK (REGEXP_LIKE(artikelnr, '^[1](1):[0-3,5-9](1,2).*$', 'c'));

A3)select p.name, count(b.bestellnr)
from person p
LEFT JOIN bestellung b ON p.pnr=b.pnr;

A4)CREATE TABLE Bestellposition(
bestellnr INTEGER NOT NULL,
artikelnr INTEGER NOT NULL,
lieferungsnr INTEGER,
menege);

A5)ALTER TABLE Bestellung ADD CONSTRAINT c_test CHECK(bestellnr>0);

A6)ALTER TABLE BESTELLposition ADD CONSTRAINT c_PK PRIMARY KEY(bestellnr,artikelnr);

ALTER TABLE BESTELLposition ADD CONSTRAINT FK_BEST_LIEF FOREIGN KEY(lieferungsnr) REFERENCES lieferung(lieferungsnr);
ALTER TABLE Bestellposition ADD CONSTRAINT FK_artikel FOREIGN KEY(artikelnr) REFERENCES artikel(artikelnr);
ALTER TABLE BESTELLPOSITION ADD CONSTRAINT FK_bestellung FOREIGN KEY(bestellnr) REFERENCES bestellung(bestellnr);

A7)
start <Dateipfad/zur/sql-dump-datei.sql>

A8)CREATE SEQUENCE Person_SEQ
START WITH 1000;

CREATE OR REPLACE TRIGGER trig_BIU
BEFORE INSERT OR UPDATE ON PERSON
FOR EACH
IF(INSERTING)THEN
:NEW.PNR:=PERSON_SEQ.NEXTVAL;
END IF;

IF(UPDATING(PNR))THEN
DBMS_OUTPUT.PUT_LINE('NICHT MÖGLICH');
END IF;
END;
/

A9)INSERT INTO BESTELLUNG VALUES('100',SYSDATE,(SELECT P.PNR FROM PERSON P WHERE NAME LIKE '%Mc%'));

A10)GRANT SElect,UPdate!=artikel * from artikel to SCOTT;

A11)DELETE from person p WHERE datum<=sysdate-INTERVAL '1' YEAR;

A12)select name,geburtsdatum
from person 
ORDER BY name DESC,geburtsdatum ASC;

A13)UPDATE ARTIKEL
SET preis =preis*1.05;

A14)select * from bestellung where lieferungsnr not exists( select lieferungsnr from bestellposition);

A15)select name from person where geburtsdatum>=sysdate-INTERVAL '18' YEAR;

A16)select name from person where lenght(name)>=5AND length(name)<=10 AND name LIKE '%-%';
