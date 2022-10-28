---
title           : "Asymmetrische Kryptographie am Beispiel des RSA-Kryptosystems"
description     : "Dieser Blogpost beschäftigt sich mit dem Kryptosystem RSA. Nach einer kurzen Einführung wird ein Praxisbeispiel angeführt, um die Bedeutung asymmetrischer Verschlüsselungsverfahren zu verdeutlichen."
cover           : "102_kl.webp"
coverAlt        : "Kuhherde mit Hirte in Thüringen"
toc             : false
tags            : [ kryptographie, verschlüsselung, mathematik ]
draft           : false
katex           : true
katexExtensions : [ mhchem, copy-tex ]

---

## 1 Einleitung
Das RSA-Kryptosystem ist ein asymmetrisches Verschlüsselungsverfahren. Es wurde 1978 von R. Rivest, A. Shamir und L. Adleman unter dem Titel „A Methode for Obtaining Digital Signatures and Public Key Cryprosystems“ (Communications of the ACM, Nr. 21, Seite 120-126) vorgestellt.

Die Sicherheit des RSA-Kryptosystems beruht auf der bekannten Schwierigkeit der Zerlegung großer Ganzzahlen in Primfaktoren. Bisher sind hierzu keine effizienten Algorithmen bekannt. Alle publizierten Algorithmen haben eine exponentielle Laufzeit. Die „Pollard-p-1-Methode“ ist, mit einer Komplexität von $\mathcal{O}(\sqrt[3]{N}$), das derzeit schnellste Verfahren zur Primfaktorzerlegung.

### 1.1 Asymmetische Verschlüsselung
Das Ziel der asymmetrischen Verschlüsselung ist der sichere Informationsaustausch zwischen Teilnehmern in einem öffentlichen Netzwerk, bei dem die zu transportierenden (verschlüsselten) Daten abgehört werden können. Als Grundlage der asymmetrische Verschlüsselung werden zwei, zueinander passende aber verschiedene Schlüssel verwendet.

Mit dem öffentlichen Schlüssel werden Daten verschlüsselt, die Entschlüsselung ist ausschließlich mit dem privaten Schlüssel möglich. Außerdem kann eine Signierung und Verifikation von Daten durchgeführt werden.

### 1.2 Praxisbeispiel
Alice möchte eine Nachricht verschlüsselt an Bob senden. Dazu benötigt sie den öffentlichen Schlüssel von Bob. Diesen hat sie aus einer vertrauenswürdigen Quelle (persönlich, aus dem „Web-of-Trust“ oder auch von seiner Webseite) erhalten und sie kann sicher sein, dass dieser korrekt ist (ein Schlüssel kann Authentifizierungsmerkmale aufweisen, z. B. Bild des Besitzers).

{{< img "verschluesselung.webp" "Ver-/Entschlüsselung bei asymmetrischen Verfahren" noborder >}}

Alice schickt die mit dem öffentlich Schlüssel verschlüsselte Daten an Bob. Dort angekommen kann dieser die verschlüsselten Daten wieder entschlüsseln. Die verschlüsselte Nachricht kann von niemanden außer Bob mit seinem privaten Schlüssel entschlüsselt werden. Um den Diebstahl eines privaten Schlüssels zu erschweren ist dieser zudem mit einem Passwort geschützt.

{{< img "signierung.webp" "Signierung/Verifikation bei asymmetrischen Verfahren" noborder >}}

Alice kann Daten für Bob auch signieren, d. h. digital unterschreiben. Dazu wird ein Prüfwert der Nachricht mit dem privaten Schlüssel von Alice erstellt. Bob kann dann mit dem öffentlichen Schlüssel von Alice nachprüfen, ob die Daten tatsächlich von Alice stammen oder ob diese modifiziert wurden.

## 2. Grundlagen
Zur Durchführung von Ver- und Entschlüsselung mit dem RSA-Kryptosystem sind einige wenige mathematische Grundlagen notwendig, die in diesem Abschnitt kurz vorgestellt werden sollen.

