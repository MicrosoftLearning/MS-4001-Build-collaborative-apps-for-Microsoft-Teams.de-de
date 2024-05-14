---
lab:
  title: Erstellen eines Bots
  module: Exercise 4
---

# Übung 4: Erstellen eines Bots

## Szenario

Angenommen, das von Ihnen unterstützte IT-Supportteam erhält eine große Anzahl häufiger, sich wiederholender Abfragen von Mitarbeitern in der gesamten Organisation. Diese Abfragen betreffen häufig einfache Probleme wie Kennwortzurücksetzungen, Softwareinstallationsanweisungen oder die Problembehandlung häufiger Fehler.

Um den Prozess zu optimieren und die Arbeitsauslastung Ihres Teams zu reduzieren, entscheiden Sie sich für die Erstellung eines Bots, der diese allgemeinen Abfragen in Microsoft Teams verarbeiten kann.

Sie entscheiden sich dazu, dem Bot einen ersten Befehl mit dem Namen „resetPassword“ hinzuzufügen. Wenn ein Benutzer oder eine Benutzerin diesen Befehl eingibt, antwortet der Bot mit schrittweisen Anleitungen zum Zurücksetzen des Kennworts. Auf diese Weise können Benutzer bzw. Benutzerinnen ihr Problem lösen, ohne sich direkt an das IT-Supportteam wenden zu müssen. So hat Ihr Team mehr Zeit für die Behandlung komplexerer Probleme.

Zusätzlich zum Befehl „resetPassword“ möchten Sie weitere Befehle hinzufügen, um andere allgemeine Abfragen zu verarbeiten. Dadurch wird der Bot zu einem umfassenden Self-Service-Tool für die Beschäftigten in der Organisation.

## Übungsaufgaben

Um die Übung abzuschließen, müssen Sie die folgenden Aufgaben erledigen:

1. Erstellen des Bots mithilfe des Teams-Toolkits
2. Konfigurieren des App-Manifests
3. Erstellen einer adaptiven Karte
4. Verarbeiten des Befehls

**Geschätzte Abschlusszeit:** 17 Minuten

## Aufgabe 1: Erstellen eines Bots mithilfe des Teams-Toolkits

Verwenden Sie die ‚Vorlage für den Befehls-Bot, um einen neuen Bot zu erstellen:

1. Öffnen Sie Visual Studio Code.
1. Wählen Sie auf der Seitenleiste das Symbol für **Microsoft Teams** aus, um den Bereich **TEAMS-TOOLKIT** zu öffnen.
1. Klicken Sie auf die Schaltfläche **Neue App erstellen**.
1. Wählen Sie im Menü **Neues Projekt** die Option **Bot** und dann **Chatbefehl** aus, um einen Befehls-Bot zu erstellen.
1. Wählen Sie für die Programmiersprache **TypeScript** aus.
1. Wählen Sie unter **Arbeitsbereichsordner** einen Ordner aus, oder erstellen Sie einen, um Ihre Projektdateien auf dem Computer zu speichern.
1. Geben Sie unter **Anwendungsname** den Namen **SupportCommandBot** ein, und drücken Sie die **EINGABETASTE**. Das Teams-Toolkit erstellt ein Gerüst für eine neue App und öffnet den Projektordner in Visual Studio Code.
1. Möglicherweise erhalten Sie eine Nachricht von Visual Studio Code, die sie fragt, ob Sie den Autoren der Dateien in diesem Ordner vertrauen. Wählen Sie die Schaltfläche **Ja, ich vertraue den Autoren** aus, um fortzufahren.
1. Überprüfen Sie die Projektverzeichnisse und Dateien im Explorer in Visual Studio Code, um sich mit dem Quellcode vertraut zu machen.

## Aufgabe 2: Konfigurieren des Manifests

Definieren Sie einen `ResetPassword`-Befehl im App-Manifest:

1. Öffnen Sie die Datei `manifest.json` im Ordner `appPackage`.
2. Suchen Sie im `bots`-Objekt nach `commandLists`.  Derzeit ist ein einzelner Befehl mit dem Titel `helloWorld` vorhanden.
3. Ersetzen Sie `commands` wie folgt durch den folgenden Code, sodass er einen neuen `ResetPassword`-Befehl enthält:

    ```typescript
            "commands": [
                {
                    "title": "helloWorld",
                    "description": "A helloworld command to send a welcome message"
                },
                {
                    "title": "resetPassword",
                    "description": "Request instructions to reset your password"
                }
            ]
    ```

## Aufgabe 3: Erstellen einer adaptiven Karte

Erstellen Sie eine adaptive Karte, die als Reaktion auf den `ResetPassword`-Befehl gesendet werden soll:

