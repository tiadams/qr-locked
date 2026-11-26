# qr-locked

Statische, clientseitig verschlüsselte Seite für GitHub Pages.

`index.html` enthält **keinen Klartext**: nur PBKDF2-Parameter, Salz, IV und einen
AES-256-GCM-Ciphertext. Die Entschlüsselung passiert im Browser über die Web Crypto API,
das Passwort wird nie übertragen.

- KDF: PBKDF2-HMAC-SHA256, 600.000 Iterationen
- Cipher: AES-256-GCM
- Ohne Passwort ist der Inhalt nicht rekonstruierbar (öffentlich lesbar ist nur der Ciphertext)

Diese Variante ersetzt keinen serverseitigen Zugriffsschutz: GitHub Pages kann das auf
normalen Plänen nicht. Sie schützt den Inhalt kryptographisch, nicht den Server.
