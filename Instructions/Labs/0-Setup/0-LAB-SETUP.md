# Lab-Einrichtung

Führen Sie die folgenden Aufgaben aus, um Ihre Entwicklungsumgebung vor dem Durchführen der Labs vorzubereiten.

## Voraussetzungen des Labs

Sie benötigen die folgenden Tools, um die Labs für diesen Kurs abzuschließen:

- Administratorzugriff auf einen Microsoft 365-Mandanten.
- Ein Azure-Abonnement.
- Visual Studio Code.
- Teams-Toolkit-Erweiterung für Visual Studio Code:  Version 5.2.0 oder höher. (Sie werden dies während dem Lab installieren)
- Der Microsoft Teams-Client (für Arbeit oder Schule) oder der Zugriff auf Microsoft Teams über einen Webbrowser.
- Node.js Version 16.14.2.

## Installieren von nvm-windows

Sie werden dieses Tool verwenden, um Node.js zu installieren und optional bei Bedarf Knotenversionen für Ihre Projekte zu wechseln.

1. Navigieren Sie hierzu in einem Webbrowser zu [https://github.com/coreybutler/nvm-windows/releases](https://github.com/coreybutler/nvm-windows/releases).
2. Suchen Sie die neueste Releaseversion, und wählen Sie die **nvm-setup.zip**-Datei zum Herunterladen aus.  Die Datei wird auf Ihren Computer heruntergeladen werden.
3. Öffnen Sie den Dateiordner, und **extrahieren** Sie den Inhalt des ZIP-Ordners in einen Ordner auf Ihrem Computer.
4. Wählen Sie im neuen Ordner **nvm-setup.exe** aus, um die Setupdatei zu öffnen.
5. Folgen Sie den Anweisungen im Installationsprogramm, um das Tool mithilfe der Standardoptionen zu installieren.
6. Nvm für Windows wird auf Ihrem Computer installiert werden.

## Installieren von Node.js

Installieren Sie Node.js Version 16.14.2, die mit allen Lösungen in diesem Kurs kompatibel ist.

1. Öffnen Sie die Anwendung **Eingabeaufforderung**.
2. Geben Sie den Befehl `nvm install 16.14.2` ein, um Node.js zu installieren.
3. Die nvm-Ausgabe sollte bestätigen, dass die Installation abgeschlossen ist.
4. Führen Sie den Befehl `nvm use 16.14.2` aus, um diese Version von Node.js zu verwenden.
5. Führen Sie den Befehl `node -v` aus, um zu bestätigen, dass Sie Version 16.14.2 installiert haben.

Sie haben jetzt Node.js Version 16.14.2 installiert und konfiguriert

## Azure-Abonnement

Beachten Sie, dass, wenn Sie Azure-Anmeldeinformationen erhalten haben, bereits eine Ressourcengruppe für Ihre Verwendung erstellt wurde.  Wählen Sie für die Bereitstellungsaufgaben in den Labs bei der Aufforderung „Wählen Sie eine Ressourcengruppe aus, oder erstellen Sie eine neue“, **die bereitgestellte Ressourcengruppe aus**.

## Debuggen von Teams-Apps

Beim lokalen Debuggen Ihrer Teams-App werden Sie möglicherweise aufgefordert, ein Entwicklungszertifikat für Localhost zu installieren.  Sie müssen dies tun, um lokal zu debuggen.

Wählen Sie **Installieren** aus, wenn Sie dazu aufgefordert werden.

![Screenshot der Eingabeaufforderung zum Installieren des Entwicklerzertifikats.](../../media/install-certificate.png)

Wählen Sie dann im Dialogfeld „Sicherheitswarnung“ die Option **Ja** aus.

![Screenshot des Dialogfelds „Sicherheit“.](../../media/development-certificate.png)

Besuchen Sie die Teams-Dokumentation, um mehr zu erfahren: [Lokales Debuggen Ihrer Teams-App](https://learn.microsoft.com/microsoftteams/platform/toolkit/debug-local?tabs=Windows&pivots=visual-studio-code-v5)