### 2.1 Modulo-Operation

Teilt man eine Zahl $m$ durch eine andere Zahl $n$, so bleibt neben dem ganzzahligen Ergebnis $q$ ein Rest $r$. Die ganzzahlige Division wird, zur Unterscheidung von der normalen Division, als $div$ geschrieben und die Operation zur Bestimmung des Restes wird *Modulo-Operation* $mod$ genannt.

$$ 
\begin{align*}
    q & = m\ \textrm{div}\ n\newline
    r & = m\ \textrm{mod}\ n\newline
    m & = q\cdot n+r\newline
      & = (m\ \textrm{div}\ n)\cdot n+(m\ \textrm{mod}\ n)
\end{align*}
$$

#### Beispiel

$$
\begin{align*}
    5 & = 17\ \textrm{div}\ 3\newline
    2 & = 17\ \textrm{mod}\ 3\newline
   17 & = 5\cdot3+2\newline
      & = (17\ \textrm{div}\ 3)\cdot3+(17\ \textrm{mod}\ 3)
\end{align*}
$$

### 2.2 Modulo-Inverse

Die *Kongruenz* ist eine Beziehung zwischen zwei Ganzzahlen. Man nennt zwei Zahlen $a$, $b$ kongruent (Symbol $\equiv$) bezüglich einer weiteren Zahl m, wenn sie bei Division durch den Modulo denselben Rest haben.

$$
\begin{align*}
    a & \equiv b\ \textrm{mod}\ m\newline
    a\ mod\ m & = b\ \textrm{mod}\ m
\end{align*}
$$

Die *Modulo-multiplikativ-Inverse* einer Ganzzahl $a$ ist eine Ganzzahl $x$ für die folgende Bedingung erfüllt ist:

$$
\begin{align*}
    a^{-1} & \equiv x\ \textrm{mod}\ m\newline
    ax\equiv aa^{-1} & \equiv 1\ \textrm{mod}\ m
\end{align*}
$$

Der *Euklidische Algorithmus* ist ein Verfahren, um den größten gemeinsamen Teiler zweier positiver Ganzzahlen zu berechnen. Sind $a$ und $m$ zwei teilerfremde positive ganze Zahlen, so kann die erweiterte Version des Algorithmus verwendet werden, um die Inverse von $a\ \textrm{mod}\ m$, also die positive Zahl $x<m$ die die Gleichung $ax\ \textrm{mod}\ m=1$ erfüllt, zu berechnen.

#### Beispiel

Der Erweiterte Euklidische Algorithmus sei an dem folgenden Beispiel erläutert, bei dem die Inverse von 5 modulo 48 berechnet werden soll. Zunächst wird der Euklidische Algorithmus angewandt, mit dem der größte gemeinsame Teiler, hier $\textrm{ggT}(\color{red}5\color{none},\color{cyan}48\color{none})=\color{magenta}1$, ermittelt werden kann.

$$
\begin{align*}
    \color{cyan}48\color{none} & = 9\cdot\color{red}5\color{none}+\color{green}3\newline
    \color{red}5\color{none} & = 1\cdot\color{green}3\color{none}+\color{blue}2\newline
    \color{green}3\color{none} & = 1\cdot\color{blue}2\color{none}+\color{magenta}1
\end{align*}
$$

In einem weiteren Schritt wird nach den ermittelten Resten $\color{magenta}1\color{none}, \color{blue}2\color{none}, \color{green}3\color{none}$ umgestellt und diese nacheinander, mit der untersten Zeile beginnend, eingesetzt.

$$
\begin{align*}
  \color{magenta}1\color{none} & = \color{green}3\color{none}-1\cdot\color{blue}2\color{none}\newline
  \color{magenta}1\color{none} & = \color{green}3\color{none}-1\cdot(\color{red}5\color{none}-1\cdot\color{green}3\color{none})=2\cdot\color{green}3\color{none}-1\cdot\color{red}5\color{none}\newline
  \color{magenta}1\color{none} & = 2\cdot(\color{cyan}48\color{none}-9\cdot\color{red}5\color{none})-1\cdot\color{red}5\color{none}=2\cdot\color{cyan}48\color{none}-19\cdot\color{red}5
\end{align*}
$$

Damit wurde gezeigt, dass $\color{magenta}1\color{none}=2\cdot\color{cyan}48\color{none}-19\cdot\color{red}5$ und somit gilt:

$$
-19\cdot\color{red}5\color{none}\  \textrm{mod}\ \color{cyan}48\color{none}=\color{magenta}1
$$

Da die Inverse positiv und kleiner als 48 sein soll, wird auf der linken Seite der Gleichung noch $(\color{cyan}48\color{none}\cdot\color{red}5\color{none})$ addiert, das Ergebnis lautet somit:

$$
\begin{align*}
	(-19\cdot\color{red}5\color{none})+(\color{cyan}48\color{none}\cdot\color{red}5\color{none})\  \textrm{mod}\ \color{cyan}48\color{none} & = \color{magenta}1\newline
	29\cdot\color{red}5\color{none}\  \textrm{mod}\ \color{cyan}48\color{none} & = \color{magenta}1\newline
	\color{red}5\color{none}^{-1}\  \textrm{mod}\ \color{cyan}48\color{none} & = 29
\end{align*}
$$

### 2.3 Primzahlen

Primzahlen sind natürliche Zahlen, die größer als eins und ausschließlich durch sich selbst und eins teilbar sind. Es gibt keine Formel mit der Primzahlen berechnet werden können. Zur Ermittlung einer Primzahl wird eine zufällige Zahl in der gewünschten Größenordnung gewählt und mit einem *Primzahltest* (z. B. Miller-Rabin-Test, Agarwal-Saxena-Kayal-Test) überprüft, ob es sich um eine Primzahl handelt. 

Der *Primzahlsatz* $\pi(n)$ für eine beliebige reelle Zahl $n$ ist eine Approximation mittels Logarithmus für die Anzahl von Primzahlen $p$ für die gilt $p\leq n$. 

$$
\pi(n)=\frac{n}{\ln(n)}
$$

Für den Primzahlsatz existieren auch stärkere Formen die bessere Approximationen liefern (z. B. Legendres Formel, Integrallogarithmus). Außerdem zeigt der Primzahlsatz, dass nicht viele Primzahltests durchgeführt werden müssen, um eine Primzahl zu finden.

#### Beispiel

Wie viele Primzahlen mit 512 Bit gibt es?

$$
\pi(2^{512})-\pi(2^{511})=\frac{2^{512}}{\ln(2^{512})}-\frac{2^{511}}{\ln(2^{511})}\thickapprox2^{502}
$$


Wie wahrscheinlich ist es, dass eine zufällig ausgewählte Zahl eine Primzahl ist?

$$
\frac{2^{502}}{2^{512}-2^{511}}=2^{-9}=\frac{1}{512}
$$

Wenn man vorher die geraden Zahlen ausschließt, so verbessert sich die Wahrscheinlichkeit auf $2^{-8}=\frac{1}{256}$. Im Mittel kann also nach rund 250 Versuchen eine Primzahl mit einer Größe von 512 Bit gefunden werden.

## 2.4 Euler'sche φ-Funktion

Die Euler'sche φ-Funktion gibt für jede natürliche Zahl $m$ an, wie viele zu $m$ teilerfremde positive ganze Zahlen es gibt, die nicht größer als $m$ sind. Mit anderen Worten: Wie viele Zahlen von eins bis $m$ gibt es, bei denen der größte gemeinsame Teiler (ggT) gleich eins ist?

