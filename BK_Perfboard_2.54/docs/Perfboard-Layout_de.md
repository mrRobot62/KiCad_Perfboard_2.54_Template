# Perfboard-Layout

## Zweck

Dieses Dokument beschreibt die Verwendung des KiCad-Templates
`BK_Perfboard_2.54` für die Planung und Dokumentation von Schaltungen
auf 2,54-mm-Lochrasterplatinen.

Das Template ist ein Werkzeug zur Planung. Es schreibt keine bestimmte
Verdrahtungs- oder Löttechnik vor.

## Grundprinzip

Die reale Lochrasterplatine wird in KiCad durch ein virtuelles
2,54-mm-Lochraster dargestellt. Die elektrischen Verbindungen werden mit
mehreren Kupferlagen modelliert, um Verdrahtung auf beiden
Platinenseiten sowie Drahtbrücken eindeutig darstellen und durch den DRC
prüfen zu können.

## Layer-Konzept

  KiCad-Layer   Bezeichnung     Verwendung
  ------------- --------------- -----------------------------------------
  B.Cu          Bottom Wire     Bevorzugte Verdrahtung auf der Lötseite
  F.Cu          Top Wire        Verdrahtung auf der Bauteilseite
  In1.Cu        Top Jumper      Drahtbrücken auf der Bauteilseite
  In2.Cu        Bottom Jumper   Drahtbrücken auf der Lötseite

`B.Cu` ist der bevorzugte und im Template voreingestellte Arbeitslayer.

Die zusätzlichen Layer dienen der logischen Darstellung in KiCad. Sie
stellen keine physisch mehrlagige Lochrasterplatine dar.

## Raster

Das Standardraster beträgt 2,54 mm und entspricht dem üblichen
Lochraster.

Feinere Hilfsraster können bei Bedarf verwendet werden, insbesondere:

-   1,27 mm
-   0,635 mm

Bauteile und Lötpunkte sollten grundsätzlich am realen
2,54-mm-Lochraster ausgerichtet werden.

## Virtuelles Lochraster

Das Lochraster auf `User.Drawings` dient ausschließlich als visuelle
Orientierung.

Es ist kein elektrisches Element und besitzt keine Verbindung zu den
Netzen des Schaltplans.

Die Darstellung ist bewusst dezent gehalten, damit Leiterbahnen, Jumper,
Footprints und Netze deutlich erkennbar bleiben.

## Platinenumriss

Das Template verwendet einen rasterkonformen Standard-Platinenumriss von
ungefähr 120 x 80 mm.

Der tatsächliche Umriss beträgt:

`121,92 x 81,28 mm`

Die `Edge.Cuts` verlaufen durch Rasterpunkte. Dadurch kann der Anwender
den Platinenumriss einfach in ganzen 2,54-mm-Rasterschritten verändern.

Vom Platinenrand geschnittene Rasterpunkte gelten nicht als nutzbare
Lötpunkte.

## BK_Perf_SolderPoint

`BK_Perf_SolderPoint` kennzeichnet einen bewusst gesetzten elektrischen
Löt-, Knoten- oder Übergabepunkt.

Typische Anwendungen sind:

-   Übergang zwischen Verdrahtungs- und Jumper-Layern
-   definierter Anschluss einer Drahtbrücke
-   Verzweigung eines Netzes
-   T-Knoten für mehrere Verbindungen desselben Netzes

Mehrere Verbindungen desselben Netzes können an einem gemeinsamen
SolderPoint zusammengeführt werden. Unmittelbar benachbarte SolderPoints
sollten vermieden werden, wenn ein einzelner gemeinsamer Knoten
denselben Zweck erfüllt.

SolderPoints sollten nur dort eingesetzt werden, wo sie für die geplante
physische Verdrahtung sinnvoll sind.

## Layerwechsel

Ein Layerwechsel repräsentiert eine Änderung der physischen
Verdrahtungsart oder Platinenseite.

