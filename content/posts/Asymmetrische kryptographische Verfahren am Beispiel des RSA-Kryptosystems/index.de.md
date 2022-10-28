---
title           : "Asymmetrische kryptographische Verfahren am Beispiel des RSA-Kryptosystems"
description     : ""
cover           : "102_kl.webp"
coverAlt        : "Kuhherde mit Hirte in Thüringen"
toc             : false
tags            : [ kryptographie, verschlüsselung, mathematik ]
draft           : true
katex           : true
katexExtensions : [ mhchem, copy-tex ]

---

# Asymmetrische kryptographische Verfahren am Beispiel des RSA-Kryptosystems

## 1 Einleitung
Das RSA-Kryptosystem ist ein asymmetrisches Verschlüsselungsverfahren. Es wurde 1978 von R. Rivest, A. Shamir und L. Adleman unter dem Titel „A Methode for Obtaining Digital Signatures and Public Key Cryprosystems“ (Communications of the ACM, Nr. 21, Seite 120-126) vorgestellt.

Die Sicherheit des RSA-Kryptosystems beruht auf der bekannten Schwierigkeit der Zerlegung großer Ganzzahlen in Primfaktoren. Bisher sind hierzu keine effizienten Algorithmen bekannt. Alle publizierten Algorithmen haben eine exponentielle Laufzeit. Die „Pollard-p-1-Methode“ ist, mit einer Komplexität von $\mathcal{O}(\sqrt[3]{N}$), das derzeit schnellste Verfahren zur Primfaktorzerlegung.

### 1.1 Asymmetische Verschlüsselung
Das Ziel der asymmetrischen Verschlüsselung ist der sichere Informationsaustausch zwischen Teilnehmern in einem öffentlichen Netzwerk, bei dem die zu transportierenden (verschlüsselten) Daten abgehört werden können. Als Grundlage der asymmetrische Verschlüsselung werden zwei, zueinander passende aber verschiedene Schlüssel verwendet. Mit dem öffentlichen Schlüssel werden Daten verschlüsselt, die Entschlüsselung ist ausschließlich mit dem privaten Schlüssel möglich. Außerdem kann eine Signierung und Verifikation von Daten durchgeführt werden.
  
Teilt man eine Zahl $m$ durch eine andere Zahl $n$, so bleibt neben dem ganzzahligen Ergebnis $q$ ein Rest $r$. Die ganzzahlige Division wird, zur Unterscheidung von der normalen Division, als \noun{div} geschrieben und die Operation zur Bestimmung des Restes wird \emph{Modulo-Operation} \noun{(mod)} genannt.

### 1.2 Praxisbeispiel
Alice möchte eine Nachricht verschlüsselt an Bob senden. Dazu benötigt sie den öffentlichen Schlüssel von Bob. Diesen hat sie aus einer vertrauenswürdigen Quelle (persönlich, aus dem „Web-of-Trust“ oder auch von seiner Webseite) erhalten und sie kann sicher sein, dass dieser korrekt ist (ein Schlüssel kann Authentifizierungsmerkmale aufweisen, z. B. Bild des Besitzers).

{{< img "verschluesselung.webp" "Ver-/Entschlüsselung bei asymmetrischen Verfahren" noborder >}}

Alice schickt die mit dem öffentlich Schlüssel verschlüsselte Daten an Bob. Dort angekommen kann dieser die verschlüsselten Daten wieder entschlüsseln. Die verschlüsselte Nachricht kann von niemanden außer Bob mit seinem privaten Schlüssel entschlüsselt werden. Um den Diebstahl eines privaten Schlüssels zu erschweren ist dieser zudem mit einem Passwort geschützt.

{{< img "signierung.webp" "Signierung/Verifikation bei asymmetrischen Verfahren" noborder >}}

## 2. Grundlagen
Zur Durchführung von Ver- und Entschlüsselung mit dem RSA-Kryptosystem sind einige wenige mathematische Grundlagen notwendig, die in diesem Abschnitt kurz vorgestellt werden sollen.

### 2.1 Modulo-Operation

Teilt man eine Zahl $m$ durch eine andere Zahl $n$, so bleibt neben dem ganzzahligen Ergebnis $q$ ein Rest $r$. Die ganzzahlige Division wird, zur Unterscheidung von der normalen Division, als \noun{div} geschrieben und die Operation zur Bestimmung des Restes wird \emph{Modulo-Operation} \noun{(mod)} genannt.


$$ 
\begin{align*}
    q & = m\ \textrm{div}\ n\newline
    r & = m\ \textrm{mod}\ n\newline
    m & = q\cdot n+r\newline
      & = (m\ \textrm{div}\ n)\cdot n+(m\ \textrm{mod}\ n)
\end{align*}
$$


Der Erweiterte Euklidische Algorithmus sei an dem folgenden Beispiel erläutert, bei dem die Inverse von 5 modulo 48 berechnet werden soll. Zunächst wird der Euklidische Algorithmus angewandt, mit dem der größte gemeinsame Teiler, hier $\textrm{ggT}(\color{red}5\color{none},\color{cyan}48\color{none})=\color{magenta}1$, ermittelt werden kann.

$$
\begin{align*}
    \color{cyan}48\color{none} & = 9\cdot\color{red}5\color{none}+\color{green}3\newline
    \color{red}5\color{none} & = 1\cdot\color{green}3\color{none}+\color{blue}2\newline
    \color{green}3\color{none} & = 1\cdot\color{blue}2\color{none}+\color{magenta}1
\end{align*}
$$