$$
\varphi(m)=|\lbrace a\in\mathbb{N}\ |\ 1\leq a\leq m\ \wedge\ \textrm{ggT}(a,m)=1 \rbrace|
$$

Da im Zusammenhang mit dem RSA-Kryptosystem Primzahlen verwendet werden und diese nur durch eins und sich selbst teilbar sind, so sind die Zahlen $1$ bis $(p-1)$ teilerfremd. Die Bestimmung der Euler'sche φ-Funktion bei Primzahlen ist daher trivial.

$$
\begin{equation*}
    \varphi(p) = p-1
\end{equation*}
$$

Der Vollständigkeit halber sei noch die allgemeine Berechnungsformel angegeben, aus der sich für jede Zahl $m$ die φ-Funktion aus ihrer kanonischen Primfaktorzerlegung berechnen lässt. 

$$
\varphi(m)=m\underset{p|n}{\prod}\left(1-\frac{1}{p}\right)
$$

## 2.5 Satz von Fermat-Euler

Die Euler'sche φ-Funktion findet im Satz von Fermat-Euler eine ihre wichtigsten Anwendungen. Der Satz sagt aus, dass für zwei ganze, positive und teilerfremde Zahlen $m$ und $n$, $m$ ein Teiler von $(n^{\varphi(m)}-1)$ ist.

$$
\textrm{ggT}(m,n)=1\Rightarrow m^{\varphi(n)}\equiv1\ \textrm{mod}\ n
$$

Der Spezialfall des *Kleinen-Fermat-Satzes* tritt ein, wenn $n$ durch $m$ nicht ganzzahlig geteilt werden kann. Dies trifft immer zu wenn $n$ eine Primzahl und $m>1$ ist.

$$
n\nmid m\Rightarrow m^{n-1}\equiv1\ \textrm{mod}\ n
$$

## 3. Funktionsweise

### 3.1 Generierung des privaten und öffentlichen Schlüssels

#### 3.1.1 Wähle zwei verschiedene Primzahlen p und q

Wie bereits gezeigt wurde können ausreichend Primzahlen in nicht allzuvielen Wiederholungen generiert werden (siehe Abschnitt Primzahlen). Bei der Wahl der Primzahlen sollte folgendes beachtet werden, da andernfalls bekannte Faktorisierungsalgorithmen (z. B. Pollard-p-1-Methode, Fermat-Faktorisierung, Quadratisches Sieb, Zahlkörpersieb) zu effizient arbeiten könnten:

- Die großen Primzahlen $p$ und $q$ sollen sich nicht zu stark unterscheiden (Zahlkörpersieb),
- die Primzahlen sollten jedoch auch nicht zu nah beieinander liegen (Fermat-Faktorisierung) und 
- $(p+1)$ und $(p-1)$ sollten möglichst wenig kleine Primteiler haben (Pollard-Rho-Algorithmus).

Für besonders starke Verschlüsselung empfehlen sich Primzahlen bei denen $\frac{(p-1)}{2}$ und $\frac{(q-1)}{2}$ auch Primzahlen sind (sog. *starke Primzahlen*).

#### 3.1.2 Berechne n

Das Produkt aus $p$ und $q$ ist Teil des öffentlichen Schlüssels.

$$
n=p\cdot q
$$


#### 3.1.3 Berechne Euler'sche φ-Funktion

Die Berechnung der Euler'sche φ-Funktion ist trivial (vgl. Abschnitt Euler'sche φ-Funktion).

$$
\varphi(p\cdot q)=(p-1)(q-1)
$$

#### 3.1.4 Bestimmung einer Zahl e

Wähle eine natürliche Zahl $e$ zwischen 1 und $\varphi(pq)$ bei der der größte gemeinsame Teiler (ggT) mit $\varphi(pq)$ , eins ist.

$$
1<e<\varphi,\ e\in\mathbb{N}
$$

$$
\textrm{ggT}(e,\varphi)=1
$$


#### 3.1.5 Bestimmung einer Zahl d

