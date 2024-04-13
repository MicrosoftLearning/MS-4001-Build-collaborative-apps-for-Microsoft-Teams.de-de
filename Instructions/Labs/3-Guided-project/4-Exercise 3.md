---
lab:
  title: Erstellen einer Teams-Registerkarte
  module: Exercise 3
---

# Übung 3: Erstellen einer Teams-Registerkarte

## Szenario

Angenommen, das IT-Supportteam möchte eine Teams-Registerkarte erstellen, um Benutzern und Benutzerinnen den Zugriff auf erforderliche Informationen beim Übermitteln von Supporttickets zu erleichtern. Beispielsweise muss das Team die Gebietsschemacodes der Benutzer und Benutzerinnen für Ticketverarbeitung und -berichte anzeigen. Ihre aktuelle Aufgabe besteht darin, diese Registerkarte zu erstellen, um den Gebietsschemacode eines Benutzers oder einer Benutzerin anzuzeigen. Weitere Informationen werden der Registerkarte zu einem späteren Zeitpunkt hinzugefügt.

## Übungsaufgaben

Ihre Aufgabe besteht darin, eine Teams-Registerkarten-App zu erstellen, die das Gebietsschema des Benutzers oder der Benutzerin mithilfe des Teams-Kontexts abruft und auf einer persönlichen Registerkarte anzeigt.

Sie müssen die folgenden Aufgaben ausführen, um die Übung abzuschließen:

1. Erstellen Sie eine Registerkarten-App mit dem Teams-Toolkit für Visual Studio Code.
1. Aktualisieren Sie die App, um das Gebietsschema des Benutzers oder der Benutzerin abzurufen und anzuzeigen.

**Geschätzte Abschlusszeit:** 10 Minuten

## Aufgabe 1: Erstellen einer Registerkarten-App mit dem Teams-Toolkit für Visual Studio Code

1. Öffnen Sie Visual Studio Code.
1. Wählen Sie auf der Seitenleiste das Symbol für **Microsoft Teams** aus, um den Bereich **TEAMS-TOOLKIT** zu öffnen.
1. Wählen Sie unter **Neue App erstellen** und dann **Registerkarte** aus.
1. Wählen Sie in der Liste der verfügbaren Optionen die Registerkarte **Grundlagen** aus.
1. Wählen Sie die Programmiersprache **TypeScript** aus.
1. Wählen Sie unter **Arbeitsbereichsordner** die Option **Standardordner** aus.
1. Geben Sie unter **Anwendungsname** den Namen **UserInfoApp** ein.

Eine Benachrichtigung wird angezeigt, wenn alle Ordner und Dateien erfolgreich erstellt wurden, und eine neue Instanz von Visual Studio Code öffnet den neuen Projektordner.

Im Bereich **EXPLORER** enthält der Ordner *src* den Quellcode für Ihre App. Dateien außerhalb des Ordners *src* sind serverbezogen, z. B. der Bot.

## Aufgabe 2: Aktualisieren der App, um das Gebietsschema des Benutzers oder der Benutzerin abzurufen und anzuzeigen

Jetzt können Sie der Registerkarten-App die gewünschten Funktionen hinzufügen.

1. Navigieren Sie zum Ordner `src` > `views`, und öffnen Sie dann die Datei `hello.html`.
1. Suchen Sie das Element `<div>`, und aktualisieren Sie es so, dass es die folgenden Elemente zwischen den Tags `<div>` und `</div>` enthält:

    ```html
        <h1>Hello, User</h1>
      <span>
        <h2>Review your locale code:</h2>
        <p id="locale"></p>
      </span>
    ```

1. Navigieren Sie zum Ordner `src` > `static` > `scripts`, und öffnen Sie dann die Datei `teamsapp.js`.
1. Ersetzen Sie den Inhalt der Datei  durch den folgenden Code:

    ```typescript
        (function () {
          "use strict";
        
          // Call the initialize API first
          microsoftTeams.app.initialize().then(function () {
            microsoftTeams.app.getContext().then(function (context) {
              if (context?.app?.locale) {
                updateLocale(context.app.locale);
              }
              else{
                updateLocale("unknown");
              }
            });
          });
        
          function updateLocale(locale) {
            if(locale){
              document.getElementById("locale").innerHTML = locale;
            }
          }
        })();
    ```

    Dieser Code verwendet das Objekt **context**, um das Gebietsschema des Benutzers oder der Benutzerin abzurufen, und aktualisiert den HTML-Code, um den Gebietsschemacode anzuzeigen.

## Arbeit überprüfen

Führen Sie Ihre App im Debugmodus aus, um die Funktionalität zu testen.

1. Wählen Sie in Visual Studio Code das Symbol für **Microsoft Teams** aus, um den Bereich **TEAMS-TOOLKIT** zu öffnen.

2. Starten Sie die Ausführung Ihrer App mit dem angefügten Debugger. Verwenden Sie dazu eine der folgenden Methoden:

   - Drücken Sie die Taste F5.
   - Navigieren Sie in Visual Studio Code zum Menü **Ausführen und Debuggen**.  Wählen Sie **Debuggen in Teams** mit der von Ihnen gewünschten Browseroption und dann die Schaltfläche **Debuggen starten** aus.
   - Öffnen Sie im Abschnitt **UMGEBUNG** des Teams-Toolkits den Ordner *local*, und wählen Sie dann den gewünschten Browser aus.

3. Nachdem Visual Studio Code einige Überprüfungen durchgeführt hat, deren Aktionen auf der Registerkarte **Konsole** angezeigt werden, wird ein neues Browserfenster geöffnet. Wählen Sie im Dialogfeld **UserInfoApplocal** die Schaltfläche **Hinzufügen**, um die App in Teams zur Vorschau zu installieren.

Die App kann jetzt auf der Seitenleiste angezeigt werden. Die App ist mit zwei Registerkarten vorkonfiguriert: **Persönliche Registerkarte** und **Info**. Stellen Sie sicher, dass der Gebietsschemacode auf der Registerkarte angezeigt wird.