1. Erstellen Sie in `src`/`adaptiveCards` eine neue Datei mit dem Namen `resetPassword.json`.
2. Fügen Sie der Datei folgenden Inhalt hinzu, und speichern Sie sie:

   ```json
        {
            "type": "AdaptiveCard",
            "body": [
                {
                    "type": "TextBlock",
                    "size": "Medium",
                    "weight": "Bolder",
                    "text": "Reset Password Instructions"
                },
                {
                    "type": "TextBlock",
                    "text": "1. Navigate to the login page and select 'Forgot Password'.",
                    "wrap": true
                },
                {
                    "type": "TextBlock",
                    "text": "2. Enter your email or username and select 'Submit'.",
                    "wrap": true
                },
                {
                    "type": "TextBlock",
                    "text": "3. Check your email for a password reset link and select it.",
                    "wrap": true
                },
                {
                    "type": "TextBlock",
                    "text": "4. Enter and confirm your new password, then select 'Save'.",
                    "wrap": true
                },
                {
                    "type": "TextBlock",
                    "text": "5. Log in with your new password.",
                    "wrap": true
                }
            ],
            "actions": [
                {
                    "type": "Action.OpenUrl",
                    "title": "Go to Login Page",
                    "url": "https://www.adaptivecards.io/designer/"
                }
            ],
            "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
            "version": "1.4"
        }
   ```

## Aufgabe 4: Verarbeiten des Befehls

Verarbeiten Sie als Nächstes den Befehl im Quellcode des Bots mithilfe der `TeamsFxBotCommandHandler`-Klasse.  Importieren Sie das `resetPasswordCard`-Element aus der JSON-Datei, und rendern Sie es beim Aufrufen des Befehls:

1. Erstellen Sie im Ordner `src` eine neue Datei namens `resetPasswordCommandHandler.ts`.
2. Fügen Sie der Datei die folgenden Importanweisungen hinzu, einschließlich einer Anweisung zum Importieren der unformatierten `resetPassword`-Karte, die Sie erstellt haben:

   ```typescript
   import { Activity, CardFactory, MessageFactory, TurnContext } from "botbuilder";
    import { CommandMessage, TeamsFxBotCommandHandler, TriggerPatterns } from "@microsoft/teamsfx";
    import { AdaptiveCards } from "@microsoft/adaptivecards-tools";
    import rawResetPasswordCard from "./adaptiveCards/resetPassword.json";
   ```

3. Fügen Sie unter den Importanweisungen den folgenden Code hinzu, um den Befehlshandler zu implementieren, und speichern Sie dann die Datei:

   ```typescript
       export class ResetPasswordCommandHandler implements TeamsFxBotCommandHandler {
          triggerPatterns: TriggerPatterns = "resetPassword";
        
          async handleCommandReceived(
            context: TurnContext,
            message: CommandMessage
          ): Promise<string | Partial<Activity> | void> {
            console.log(`App received message: ${message.text}`);
        
            const resetPasswordCard = AdaptiveCards.declareWithoutData(rawResetPasswordCard).render();
            await context.sendActivity({ attachments: [CardFactory.adaptiveCard(resetPasswordCard)] });
          }
        }
   ```

## Aufgabe 5: Registrieren des neuen Befehls

Jeder neue Befehl muss in `ConversationBot`konfiguriert werden, wodurch der Unterhaltungsfluss der Befehlsbotvorlage unterstützt wird.

1. Navigieren Sie zur Datei `src/internal/initialize.ts`.
2. Fügen Sie in Zeile 2 die folgende import-Anweisung hinzu:

    `import { ResetPasswordCommandHandler } from "../resetPasswordCommandHandler";`
3. Fügen Sie in Zeile 20 dem `commands`-Array der `command`-Eigenschaft eine Anweisung zum Initialisieren des neuen Handlers hinzu. `new ResetPasswordCommandHandler()`  Das aktualisierte `command`-Objekt sollte wie folgt aussehen:

   ```json
   command: {    enabled: true,    commands: [new HelloWorldCommandHandler(), new ResetPasswordCommandHandler()],  },
    ```

## Aufgabe 6: Wechseln vom Entwicklertunnel zu ngrok (optional)

Wenn Ihre Entwicklungsumgebung den Entwicklungstunnel des Teams-Toolkits nicht unterstützt, können Sie den Entwicklertunnel durch ngrok ersetzen.

1. Führen Sie die folgenden Schritte aus, um ngrok zu installieren:
   1. Wechseln Sie zur [ngrok-Website](https://ngrok.com/) und registrieren Sie sich für ein Konto.
   1. Laden Sie die ausführbare Datei „ngrok“ für Ihr Betriebssystem herunter.
   1. Extrahieren Sie die heruntergeladene Datei in ein Verzeichnis Ihrer Wahl.
   1. Fügen Sie für die Windows-Umgebung das Verzeichnis hinzu, in dem sich `ngrok.exe` befindet, die PATH-Umgebungsvariable des Systems. 
      ```powershell
      setx PATH "$Env:path;<ngrok_full_path>"
      ```
      _Ersetzen Sie `<ngrok_full_path>` in der PowerShell-Umgebung mit dem `ngrok.exe` lokalisierten Pfad._
      > Um diese Umgebungsvariablenänderung anzuwenden, müssen Sie Terminals und **Visual Studio Code** für das aktuelle Projekt neu starten.

   1. Öffnen Sie ein Terminal oder eine Eingabeaufforderung, und führen Sie den folgenden Befehl aus, um Ihr ngrok-Konto zu authentifizieren:
      ```shell
      ngrok config add-authtoken <your_auth_token>
      ```
      _Ersetzen Sie `<your_auth_token>` mit dem auf der ngrok-Website bereitgestellten Authentifizierungstoken._
   1. Führen Sie den folgenden Befehl aus, um einen Tunnel auf Port 3978 zu starten:
      ```shell
      ngrok http 3978
      ```
   1. Ngrok generiert eine Weiterleitungs-URL, mit der Sie über das Internet auf Ihre App zugreifen können.
      ```shell
      Forwarding      http://<random_string>.ngrok-free.app -> http://localhost:3978
      ```
   1. Klicken Sie, `Ctrl + C` um den ngrok-Tunnel zu trennen.
1. Navigieren Sie zum Ordner `.vscode`, und öffnen Sie dann die Datei `task.json`. Aktualisieren Sie Aufgabe `Start local tunnel`:
   ```json
    {
        "label": "Start local tunnel",
        "type": "shell",
        "command": "ngrok http 3978 --log=stdout --log-format=logfmt",
        "isBackground": true,
        "problemMatcher": {
            "pattern": [
                {
                    "regexp": "^.*$",
                    "file": 0,
                    "location": 1,
                    "message": 2
                }
            ],
            "background": {
                "activeOnStart": true,
                "beginsPattern": "starting web service",
                "endsPattern": "started tunnel|failed to reconnect session"
            }
        }
    }
   ```
1. Navigieren Sie zu der `teamsapp.local.yml`-Datei im Stammordner. Fügen Sie die folgende Aktion im ersten Schritt des Bereitstellungslebenszyklus hinzu
   - Windows
     ```yml
     provision:
       - uses: script
         with:
           shell: powershell
           run: |
                for ($i = 1; $i -le 10; $i++) {
                    $endpoint = (Invoke-WebRequest -Uri "http://localhost:4040/api/tunnels" | Select-String -Pattern 'https://[a-zA-Z0-9 -\.]*\.ngrok-free\.app').Matches.Value
                    if ($endpoint) {
                        break
                    }
                    sleep 10
                }
                if (-not $endpoint) {
                    echo "ERROR: Failed to find tunnel endpoint after 10 attempts."
                    exit 1
                } else {
                    echo "::set-teamsfx-env BOT_ENDPOINT=$endpoint"
                    echo "::set-teamsfx-env BOT_DOMAIN=$($endpoint.Substring(8))"
                }
     ```
   - Linux und macOS
     ```yml
     provision:
        - uses: script
            with:
            run: |
                for i in {1..10}; do
                    endpoint=$(curl -s localhost:4040/api/tunnels | grep -o 'https://[a-zA-Z0-9 -\.]*\.ngrok-free\.app')
                    if [ -n "$endpoint" ]; then
                        break
                    fi
                    sleep 10
                done
                if [ -z "$endpoint" ]; then
                    echo "ERROR: Failed to find tunnel endpoint after 10 attempts."
                    exit 1
                else
                    echo "::set-teamsfx-env BOT_ENDPOINT=$endpoint"
                    echo "::set-teamsfx-env BOT_DOMAIN=${endpoint:8}"
                fi
     ```
## Arbeit überprüfen

Führen Sie Ihre App lokal aus, um die Funktionalität zu testen:

1. Öffnen Sie das **TEAMS TOOLKIT**-Pannel. Wählen Sie im Menü **LEBENSZYKLUS** die Option **Vorschau Ihrer Teams-App** aus (oder verwenden Sie die Taste `F5`), und wählen Sie dann in Ihrem bevorzugten Browser **In Teams debuggen ()** aus.  
2. Das Teams-Toolkit stellt Ihre App bereit und führt sie lokal in einem Browser aus.
3. Wählen Sie im Browser im Dialogfeld für die App-Installation **Hinzufügen** aus, um Ihre Teams-App zu installieren.  Teams öffnet eine Unterhaltung mit Ihrem installierten Bot.
4. Geben Sie den Befehl `resetPassword` ein, oder wählen Sie ihn aus.
5. Stellen Sie sicher, dass der Bot mit einer adaptiven Karte antwortet, die Anweisungen zur Kennwortzurücksetzung enthält.