Wähle eine natürliche Zahl $d$ zwischen 1 und $\varphi(pq)$ bei der das Produkt aus $d\cdot e$ kongruent zu $1\ \textrm{mod}\ \varphi(pq)$ (vgl. Abschnitt Modulo-Inverse).

$$
1<d<\varphi,\ d\in\mathbb{N}
$$

$$
d\cdot e\equiv1\ \textrm{mod}\ \varphi
$$

#### 3.1.6 Öffentlicher Schlüssel (e, n)

Der öffentliche Schlüssel setzt sich aus den beiden Zahlen $e$ und $n$ zusammen.

#### 3.1.7 Privater Schlüssel (d, n)

Der private Schlüssel setzt sich aus der Zahl $d$ und einem Teil des öffentlichen Schlüssels (Zahl $n$) zusammen.

### 3.2 Ver- und Entschlüsselung

#### 3.2.1 Verschlüsselung

Eine Nachricht $m$ muss als natürliche Zahl kodiert werden, wobei $0<m<n$ gilt. Die Verschlüsselung erfolgt mit dem öffentlichen Schlüssel $(e, n)$:

$$
c=m^{e}\ \textrm{mod}\ n
$$

#### 3.2.2 Entschlüsselung

Die Entschlüsselung der verschlüsselten Nachricht $c$ erfolgt mit dem privaten Schlüssel $(d ,n)$ und kann nur vom Empfänger bzw. vom Ersteller des Schlüsselpaares durchgeführt werden.

$$
\begin{align*}
    c^{d} & \equiv m\ \textrm{mod}\ n\newline
    m & = c^{d}\ \textrm{mod}\ n
\end{align*}
$$

### 3.3 Signierung und Verifizierung

Bei der Generierung und Überprüfung einer RSA-Verifizierung geht man analog zur Ver- und Entschlüsselung vor. Eine Signierung entspricht dabei der Entschlüsselung und wird mit dem privaten Schlüssel durchgeführt. Die Verifizierung kann von jedem mit dem öffentlichem Schlüssel durchgeführt werden, entspricht also der Verschlüsselung.

Tatsächlich wird in der Signatur der gesamte Text verschlüsselt abgelegt. Folglich entstehen sehr große Signaturen. Durch zuvor festgelegt Konventionen kann die Signatur verkleinert werden. Diese Festlegungen müssen natürlich zum Zeitpunkt der Verifizierung bekannt sein.

## 3.4 Zufallszahlen

Mit dem RSA-Kryptosystem kann auch ein Pseudozufallszahlengenerator implementiert werden. Dazu wählt man zwei Primzahlen $p$ und q, so dass das Produkt $n=p\cdot q$ schwer zu faktorisieren ist. Zudem muss ein Startwert $x_{0}$ gewählt werden, der teilerfremd zu $n$ ist. Folgewerte berechnet man wie folgt:

$$
x_{x+1}=x_{i}^{e}\ \textrm{mod}\ n
$$

Die Ausgabe des Generators ist jeweils das letzte Bit von $x_{i}$. Insofern $n$ nicht faktorisiert werden kann, so ist die Vorhersage des jeweils nächsten Bits nicht möglich (andernfalls wäre die Ratewahrscheinlichkeit besser als $\frac{1}{2}$, dies ist, mathematisch beweisbar, nicht der Fall). Der Nachteil dieser Methode ist ihre Ineffizienz.

### 3.5 Beispiel

#### 3.5.1 Erzeugung des Schlüsselpaars

**Primzahlen:** $p=61$ und $q=53$

**Bereche n:** $n=p\cdot q=61\cdot53=\underline{3233}$

**Berechne φ:** $\varphi(p\cdot q)=(p-1)(q-1)=(61-1)(53-1)=3120$

