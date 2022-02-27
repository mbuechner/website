---
title         : "Migration von E-Mail-Postfächer"
description   : "Wie zieht man am besten seine (IMAP-) Postfächer von einem auf einen anderen Server um?"
cover         : "26_kl.webp"
coverAlt      : "Kuhherde mit Hirte in Thüringen"
toc           : false
tags          : [ admin, e-mail, linux ]
draft         : false
---

## Wie zieht man am besten (IMAP-) Postfächer von einem auf den anderen Server um?

Ich habe viel ausprobiert und bin beim kostenlosen [Imapsync](https://imapsync.lamiral.info/) gelandet. Alle anderen (kostenlosen) Tools haben bei meinen Migrationen leider nicht gut funktoniert, z.B. fehlende E-Mails, Encoding-Probleme.

Nach der [Installation](https://imapsync.lamiral.info/#install), die zugegebenermaßen etwas tricky ist, ist aber die Benutzung des Kommandozeilentools denkbar einfach. Imapsync findet auch Besonderheiten der Mail-Server-Konfigurationen und reagiert entsprechend. Natürlich werden Posteingang, -ausgang, Gesendet und alle weiteren Ordner ordentlich synchronisiert.

```bash
imapsync \
 --host1 127.0.0.1 --user1 mail@example.com --password1 example01 \
 --host2 mail.example.new --user2 mail@example.com --password2 example02
```

...oder noch viel einfacher (und ohne Installation) mit [Docker](https://hub.docker.com/r/gilleslamiral/imapsync/):

```bash
docker run gilleslamiral/imapsync imapsync \
 --host1 127.0.0.1 --user1 mail@example.com --password1 example01 \
 --host2 mail.example.new --user2 mail@example.com --password2 example02
```
