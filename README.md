# Scalopedia Registry Specification v1.0 — Konzeptentwurf

## 1. Die Tier-ID (SCA-ID)
Jedes in Scalopedia registrierte Tier erhält eine eindeutige, lebenslange Identifikationsnummer — die SCA-ID. Sie ist unveränderlich, nicht übertragbar und bleibt dem Tier selbst dann erhalten, wenn es den Besitzer wechselt.

Aufbau am Beispiel: SCA-DE-PREG-2026-000001

Das Präfix SCA steht für Scalopedia und kennzeichnet das System eindeutig. Das Länderkürzel DE folgt dem ISO-3166-Standard und gibt das Herkunftsland der Registrierung an — perspektivisch sind weitere Ländercodes wie AT oder CH vorgesehen. Der Artcode PREG wird aus den ersten vier Buchstaben des wissenschaftlichen Artnamens abgeleitet (z. B. Pogona → POGO, Eublepharis macularius → EUBL, Python regius → PREG). Die Jahreszahl entspricht dem Kalenderjahr der Erstzulassung. Die sechsstellige Laufnummer wird pro Präfix-Kombination fortlaufend vergeben und stellt innerhalb eines Jahrgangs und einer Art die Einzigartigkeit sicher.

Die SCA-ID is so gestaltet, dass sie auch ohne digitale Hilfsmittel lesbar und interpretierbar bleibt. Ein Halter, Tierarzt oder Zollbeamter kann allein aus der ID-Struktur das Registrierungsland, die Art und das Registrierungsjahr ablesen.

## 2. Das QR-Code-System
Zu jeder SCA-ID wird automatisch ein QR-Code generiert. Dieser QR-Code kodiert eine URL der Form https://scalopedia.app/verify/{SCA-ID} — also beispielsweise https://scalopedia.app/verify/SCA-DE-PREG-2026-000001.

### Lokale Generierung
Der QR-Code wird vollständig auf dem Gerät des Halters erzeugt, ohne dass dafür eine Internetverbindung erforderlich ist. Er enthält keine sensiblen Daten, sondern ausschließlich die öffentliche Verifikations-URL. Das bedeutet: Selbst wenn Scalopedia temporär nicht erreichbar ist, bleibt das physische Dokument mit dem aufgedruckten QR-Code gültig und lesbar.

### Verifikationsprinzip
Wer den QR-Code scannt — sei es mit der Scalopedia-App oder mit jedem beliebigen Smartphone-Scanner — wird auf die Verifikationsseite weitergeleitet. Dort werden ausschließlich öffentlich freigegebene Informationen angezeigt: der registrierte Name des Tieres, die Art, das Geschlecht, das Registrierungsjahr sowie der aktuelle Verifikationsstatus. Private Daten wie Name und Adresse des Halters bleiben standardmäßig verborgen und werden nur angezeigt, wenn der Halter sein Profil ausdrücklich als öffentlich markiert hat.

### Physischer Ausdruck
Die App ermöglicht den Export eines offiziellen Herkunftsnachweises als PDF. Dieses Dokument enthält den QR-Code, die SCA-ID im Klartext, die Tieridentifikationsdaten sowie optional Abstammungsinformationen. Es ist so gestaltet, dass es als Begleitpapier bei Transport, Verkauf oder tierärztlicher Behandlung genutzt werden kann.

## 3. Der digitale Besitzerwechsel
Der Eigentumsübergang in Scalopedia folgt einem klar strukturierten zweistufigen Prinzip: Anfrage und Bestätigung. Kein Tier kann ohne aktive Zustimmung beider Parteien den Besitzer wechseln.

### Schritt 1 — Initiierung durch den aktuellen Halter
Der bisherige Halter sucht den neuen Halter innerhalb der App (z. B. über dessen Profil oder SCA-ID) und erstellt eine Übergabeanfrage für ein bestimmtes Tier. Diese Anfrage enthält die SCA-ID des Tieres, den Empfänger sowie einen optionalen Freitext für Übergabenotizen.

### Schritt 2 — Benachrichtigung des Empfängers
Der designierte neue Halter erhält eine Echtzeit-Benachrichtigung in der App. Er kann die Anfrage annehmen oder ablehnen. Erst mit seiner ausdrücklichen Bestätigung wird der Vorgang fortgesetzt.

### Schritt 3 — Atomarer Eigentumsübergang
Sobald die Bestätigung erteilt wird, führt das System einen atomaren Datenbankvorgang durch. Das bedeutet: Entweder gelingt der gesamte Übergang vollständig — einschließlich der Aktualisierung des aktuellen Halters, der Erstellung eines Eintrags in der Eigentumshistorie und dem Abschluss der Übergabeanfrage — oder er schlägt als Ganzes fehl, ohne dass ein inkonsistenter Zwischenzustand entsteht. Partielle Übergänge (z. B. Halter geändert, aber Historieneintrag fehlt) sind technisch ausgeschlossen.

### Eigentumshistorie
Jeder Besitzerwechsel wird dauerhaft in der Eigentumshistorie des Tieres gespeichert. Diese Chronologie ist Teil des offiziellen Herkunftsnachweises und kann im PDF-Export abgerufen werden. Sie dokumentiert lückenlos, durch wessen Hände ein Tier gegangen ist — ein zentrales Element für seriöse Züchter und Käufer gleichermaßen.

