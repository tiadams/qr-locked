# qr-locked

Statische, token-geschützte Seite für GitHub Pages.

`index.html` enthält **keinen Klartext**: nur HKDF-Parameter, Salz, IV und einen
AES-256-GCM-Ciphertext. Der Zugangsschlüssel steckt im URL-Fragment (`#k=…`), das
der Browser nie an den Server überträgt. Ohne Token bleibt der Inhalt unlesbar.

- Token: 256 Bit Zufall (base64url, 43 Zeichen) – liegt nur im QR-Code
- KDF: HKDF-SHA256 (Salt + Info-Kontext)
- Cipher: AES-256-GCM (authentifiziert)
- Entschlüsselung: ausschließlich clientseitig über die Web Crypto API

Die Seite hat **kein Eingabefeld**: ohne gültigen Schlüssel im Fragment zeigt sie nur
einen Hinweis. Der QR-Link trägt eine Build-Version im Query (`?v=N`), weil GitHub Pages
`max-age=600` ausliefert und sonst bis zu 10 Minuten die alte Seite aus dem Cache kommt.

Inhalt ist derzeit ein CV. Der Klartext bleibt lokal; hier liegt nur der Ciphertext.
Druckvorlagen (Einzelcode + A4-Bogen mit 9 Codes) entstehen außerhalb des Repos.

## Grenzen

- Der QR-Code **ist** die Capability: wer ihn fotografiert, hat Zugang.
- Kein serverseitiger Schutz – GitHub Pages kann das auf normalen Plänen nicht.
- Entzug nur durch Rotation des Tokens (neu bauen, neu pushen, neue QR-Codes).
- Einmal-Links brauchen einen Server; statisch ist das nicht möglich.
