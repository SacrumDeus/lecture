# Einführung in ABAP

![Einführung in ABAP](./../src/abap-control-introduction.png)

## Was ist SAP ABAP?

SAP ABAP ist eine Programmiersprache für das SAP System zur Entwicklung kommerzieller Anwendungen.

Die Abkürzung steht für **A**dvanced **B**usiness **A**pplication **P**rogramming. Bei ABAP handelt es sich um eine *proprietäre* Programmiersprache, welche objektorientierte, imperative und funktionale Elemente hat.

> **Was bedeutet "proprietär"?**
>
> In der IT wird zwischen *Open Source* und *Proprietär* unterschieden. Hierbei bedeutet proprietär *in Eigentum befindlich*. Es wird auch häufig als *Closed Source* bezeichnet. Hierbei veröffentlicht der Inhaber nicht den Code und die Funktionen und veröffentlicht nur das "Endprodukt".
>
> Im Falle von SAP ABAP handelt es sich bei SAP ABAP um das Produkt.
>
> Beispiele für Closed Source Software sind:
> 
> * Microsoft Windows 
> * Microsoft Office
> * Apple macOS / Apple iOS

SAP ABAP wird verwendet um Anwendungen für SAP ERP-Systeme (on-Premise/Cloud) zu entwickeln. Andere SAP-Produkte nutzen nicht zwangsläufig SAP ABAP.

**Eigenschaften von ABAP**

* Es wird die prozedurale Entwicklung (Unterprogramme, Funktionsbausteine) unterstützt
* Es wird die objektorientierte Entwicklung (Klassen, Interfaces) unterstützt
* Es wird teilweise die funktionale Programmierung (List Comprehension) unterstützt
* Interne Tabellen als Bestandteil der Sprache
* Integrierter SQL-Zugriff auf Datenbanken
* Berechtigungen
* Abwärtskompatibel

> **Bedeutung der Abwärtskompatibilität**
>
> SAP ABAP ist Abwärtskompatibel. Das bedeutet, dass Programme, welche seit jahrzehnten nicht mehr aktualisiert wurden, nicht durch ABAP-Updates unbrauchbar werden. 
>
> Auswirkungen hat es auf den Sprach-Umfang, da die Anzahl an alten Befehlen (auch *Legacy Code* genannt) immer weiter anwächst. Dies erhöht die Komplexität des Codes.

**Weitere Links und Informationen**