**Bestimme e:** Die Bestimmung von $e$ erfolgt zufällig im Bereich von 1 bis $\varphi(p\cdot q)$. Die Überprüfung, ob $\textrm{ggT}(e,3120)=1$ erfüllt ist kann mit dem Euklidischen Algorithmus (siehe Abschnitt Modulo Inverse) erfolgen.

$$
\begin{align*}
    \textrm{ggT}(17,3120) & \overset{?}{=} 1\newline
                                 3120 & = 183\cdot17+9\newline
                                   17 & = 1\cdot9+8\newline
                                    9 & = 1\cdot8+\underline{1}\newline
                \textrm{ggT}(17,3120) & = 1
\end{align*}
$$

**Berechne d**

$$
\begin{align*}
    e\cdot d & \equiv & 1\ \textrm{mod}\ \text{φ}(p\cdot q)\newline
    17\cdot d & \equiv & 1\ \textrm{mod}\ 3120
\end{align*}
$$

Die Berechnung der Modular-Inversen $d$ kann mit dem Erweiterten Euklidischen Algorithmus (siehe ebenso Abschnitt Modulo-Inverse) erfolgen.

$$
\begin{align*}
    1 & = 9-1\cdot8\newline
    1 & = 9-1\cdot(7-1\cdot9)=2\cdot9-1\cdot7\newline
    1 & = 2\cdot(3120-183\cdot17)-1\cdot7=2\cdot3120-367\cdot17
\end{align*}
$$

Es gilt somit:

$$
\begin{align*}
    (-367\cdot17)+(3120\cdot17)\ \textrm{mod}\ 3120 & = 1\newline
                    2753\cdot17\ \textrm{mod}\ 3120 & = 1\newline
                                                  d & = \underline{2753}
\end{align*}
$$

**Privater Schlüssel:** $(d,n)=(2753,3233)$

**Öffentlicher Schlüssel:** $(e,n)=(17,3233)$

#### 3.5.2 Verschlüsselung von 1234 mit öffentlichem Schlüssel

$$
c=m^{e}\ \textrm{mod}\ n=1234{}^{17}\ \textrm{mod}\ 3233=\underline{2183}
$$


#### 3.5.3 Entschlüsselung von 2183 mit privatem Schlüssel

$$
m=c^{d}\ \textrm{mod}\ n=2183^{2753}\ \textrm{mod}\ 3233=\underline{1234}
$$


#### 3.5.4 Signierung von 1234 mit privatem Schlüssel

$$
s=m^{d}\ \textrm{mod}\ n=1234^{2753}\ \textrm{mod}\ 3233=\underline{1512}
$$


#### 3.5.5 Verifizierung von 1234 mit Signatur 1512 und öffentlichem Schlüssel

Die Nachricht $m=1234$ soll mit der Signatur $s=1512$ und dem öffentlichem Schlüssel verifiziert werden:

$$
\begin{align*}
       m & \overset{?}{=} s^{e}\ \textrm{mod}\ n\newline
    1234 & \overset{?}{=} 1512^{17}\ \textrm{mod}\ 3233\newline
                1234 & = 1234
\end{align*}
$$

#### 3.5.6 Pseudozufallszahlengenerator

Der Startwert wird wie folgt festgelegt: $x_{0}=d=2753$

$$
\begin{align*}
                    x_{x+1} & = x_{i}^{e}\ \textrm{mod}\ n\newline
                        x_1 & = 2753^{17}\ \textrm{mod}\ 3233=1492=(10111010100)_2\newline
 (10111010100)_2\wedge(1)_2 & = \underline{0}\newline
                        x_2 & = 1492^{17}\ \textrm{mod}\ 3233=2783=(101011011111)_2\newline
(101011011111)_2\wedge(1)_2 & = \underline{1}\newline
                        x_3 & = 2783^{17}\ \textrm{mod}\ 3233=2721=(101010100001)_2\newline
(101010100001)_2\wedge(1)_2 & = \underline{1}\newline
                        x_4 & = \ldots
\end{align*}
$$

