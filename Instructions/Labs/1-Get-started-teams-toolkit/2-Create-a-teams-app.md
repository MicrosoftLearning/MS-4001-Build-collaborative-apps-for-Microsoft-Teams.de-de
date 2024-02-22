# Übung 2: Erstellen einer Teams-App aus einem Beispiel im Katalog

Das Teams-Toolkit für Visual Studio Code bietet eine Sammlung von Beispielen, die Sie erkunden und aus denen Sie Ihre Basis-App erstellen können. In dieser Übung erstellen Sie Ihre erste Microsoft Teams-App aus dem Beispielkatalog.

Führen Sie eine der folgenden Aufgaben aus, um eine Teams-App aus einem Beispiel zu erstellen oder eine neue Teams-App mittels dem Teams-Toolkit zu erstellen.

## Aufgabe 1: Erstellen einer App aus einer Vorlage

1. Wählen Sie in der Visual Studio Code-Randleiste die Schaltfläche **Teams-Toolkit** aus, um das Teams-Toolkit zu öffnen.

2. Wählen Sie im Teams-Toolkit für Visual Studio Code **Beispiele anzeigen** aus, um einen Katalog mit Beispiel-Apps anzuzeigen.

   ![Screenshot der Option zum Anzeigen von Beispielen.](../../media/view-samples.png)

3. Suchen Sie ein Beispiel, das Sie interessiert, und wählen Sie den Screenshot aus, um die Seite für dieses Beispiel zu öffnen.  Um schnell starten zu können, wählen Sie ein Beispiel aus, bei dem auf der Detailseite des Beispiels unter dem Titel angegeben ist, dass es bereit zum Debuggen ist.  (Bei anderen Beispielen ist angegeben, dass manuelle Konfigurationen erforderlich sind.)

4. Wählen Sie auf der Beispielseite **Erstellen** aus, und wählen Sie einen Ordner zum Speichern Ihres Projekts aus. Das Gerüst für dieses Projekt wird in diesem lokalen Ordner erstellt.

    ![Screenshot zum Erstellen einer App aus einem Beispiel.](../../media/create-sample.png)

5. Wenn der Gerüstbau abgeschlossen ist, wird ein neues Visual Studio Code-Fenster mit dem geladenen Projekt für den Hallo Welt-Bot angezeigt.  Nachdem das Gerüst für das Projekt erstellt wurde, erhalten Sie möglicherweise eine Visual Studio Code-Meldung mit der Frage, ob Sie den Autoren der Dateien in diesem Ordner vertrauen. Wählen Sie die Schaltfläche **Ja, ich vertraue den Autoren** aus, um fortzufahren.

    ![Screenshot des Dialogfelds mit der Frage, ob Sie den Autoren vertrauen.](../../media/trust-authors.png)

6. Jetzt können Sie den Projektcode anzeigen, der Folgendes umfasst:

- Den Code für die Teams-App.
- Bereitstellungs- und Manifestdateien im Ordner „appPackage“.
- Umgebungsvariablen im Ordner „env“.
- Eine README-Datei, die die erforderlichen Schritte zum Ausführen, Debuggen und Bereitstellen der App enthält.

    ![Screenshot einer App, für die ein Gerüst erstellt wurde.](../../media/bot-project-code.png)

## Aufgabe 2: Erstellen einer neuen Teams-App

Sie können eine neue Teams-App auch mit dem Teams-Toolkit erstellen.

1. Wählen Sie im Teams-Toolkit die Option **Neue App erstellen** aus.
2. Wählen Sie im Menü „Neues Projekt“ die Option** **Nachrichtenerweiterung** aus.
3. Wenn Sie aufgefordert werden, eine Funktion auszuwählen, wählen Sie **benutzerdefinierte Suchergebnisse** aus.
4. Wenn Sie aufgefordert werden, eine Option auszuwählen, wählen Sie **Mit einem Bot beginnen** aus.
5. Wenn Sie aufgefordert werden, eine Programmiersprache auszuwählen, wählen Sie **TypeScript** aus.
6. Wenn Sie aufgefordert werden, einen Ordner auszuwählen, wählen Sie **Standardordner** aus, oder wählen Sie einen anderen Dateispeicherort aus.
7. **Geben Sie einen Anwendungsnamen** Ihrer Wahl für Ihre Nachrichtenerweiterungsapp ein, und wählen Sie **eingeben**.
8. Das Teams-Toolkit erstellt ein Gerüst für eine neue App und öffnet den Projektordner in Visual Studio Code.
9. Möglicherweise erhalten Sie eine Nachricht von Visual Studio Code, die sie fragt, ob Sie den Autoren der Dateien in diesem Ordner vertrauen. Wählen Sie die Schaltfläche **Ja, ich vertraue den Autoren** aus, um fortzufahren.
10. Jetzt können Sie den Projektcode anzeigen, der Folgendes umfasst:

- Den Code für die Teams-App.
- Bereitstellungs- und Manifestdateien im Ordner „appPackage“.
- Umgebungsvariablen im Ordner „env“.
- Eine README-Datei, die die erforderlichen Schritte zum Ausführen, Debuggen und Bereitstellen der App enthält.