* [Wikipedia - SAP ABAP](https://de.wikipedia.org/wiki/ABAP)

## Syntax von SAP ABAP

Die Sprache ABAP hat eine Grammatik, welche auch Syntax genannt wird. Wird diese Syntax nicht eingehalten, so kann das Programm nicht generiert und ausgeführt werden.

### Kommentare

Kommentare helfen uns beim Verständnis des Codes. Hier können freie Texte eingefügt werden, welche nicht bei der Generierung berücksichtigt werden und als Dokumentation dienen.

Insbesondere bei Code, welcher 

1. durch andere Personen erstellt wurde
2. schon länger nicht geändert/angeschaut wurde

ist dadurch leichter verständlich. Es gibt zwei Formen an Kommentare, welche nachfolgend erläutert werden:

```abap
* Das ist ein Kommentar

    * Das ist kein Kommentar
```

Kommentare, welche mit dem `*` eingeführt werden, beginnen *immer* am Zeilenanfang und erstrecken sich über die gesamte Zeile.

&rarr; Die gesamte Zeile ist ein Kommentar-Feld

Wird das Zeichen `*` nicht am Zeilenanfang gesetzt, so ist das eine fehlerhafte Anweisung, welche von ABAP nicht interpretiert werden kann.

Das `"` leitet einen *Inline*-Kommentar ein und kann an jeder Position einer Zeile gesetzt werden. Bis zum Ende der Zeile ist jedes Wort ein Kommentar und wird nicht weiter berücksichtigt.

```abap
" Das ist ein Kommentar

DATA(wert_1) = 1 + 3. " Das ist ein Kommentar
```

> **Hinweis zur Formatierung**
>
> ABAP-Code wird durch den *Pretty Printer* (kommt noch) eingerückt. Davon sind auch die Kommentare betroffen.
> 
> &rarr; Kommentare, welche mit `*` eingeleitet wurden, werden *nicht* eingerückt.
> 
> &rarr; Kommentare, welche mit `"` eingeleitet wurden, werden eingerückt.

### Schreibweise

Wie auch in anderen Sprachen ist es in `SAP ABAP` notwendig, den Befehl durch ein schließendes Zeichen zu beenden.

In ABAP wird dies mit dem Zeichen `.` (Punkt) gemacht. Durch die Schreibweise mit dem Punkt weiß der Interpreter genau, wann ein Befehl zu Ende ist. Hierdurch ist es möglich, mehrere Befehle in eine Zeile zu schreiben oder einen Befehl über mehrere Zeilen zu strecken.

```abap
" mehrere Befehle in einer Zeile
DATA(wert) = 1 + 2. wert = COND #( WHEN a GT wert THEN a ELSE wert ).

" ein Befehl in mehreren Zeilen
DATA(wert) = COND #( WHEN a GT wert
                     THEN a
                     ELSE wert).
``` 

> **Hinweis zur Lesbarkeit**
>
> Die Lesbarkeit ist *immer* der Kürze vorzuziehen. Nur wenn der Code gelesen werden kann, kann er auch verstanden werden.
>
> &rarr; Ein Befehl pro Zeile!

Befehlsblöcke werden durch einen einleitenden Befehl und einen schließenden Befehl gekennzeichnet, welche jeweils durch einen Punkt abgeschlossen werden.

```abap 
FORM test.
    " Anweisungen
ENDFORM.

IF a = b.
    " Anweisungen
ENDIF.
```

Außnahmen dieser Schreibweise gibt es seit `ABAP 7.40`, welche bei Konstruktor-Ausdrücken eine Klammer als öffnendes und schließendes Element benötigt.

```abap
DATA(wert) = COND #( WHEN a GT b THEN 'a' ELSE 'b' ).
```

Auf diese Elemente wird später eingegangen.

### Literale

Literale sind feststehende Zeichenketten (auch *Strings* genannt) im Code. Zeichenketten können entweder durch Hochkomma (`'`) oder Batcktick (```` ` ````)

```abap
DATA(text_1) = 'Das ist eine Zeichenkette'.
DATA(text_2) = `Das ist eine Zeichenkette`.
```

## SAP ABAP schreiben

SAP ABAP kann an verschiedenen Stellen geschrieben werden. Es wird hierbei zwischen verschiedenen Arten an Code unterschieden.

- **SAP ABAP Reports**: Reports werden oftmals auch Programme bezeichnet. Diese werden im *ABAP Editor* geschrieben, welcher über die Transaktion `SE38` aufgerufen werden kann.
- **SAP ABAP Funktionsbausteine**: Diese werden später erklärt. Funktionsbausteine können in der Transaktion `SE37` geschrieben werden.
- **SAP ABAP Klassen**: Diese werden später erklärt. Klassen können mithilfe der Transaktion `SE24` geschrieben werden.

Alle Arten von Code benötigen einen Namen, welcher frei gewählt werden kann. Der Name unterliegt allerdings den Programmier-Richtlinien und Namenskonventionen, welche unter 

&rarr; Programmier-Richtlinien und Namenskonventionen

verfügbar sind. Hierbei handelt es sich um einen Regelsatz zur Benennung von Programmen und anderen Elementen.

> **Wichtiger Hinweis zu Namen**
>
> SAP unterscheidet zwischen einem SAP-Namensraum und einem Kundennamensraum. 
> Änderungen am SAP-Namensraum sind nur unter strengen Vorraussetzungen möglich. 
> Der Kundennamensraum ist der Namensraum, in welchem der Kunde (in diesem Fall wir) Änderungen durchführen dürfen.
> Erkennbar ist der Kundennamensraum daran, dass **alle** Namen mit `Y` oder `Z` beginnen. Generell beginnen wir mit dem `Z`.

Mithilfe des Objekt-Navigators, welcher über die Transaktion `SE80` aufgerufen werden kann, ist es möglich, alle Arten von Objekten zu bearbeiten. 

### Grund-Funktionen im Editor

|                                          Symbol                                          | Tasten-Kürzel | Bezeichnung | Beschreibung                                                                                                          |
| :--------------------------------------------------------------------------------------: | :------------ | ----------- | --------------------------------------------------------------------------------------------------------------------- |
| ![SYSTEM_SAVE](https://experience.sap.com/files/guidelines/icons_sap/ICONS/S_F_SAVE.GIF) | `Strg` + `S`  | Sichern     | Der Code wird gespeichert. Dies hilft dabei, Datenverlust vorzubeugen. Das Sichern aktiviert jedoch den Code *nicht*. |
| ![SYSTEM_DISPLAY_CHANGE](https://experience.sap.com/files/guidelines/icons_sap/ICONS/S_B_DPCH.GIF)| `Strg` + `F1` | Anzeigen &harr; Ändern | Wird der Code nur angezeigt, kann via dieser Funktion in den Bearbeitungs-Modus gewechselt werden |
| ![SYSTEM_CHECK](https://experience.sap.com/files/guidelines/icons_sap/ICONS/S_B_CHCK.GIF) | `Strg` + `F2` | Prüfen | Diese Funktion prüft den Code auf verschiedene Fehler |
| ![SYSTEM_ACTIVATE](https://experience.sap.com/files/guidelines/icons_sap/ICONS/S_B_ACTI.GIF) | `Strg` + `F3` | Aktivieren | Der geschriebene Code wird aktiviert. Das bedeutet, dass der Code auf Fehler geprüft wird und anschließend in Ausführbaren Code umgewandelt wird. Nur wenn der Code aktiviert wurde, ist der Code auch ausführbar. |
| ![SYSTEM_TEST](https://experience.sap.com/files/guidelines/icons_sap/ICONS/S_B_TEST.GIF) | `F8` | Direkt | Diese Funktion führt den aktivierten Code aus. |

Sollten Fragen zu bestimmen Operatoren im ABAP-Code bestehen, so kann der Cursor auf dem betreffenden Operator gesetzt werden und anschließend die `F1`-Taste gedrückt werden. Daraufhin wird die SAP Dokumentation aufgerufen.