### Datenschutz beim Transfer
Nur die am Transfer beteiligten Parteien sehen die vollständigen gegenseitigen Kontaktdaten. Dritte sehen lediglich, dass ein Eigentumsübergang stattgefunden hat, nicht jedoch die Identität der Beteiligten.

## 4. Scalopedia Visual Identity Verification (SVIV) — Visueller Fundtier-Abgleich
Für den Fall, dass ein registriertes Tier entflieht, stellt das Protokoll ein bildbasiertes, nicht-invasives Identifikationsverfahren bereit. Da Reptilien (insb. Schlangen anhand ihrer Kopfschuppenstruktur und Echsen anhand von Farb- und Fleckenmustern) individuelle, biometrische Merkmale aufweisen, nutzt das System diese als digitalen Fingerabdruck.

### Ablauf im Verlustfall:
1. **Verlustmeldung:** Der Halter markiert die SCA-ID in der App als "Vermisst". Dadurch werden die hinterlegten Identifikationsfotos des Tieres für das öffentliche Notfall-Suchregister freigegeben.
2. **Fundmeldung & Foto-Upload:** Ein Finder, Tierheim oder eine Behörde kann über eine öffentlich zugängliche Schnittstelle ein Foto des gefundenen Tieres hochladen und die Gattung eingrenzen.
3. **Algorithmischer Abgleich:** Das System gleicht die biometrischen Muster des Fundtier-Fotos mit den in der Region als vermisst gemeldeten Tieren derselben Art ab.
4. **Anonymisierte Kontaktaufnahme:** Bei einem Match wird der Halter automatisch benachrichtigt. Die Privatsphäre des Halters bleibt geschützt; die Kommunikation erfolgt über ein anonymisiertes Relay-System, um das Tier sicher zurückzuführen.

## 5. Scalopedia Emergency Response Protocol (SERP) — Giftnotruf- & Serum-Schnittstelle
Für die Registrierung von potenziell gefährlichen oder giftigen Tieren (Giftschlangen, Skorpione, Spinnen) integriert das Protokoll ein standardisiertes Notfall-Datenblatt, das im Falle eines Unfalls (z. B. Biss- oder Stichverletzung) lebensrettende Sekunden sichert.

### Funktionsweise:
1. **QR-Code-Notfallscan:** Rettungskräfte oder Notärzte können den QR-Code am Terrarium oder den digitalen Herkunftsnachweis scannen. Dieser Scan schaltet im medizinischen Notfallmodus sofort das spezifische Datenblatt frei.
2. **Medizinische Evidenz:** Das Protokoll liefert ohne Verzögerung die exakte wissenschaftliche Bezeichnung des Tieres, die Toxizitätsklasse, das spezifisch benötigte Antivenin (Serum) sowie die Dosierungshinweise.
3. **Logistische Kopplung:** Das System gleicht den Standort des Unfalls mit den Datenbanken der Giftnotrufzentralen und Serum-Depots ab, um den Rettungskräften sofort anzuzeigen, in welcher nächstgelegenen Klinik das passende Antivenin gelagert ist.

## 6. Cryptographic Lineage & Health Verification (CLHV) — Fälschungssichere Ahnenkette
Um dem illegalen Wildtierhandel, dem Verkauf von Schmuggelware und der Fälschung von Herkunftsnachweisen entgegenzuwirken, etabliert das Protokoll eine kryptografisch verknüpfte Ahnen- und Gesundheitschronik. Stammbäume werden im System nicht als statische Dokumente hinterlegt, sondern als dynamische, signierte Datenketten.

### Funktionsweise:
1. **Kryptografische Verknüpfung:** Bei der Registrierung einer Nachzucht müssen die SCA-IDs der Elterntiere angegeben werden. Das System fordert eine digitale Signatur (Bestätigung) der jeweiligen Besitzer der Elterntiere an. Erst nach dieser Verifizierung wird die genetische Linie im Protokoll verankert.
2. **Schutz vor Dokumentenbetrug:** Da die Kette rein digital und über eindeutige IDs läuft, ist es mathematisch unmöglich, fiktive Stammbäume zu erstellen, Wildfänge als Nachzuchten zu deklarieren oder Herkunftspapiere per Bildbearbeitung zu fälschen.
3. **Anonymisierte Vererbungstracking:** Tritt bei einem Tier ein dokumentierter, genetischer Defekt oder eine Erbkrankheit auf, kann dieser Befund (validiert durch verifizierte Fachtierärzte) im System vermerkt werden. Das Protokoll erlaubt es, das Risiko für Erbkrankheiten in den Folgegenerationen algorithmisch zu berechnen, um Qualzuchten effektiv zu verhindern, während die Identität der Halter anonym bleibt.

## Leitgedanke
Die Scalopedia Registry versteht sich nicht als bürokratisches System, sondern als Vertrauensinfrastruktur für eine Community, die verantwortungsvolle Terraristik ernst nimmt. Jede SCA-ID ist ein Versprechen: Dieses Tier existiert, es ist dokumentiert, und seine Geschichte ist nachvollziehbar — für Tierärzte, Behörden, Käufer und die Tiere selbst.