Für einen bewusst ausgeführten Übergang kann ein `BK_Perf_SolderPoint`
verwendet werden.

Der Anwender sollte dabei berücksichtigen, wie die Verbindung später
tatsächlich gelötet wird.

## Verdrahtung auf der Bauteilseite

Verdrahtung auf der Bauteilseite ist grundsätzlich möglich, kann jedoch
mechanisch eingeschränkt sein.

Insbesondere bei:

-   DIL-Fassungen
-   Mikrocontroller-Boards
-   Steckmodulen
-   großen Kondensatoren
-   dicht stehenden Bauteilen

kann ein direkter Drahtanschluss am Bauteilpin schwierig oder unmöglich
sein.

Das Template verhindert solche Verbindungen nicht. Die Beurteilung der
praktischen Lötbarkeit liegt beim Anwender.

## Routing-Empfehlungen

Für übersichtliche Lochrasterlayouts haben sich folgende Grundsätze
bewährt:

1.  `B.Cu` bevorzugt für die normale Verdrahtung verwenden.
2.  Leitungen möglichst rasterorientiert und nachvollziehbar führen.
3.  Jumper gezielt einsetzen, wenn Kreuzungen nicht sinnvoll vermieden
    werden können.
4.  SolderPoints nur für reale Löt-, Übergabe- oder Verzweigungspunkte
    verwenden.
5.  Mehrere Verbindungen desselben Netzes möglichst an einem gemeinsamen
    Knoten zusammenführen.
6.  Eine etwas längere, gut nachvollziehbare Verbindung kann bei
    Lochraster sinnvoller sein als eine kurze, schwer lötbare
    Verbindung.
7.  Versorgung und GND möglichst klar und robust führen.

Diese Punkte sind Empfehlungen und keine zwingenden Designregeln.

## ERC und unbenutzte Pins

Absichtlich unbenutzte Symbolpins sollten im Schaltplan mit einem
`No Connect`-Marker gekennzeichnet werden.

Dadurch wird dokumentiert, dass der Pin bewusst offen bleibt, und der
ERC kann zwischen einem absichtlich unbeschalteten und einem
versehentlich vergessenen Anschluss unterscheiden.

Vor dem PCB-Layout sollte der ERC möglichst ohne Fehler und Warnungen
abgeschlossen werden.

## DRC

Der DRC dient auch bei der Perfboard-Planung zur Prüfung der
modellierten elektrischen Verbindungen.

Zielzustand eines fertig geplanten Layouts:

-   0 Errors
-   0 Warnings
-   0 Unconnected Items

DRC-Freiheit bestätigt die Konsistenz des KiCad-Modells. Sie ersetzt
nicht die Prüfung, ob die geplante Verdrahtung auf einer realen
Lochrasterplatine mechanisch und löttechnisch sinnvoll umgesetzt werden
kann.

## Empfohlener Workflow

1.  Schaltplan erstellen.
2.  ERC durchführen und Fehler beseitigen.
3.  Footprints zuweisen.
4.  PCB aus dem Schaltplan aktualisieren.
5.  Bauteile auf dem 2,54-mm-Raster platzieren.
6.  Verdrahtung bevorzugt auf `B.Cu` planen.
7.  Bei Bedarf Jumper und SolderPoints einsetzen.
8.  Routing auf praktische Lötbarkeit prüfen.
9.  DRC durchführen.
10. Layout vor dem realen Aufbau nochmals mit der tatsächlichen
    Lochrasterplatine und den verwendeten Bauteilen vergleichen.

## Hinweis

Das Template bildet die geplante Lochrasterverdrahtung in KiCad ab. Es
kann nicht feststellen, ob eine Verbindung mit den tatsächlich
verwendeten Bauteilen, Drähten und Löttechniken mechanisch erreichbar
oder sinnvoll herstellbar ist.

Diese Entscheidung bleibt Bestandteil der praktischen Aufbauplanung.
