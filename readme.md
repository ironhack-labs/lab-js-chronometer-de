![logo_ironhack_blue 7](https://user-images.githubusercontent.com/23629340/40541063-a07a0a8a-601a-11e8-91b5-2f13e4e6b441.png)

# LAB | JS IronChronometer

![giphy (1)](https://user-images.githubusercontent.com/76580/167427065-a674fb55-44ea-448a-a7ef-940b45eeb9df.gif)


## Einführung

In diesem Labor werden wir einen [Chronometer](https://www.dictionary.com/browse/chronometer) erstellen. Chronometer werden häufig im Sport wie z.B. Autorennen oder Leichtathletik verwendet. Warum sollten wir also nicht unsere Kenntnisse in JS und der Manipulation von DOM üben und unseren eigenen IronChronometer erstellen? Anschließend können wir ihn verwenden, um zu sehen, wie viele Minuten und Sekunden wir für die Fertigstellung eines beliebigen unserer Labs benötigen werden. Klingt gut, oder?

Los geht's!

Das sind unsere Meilensteine:

1. Unser Chronometer wird ein _LCD-Bildschirm_ haben, auf dem wir sehen werden, wie Minuten und Sekunden vorbeigehen.
2. Es wird auch zwei verschiedene Schaltflächen haben, die je nach Status des Chronometers ihr Verhalten ändern werden. Zum Beispiel wird die Startschaltfläche zu einer Stopp-Schaltfläche, wenn der Chronometer läuft.
3. Als Bonus werden wir eine [Split-Funktion](https://www.google.com/search?q=chronometer+split&oq=chronometer+split) hinzufügen, die es uns ermöglicht, die Zeit aufzuzeichnen, wenn wir die Split-Schaltfläche drücken.

Los geht's!

Um zu überprüfen, wie deine endgültige Version aussehen sollte, schau dir diese **[Demo](https://sandrabosk.github.io/demo-chrono/index.html)** an.

## Anforderungen

- Fork dieses Repo.
- Klone dieses Repo.



## Abgabe

- Führe nach Abschluss die folgenden Befehle aus:

```shell 
$ git add .
$ git commit -m "solve iteration x, y, z"
$ git push origin master  
```   
- Erstelle einen Pull Request, damit deine TAs deine Arbeit überprüfen können.

## Anleitung

Zum Starten haben wir die folgenden Dateien und Ordner zur Verfügung:

``` ├── README.md 
    ├── index.html 
    ├── javascript 
    │   ├── chronometer.js 
    │   └── index.js 
    ├── styles 
    │   ├── fonts 
    │   │   ├── ds-digi.ttf 
    │   └── style.css 
    └── tests    
     └── chronometer.spec.js  
 ```   

Das Stylesheet enthält bereits die Schriftart `ds-digi`. Diese Schriftart hilft uns, einen klassischen LCD-Bildschirm zu haben, um den Stil der traditionellen Chronometer zu erreichen.

Wir haben auch die Uhr erstellt, damit du dich auf den JavaScript-Teil dieser Übung konzentrieren kannst. Klicke unten, um das Bild zu sehen, das angezeigt werden sollte, wenn du die `index.html`-Datei öffnest:

<br>  
<details> 
    <summary>Klicke hier, um das Bild zu sehen</summary> 
    
  <br>   

    ![](https://education-team-2020.s3-eu-west-1.amazonaws.com/web-dev/labs/chronometer.png)

</details>   


**Dieses Lab ist in zwei Hauptteile unterteilt**:

- Teil 1: die Logik (die du der Datei `javascript/chronometer.js` hinzufügen wirst).
- Teil 2: die DOM-Manipulation, damit wir die zuvor geschriebene Logik visuell darstellen und präsentieren können (der Code, den du der `javascript/index.js` hinzufügst).


Deine Lösung erfordert die Verwendung der globalen Methoden `setInterval` und `clearInterval`.

[`setInterval`](https://developer.mozilla.org/en-US/docs/Web/API/setInterval) kann mit einer Funktion als erstes Argument und einer Anzahl von Millisekunden als zweites Argument aufgerufen werden. Es wird die übergebene Funktion alle Millisekunden ausführen, die du ihm übergeben hast.

Beim Aufruf gibt `setInterval` eine Nummer zurück, die verwendet werden kann, um das _Interval_ zu identifizieren, das initialisiert wurde. Das gleiche Interval kann später gestoppt werden, indem man `clearInterval` aufruft und ihm die ID des Intervalls übergibt, das unterbrochen werden soll.


### Iteration 1: Die Logik

Im ersten Teil des LABs wirst du an der Datei `javascript/chronometer.js` arbeiten.

#### Die `Chronometer`-Klasse

Lass uns unsere `Chronometer`-Klasse erstellen. Die Methode `constructor` sollte keine Argumente erwarten. Sie sollte zwei Eigenschaften des Chronometers initialisieren:

-   `currentTime`, das als die Zahl `0` starten sollte.
-   `intervalId`, das als `null` starten sollte.

Lass uns mit der Erstellung der `Chronometer`-Methoden fortfahren.


#### Methode `start`

Die `Chronometer`-Klasse muss eine Methode `start` haben. Wenn sie aufgerufen wird, wird `start` die Zeit verfolgen, indem sie eine Funktion in einem 1-Sekunden-Intervall ausführt, die die Anzahl der in der Eigenschaft `currentTime` gespeicherten Sekunden um `1` erhöht.

Du solltest dich auf die `setInterval`-Methode verlassen, um dies zu erreichen. Die Intervall-ID, die durch den Aufruf von `setInterval` zurückgegeben wird, sollte unserer Eigenschaft `intervalId` zugewiesen werden, damit wir sie später löschen können, wenn wir den Timer anhalten müssen.

Zusätzlich sollte die `start`-Methode eine Funktion als Argument akzeptieren. Nennen wir sie `callback`. Das `callback`-Argument ist optional. Wenn `start` aufgerufen wird und ein `callback` übergeben wird, sollte dieser im Inneren der Funktion, die an `setInterval` übergeben wurde, ausgeführt werden. Wenn kein Callback übergeben wird, sollte er ignoriert werden (Tipp: Du solltest prüfen, ob das `callback` übergeben wurde, bevor du versuchst, es auszuführen).

:bulb: _Hinweis 1_: Beachte, dass, wenn du eine Funktionsdeklaration an die `setInterval()`-Methode übergibst (indem du `setInterval(function () {/* */})` schreibst), das Schlüsselwort `this` nicht auf das Objekt _chronometer_, sondern auf den globalen Scope verweist. Um auf den Chronometer durch den Zugriff auf `this` verweisen zu können, solltest du eine Funktionsausdruck (eine sogenannte Pfeilfunktion) an die `setInterval()`-Methode übergeben (indem du stattdessen `setInterval(() => {/* */})` schreibst).


#### Methode `getMinutes`

Wir speichern die Anzahl der vergangenen Sekunden in der Eigenschaft `currentTime`. Möglicherweise möchten wir jedoch herausfinden, wie viele Minuten vergangen sind.

Die Methode `getMinutes` sollte keine Argumente enthalten und die _Anzahl_ der vergangenen Minuten als Ganzzahl, als ganze Zahl, zurückgeben. Wir könnten die `Math.floor()`-Methode verwenden, um eine gerundete Zahl zu erhalten, indem wir die aktuelle Zeit durch 60 teilen.

#### Methode `getSeconds`

Wir können jetzt die Anzahl der vergangenen Minuten abrufen. Aber was ist, wenn wir die Anzahl der Sekunden abrufen möchten, die nach dem Start der aktuellen Minute vergangen sind?

Die `getSeconds`-Methode sollte die Anzahl der Sekunden zurückgeben, die nach dem Start der aktuellen Minute vergangen sind.

Wenn die Eigenschaft `currentTime` beispielsweise `75` enthält, sollte `getSeconds` `15` zurückgeben. Wenn `currentTime` `210` enthält, sollte `getSeconds` `30` zurückgeben, und so weiter.

Wir könnten den Modulo-Operator (% 60) verwenden, um die endgültige Anzahl der Sekunden zu erhalten.

Hinweis: Der [Rest-Mathematikoperator](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Remainder) kann in dieser Situation äußerst hilfreich sein.


#### Methode `computeTwoDigitNumber`

Unser Chronometer hat einen super coolen Bildschirm, der zwei Stellen benötigt, um Minuten und Sekunden anzuzeigen. Manchmal geben jedoch die Methoden `getMinutes` und `getSeconds` eine einstellige Zahl zurück. Lass uns einen super einfachen Algorithmus erstellen, der jede empfangene Zahl in eine Zahl mit zwei Stellen umwandelt.

Die `computeTwoDigitNumber`-Methode sollte eine Zahl entgegennehmen und eine Zeichenfolge zurückgeben, bei der die als Argument übergebene Zahl mit Nullen aufgefüllt wurde, um sicherzustellen, dass der Wert mindestens 2 Zeichen lang ist (wir könnten die `.slice()`-Methode verwenden, um unser Ziel zu erreichen).

Wenn beispielsweise `computeTwoDigitNumber` mit der Zahl `7` aufgerufen wird, sollte es eine Zeichenfolge mit dem Wert von `"07"` zurückgeben. Wenn es mit der Zahl `36` aufgerufen wird, sollte es eine Zeichenfolge mit dem Wert von `"36"` zurückgeben.

Später werden wir die `computeTwoDigitNumber`-Methode verwenden, um die von `getMinutes` und `getSeconds` zurückgegebenen Werte zu formatieren und sie in unserem Chronometer anzuzeigen.


#### Methode `stop`

Wir können unseren Chronometer bereits starten. Lass uns eine Methode erstellen, die ihn anhält.

Wenn die `stop`-Methode aufgerufen wird, sollte sie das Intervall mit der ID löschen, die in der `intervalId`-Eigenschaft gespeichert wurde. So einfach ist das.

:bulb: _Hinweis_: Verwende `clearInterval`.


#### Methode `reset`

`reset()` wird unseren Chronometer zurücksetzen. Da unser Code super sauber ist, müssen wir nur unsere `currentTime`-Eigenschaft auf 0 zurücksetzen, und das ist alles!

Wir müssen auch die Werte in unserer HTML-Datei zurücksetzen, indem wir `.innerHTML` verwenden.


#### Methode `split`

An bestimmten Stellen möchten wir möglicherweise einen formatierten Zeitstempel für die seit dem Start des Chronometers vergangene Zeit extrahieren. Wir nennen dies "Erhalten der Zwischenzeit".

Die `split`-Methode sollte keine Argumente enthalten und eine Zeichenfolge zurückgeben, in der die Zeit seit dem Start als "_mm:ss_" formatiert ist. Intern kann die `split`-Methode zuvor deklarierte Methoden wie `getMinutes`, `getSeconds` und `computeTwoDigitNumber` verwenden.


### Iteration 2: DOM-Manipulation

Deine Chronometer-Klasse ist jetzt vollständig! Das bedeutet, dass wir jetzt eine visuelle Schnittstelle erstellen können, die es uns ermöglicht, die gesamte Logik zu nutzen, die wir gerade programmiert haben.

Ab diesem Zeitpunkt solltest du im `javascript/index.js`-File arbeiten. Beachte, dass du für den Moment nichts in den HTML- oder CSS-Dateien ändern musst.

In dieser Iteration ist dein Ziel, einen neuen Chronometer zu erstellen und seine Methoden zu verwenden (die wir zuvor in `chronometer.js` definiert haben), während du mit dem DOM interagierst. Zum Beispiel sollte der `Start`-Button bei einem Klick die `start`-Methode des Chronometers aufrufen.

Wie du sehen kannst, haben wir zwei verschiedene Schaltflächen: `Start` und `Clear`. Dies sind die Button-Werte, wenn der Chronometer nicht läuft. Wenn der Chronometer läuft, ändert der Start-Button sein Verhalten, um den Chronometer zu stoppen. Im Gegensatz dazu wird der Reset-Button zu Split wechseln.

Beide Schaltflächen haben ein unterschiedliches Verhalten, abhängig vom Status des Chronometers. Diese Schaltflächen sind `btnLeft` und `btnRight` in unserem HTML. Wir können die unterschiedlichen Werte, die sie haben werden, in der folgenden Tabelle sehen:

| Chronometer Status | Button ID  | Text  | CSS Class   | 
| ------------------ | ---------- | ----- | ----------- |
| Stopped            | `btnLeft`  | START | `btn start` | 
| Stopped            | `btnRight` | RESET | `btn reset` | 
| Running            | `btnLeft`  | STOP  | `btn stop`  | 
| Running            | `btnRight` | SPLIT | `btn split` |

Du findest bereits zwei Click-Event-Listener, die mit beiden `btnLeft`- und `btnRight`-Schaltflächen verknüpft sind. Du musst den notwendigen Code erstellen, um den Status der Schaltflächen zu ändern.

:bulb: _Hinweis_: Um den _Status_ der Schaltflächen zu ändern, müssen wir ihre Klassen abhängig davon _toggle_n, ob ihre Klassen "start" oder "reset" enthalten.

Das bedeutet, dass wenn wir auf `btnLeft` klicken und es die `start`-Klasse hat, du den `btnLeft` und `btnRight` Buttons den im obigen Tabellen beschriebenen Running-Status zuweisen musst.

Wenn `btnLeft` beim Klicken nicht die `start`-Klasse hat, müssen wir beide `btnLeft` und `btnRight` Eigenschaften ändern und sie auf den im obigen Tabellen beschriebenen Stopped-Status setzen.

Wenn `btnLeft` die Klasse `start` hat, sollten wir die `start`-Methode des Chronometers aufrufen - denke daran, die Argumente zu übergeben! -.

#### Ändern der Schaltflächentexte

Wir werden im `javascript/index.js`-File arbeiten. Wir müssen Folgendes tun (wir könnten `.className` und `.innerHTML` verwenden, um dies zu tun):

- Wenn die linke Schaltfläche geklickt wird, während der Chronometer gestoppt ist, müssen wir:

- Die `btnLeft`-Schaltfläche mit dem Text STOP und der Klasse `btn stop` setzen.
- Die `btnRight`-Schaltfläche mit dem Text SPLIT und der Klasse `btn split` setzen.
- Wenn die linke Schaltfläche geklickt wird, während der Chronometer läuft, müssen wir:

- Die `btnLeft`-Schaltfläche mit dem Text START und der Klasse `btn start` setzen.
- Die `btnRight`-Schaltfläche mit dem Text RESET und der Klasse `btn reset` setzen.

- Erstelle im `index.js`-File eine neue Instanz des `Chronometer`-Objekts (das wir bereits zu Beginn des Files haben).

- Erstelle den notwendigen Code in `index.js`, um die `start`-Methode des Chronometers aufzurufen, wenn die Schaltfläche die Klasse `start` hat, oder die `stop`-Methode aufzurufen, wenn die Schaltfläche die Klasse `stop` hat.

#### Anzeigen unseres Chronometers

Jede Sekunde müssen wir unseren Bildschirm aktualisieren. Erstelle also eine Funktion, die den Wert für Minuten und Sekunden empfängt und diese in unserem HTML ausgibt - denke daran, unsere `computeTwoDigitNumber` Methode zu verwenden, die wir im Chronometer haben!

Du kannst die `start` Methode deines Chronometers aufrufen.

Hinweis: Wenn du dich erinnerst, erwartet die `start` Methode einen Rückruf als Argument und führt diesen Rückruf jede Sekunde aus (du kannst als Argument eine Funktion übergeben, um die Benutzeroberfläche zu aktualisieren).

<details>    
 <summary> Klicke hier, um das Bild zu sehen </summary>   

<br />   

![](https://s3-eu-west-1.amazonaws.com/ih-materials/uploads/upload_1a87e0edfb6efea2ae0c77c490e8563b.png)  

</details>   

### Iteration 3: Split Zeit

Die folgende Funktion, die wir implementieren werden, ist die Split-Taste. Denke daran, dass die Split-Taste im `btnRight` Button platziert ist, wenn der Chronometer läuft. In dieser Iteration müssen wir zwei verschiedene Dinge erstellen: HTML & CSS und das zugehörige JavaScript.


#### HTML & CSS

Zunächst müssen wir in unserer `index.html`-Datei eine geordnete Liste finden, an die wir jedes Mal, wenn wir die Split-Taste drücken, die aktuelle Zeit anhängen werden. Diese hat eine id von `splits`, und wir haben es am Anfang unserer index.js-Datei als Ziel definiert.


#### JavaScript


Sobald wir die geordnete Liste in unserem HTML gefunden haben, müssen wir die Button-Funktionalität erstellen. Jedes Mal, wenn wir auf die Split-Taste klicken, müssen wir ein neues `li`-Element erstellen und es der geordneten Liste hinzufügen. Der Text dieses Elements wird die aktuelle Zeit des Chronometers sein (wir haben eine Methode in unserem Chronometer, die dies zurückgibt :wink:).

Daher sollten wir zuerst bei jedem Klick auf den Button ein Listenelement erstellen. Danach sollten wir diesem Listenelement einen Klassennamen hinzufügen ('list-item'). Dann sollten wir den innerHTML mit dem Ergebnis unserer Methode `split`in chronometer aktualisieren. Und schließlich sollten wir es dem übergeordneten Element in der HTML-Datei (der geordneten Liste mit `id`s von '`splits`) hinzufügen.


<details>    
 <summary> Klicke hier, um das Bild zu sehen </summary>   
<br>   

![](https://s3-eu-west-1.amazonaws.com/ih-materials/uploads/upload_a5c9687f25bd710b2e7658ee6d997174.png)

</details>   


### Iteration 4: Reset

Um mit dieser Lektion fertig zu werden, werden wir die _Clear_-Funktion erstellen. Denke daran, dass wir dies ausführen, wenn der Chronometer angehalten ist und der Benutzer auf die rechte Schaltfläche klickt - überprüfe den Ereignislistener am Ende der Datei. Das Verhalten hier ist einfach: Wir müssen alle Daten auf der Uhr löschen.

Um dies zu tun, müssen wir die Minuten und Sekunden auf Null in unserer Uhr setzen und alle `li`-Elemente entfernen, die wir in der vorherigen Iteration erstellt haben.

### BONUS Iteration 5: Millisekunden

Jetzt können wir unseren Chronometer verwenden, um zu berechnen, wie viel Zeit wir für jede Ironhack-Übung benötigen. Was passiert, wenn wir unsere Zeit in einem Rennen berechnen wollen? Wir müssen genauer mit unserem Chronometer sein. Wie können wir genauer sein? Durch Hinzufügen von Millisekunden!

Wenn wir Millisekunden zum Chronometer hinzufügen möchten, müssen wir HTML, CSS und JavaScript manipulieren. Im HTML müssen wir einen Container hinzufügen, um die Millisekunden anzuzeigen, den Stil dieses Containers ändern und den DOM mit dem Dezimal- und Einheitswert der Millisekunden ändern (sie sind am Anfang der index.js-Datei ausgewählt).    
Schließlich müssen wir in JavaScript alle Logik hinzufügen, um die Millisekunden auf der Uhr anzuzeigen. Wir müssen diese Millisekunden auch zum Split-Zähler hinzufügen - wir sollten hier auch die twoDigits-Methode aufrufen.

![](https://s3-eu-west-1.amazonaws.com/ih-materials/uploads/upload_82e9d1fd5976a3f98bb1382f2385f6a1.png)


Dein Ziel ist es, die JavaScript-Logik zu erstellen, um:

- Die Millisekunden zu zählen.
- Die Millisekunden während des Vorwärtszählens anzuzeigen.
- Die Millisekunden anzuzeigen, wenn du eine Split-Zeit aufzeichnest.
- Die Millisekunden zu löschen, wenn die Reset-Taste geklickt wird.

Dieses Labor ist etwas komplex, aber es wird dich durch den logischen Prozess führen, das Problem zu lösen, und gleichzeitig wirst du lernen, wie man zwischen der Logik und der DOM-Manipulation (die visuellen Elemente) trennt.



## Teste Deinen Code

## Tests, tests, tests!

Dieses LAB ist mit Unit-Tests ausgestattet, um automatisiertes Feedback zu Ihrem Lab-Fortschritt zu geben. Du beginnst damit, mit den Tests zu arbeiten und sie zusammen mit den Iterationsanweisungen zu verwenden.

Öffne bitte dein Terminal, wechsle in das Stammverzeichnis des Labs und führe `npm install` aus, um den Testrunner zu installieren. Führe anschließend den Befehl `npm run test:watch` aus, um automatisierte Tests durchzuführen.

```shell 
$ cd lab-javascript-chronometer
$ npm install
$ npm run test:watch  
```   
<br>   

Öffne die resultierende `lab-solution.html` Datei mit der [Live Server](https://marketplace.visualstudio.com/items?itemName=ritwickdey.LiveServer) VSCode Erweiterung, um die Testergebnisse zu sehen.

**Hinweis:** Die Testumgebung und die `lab-solution.html` Seite erlauben es nicht, _console logs_ im Browser auszudrucken.

Um die console.log-Ausgaben zu sehen, die Du in einer der JavaScript-Dateien schreibst, öffne die `index.html` Datei mit der [Live Server](https://marketplace.visualstudio.com/items?itemName=ritwickdey.LiveServer) VSCode Erweiterung.

<br>  

**Viel Spaß beim Coden!** :heart: