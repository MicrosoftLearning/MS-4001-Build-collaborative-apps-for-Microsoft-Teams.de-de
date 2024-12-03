---
lab:
  title: Erstellen eines Bots mit KI
  module: Exercise 4
---

# Übung 4: Erstellen eines Bots mit KI

## Szenario

Stellen Sie sich vor, Sie sind Mitglied des IT-Supportteams. Sie wissen, dass das Erstellen des wöchentlichen Berichts ein sehr mechanischer und zeitaufwendiger Prozess ist. Sie möchten einen KI-Bot in MS Teams erstellen. Indem Sie einfach die wöchentlichen Arbeitsaufgaben und Tasks für die kommende Woche mit dem Bot in einer Unterhaltung besprechen, kann er einen gut formatierten wöchentlichen Bericht erstellen. Dies könnte die Arbeitseffizienz erheblich verbessern.

## Übungsaufgaben

Um die Übung abzuschließen, müssen Sie die folgenden Aufgaben erledigen:

1. Erstellen eines Bots mithilfe der Teams-KI-Bibliothek
1. Herstellen einer Verbindung mit dem OpenAI Service
1. Implementieren von Codefunktionen
1. Aktualisieren von Prompts

**Geschätzte Bearbeitungszeit:** 20 Minuten

## Voraussetzungen

Um die KI-Chat-Bot-Vorlage auf Ihrem lokalen Entwicklungscomputer auszuführen, müssen Sie nicht nur die in der vorherigen Übung erwähnten Ressourcenanforderungen erfüllen, sondern benötigen auch ein OpenAI-Konto. Dieses Konto kann entweder von [OpenAI](https://platform.openai.com/) oder [Azure OpenAI](https://aka.ms/oai/access) sein.

## Aufgabe 1: Erstellen eines Bots mithilfe der Teams-KI-Bibliothek

**Ziel:** Richten Sie ein neues Bot-Projekt mithilfe der Teams KI-Bibliothek ein und machen Sie sich mit der Projektstruktur und den Dateien vertraut.  

Verwenden Sie die KI-Chat-Bot-Vorlage, um einen neuen Bot zu erstellen:

1. Öffnen Sie Visual Studio Code.
1. Wählen Sie auf der Seitenleiste das Symbol für **Microsoft Teams** aus, um den Bereich **TEAMS-TOOLKIT** zu öffnen.
1. Wählen Sie die Schaltfläche **Neue App erstellen** aus.
1. Wählen Sie im Menü **Neues Projekt** die Option **Benutzerdefinierter Copilot** und dann **Einfacher KI-Chatbot** aus, um einen Befehls-Bot zu erstellen.
1. Wählen Sie für die Programmiersprache **TypeScript** aus.
1. Wählen Sie für **Service für großes Sprachmodell (Large Language Model, LLMs)** basierend auf Ihrem LLM-Konto entweder **Azure OpenAI** oder **OpenAI** aus.
1. Drücken Sie die **EINGABETASTE** , um die Einstellung „Großes Sprachmodell (Large Language Model, LLMs)“ zunächst zu überspringen. Der OpenAI-Schlüssel wird im nächsten Schritt eingerichtet.
1. Wählen Sie unter **Arbeitsbereichsordner** einen Ordner aus, oder erstellen Sie einen, um Ihre Projektdateien auf dem Computer zu speichern.
1. Geben Sie für **Anwendungsname** **WeeklyReportChatBot** ein und drücken Sie dann die **EINGABETASTE**. Das Teams-Toolkit erstellt ein Gerüst für eine neue App und öffnet den Projektordner in Visual Studio Code.
1. Möglicherweise erhalten Sie eine Nachricht von Visual Studio Code, die sie fragt, ob Sie den Autoren der Dateien in diesem Ordner vertrauen. Wählen Sie die Schaltfläche **Ja, ich vertraue den Autoren** aus, um fortzufahren.
1. Überprüfen Sie die Projektverzeichnisse und Dateien im Explorer in Visual Studio Code, um sich mit dem Quellcode vertraut zu machen.

## Aufgabe 2: Herstellen einer Verbindung mit dem OpenAI Service

**Ziel:** Konfigurieren Sie Ihren Bot so, dass eine Verbindung mit einem OpenAI Servicd hergestellt wird, entweder über OpenAI direkt oder mithilfe von Azure OpenAI, indem Sie die erforderlichen API-Schlüssel und -Endpunkte einrichten.  

### Verwenden sie ein OpenAI-Konto
1. Öffnen Sie die Datei `.env.local.user` im Ordner `env`.
1. Füllen Sie in der Datei *env/.env.local.user* Ihren OpenAI-Schlüssel `SECRET_OPENAI_API_KEY=<your-key>`aus.
1. Öffnen Sie die Datei `app.ts` im Ordner `src`.
1. (Optional) Da diese Demonstration die Planungsfunktionen des Modells verwendet, bietet gpt-4 eine erhebliche Verbesserung gegenüber der Standardausgabe gpt-3.5. Aktualisieren Sie in der Datei *src/config.ts* den Eigenschaftswert *openAIModelName* von `"gpt-3.5-turbo"` auf `"gpt-4"` oder `"gpt-4-turbo"`.

### Benutzer Azure OpenAI:
1. Öffnen Sie die Datei `.env.local.user` im Ordner `env`.
1. Geben Sie in der Datei *env/.env.local.user* Ihren Azure OpenAI-Schlüssel `SECRET_AZURE_OPENAI_API_KEY=<azure-openai-api-key>`, den Azure OpenAI-Endpunkt `AZURE_OPENAI_ENDPOINT=<azure-openai-endpoint>` und den Azure OpenAI-Bereitstellungsnamen `AZURE_OPENAI_DEPLOYMENT_NAME=<azure-openai-deployment-name>` ein.

## Aufgabe 3: Implementieren von Codefunktionen

**Ziel:** Entwickeln Sie die Kernfunktionen Ihres Bots, indem Sie die app.ts-Datei ändern, erforderliche Importe hinzufügen und Antwortlogik implementieren, um Benutzerinteraktionen zu verarbeiten.  

1. Öffnen Sie die Datei *src/app/app.ts*. Wir ändern diese Datei gemäß den folgenden Schritten. Auf die endgültige Datei kann in [app.ts](../../../Allfiles/Labs/Guided-Exercise5/app.ts) verwiesen werden.
1. Hinzufügen von `TurnContext`-Import aus `botbuilder` 
    ```typescript
    import { MemoryStorage, TurnContext } from "botbuilder";
    ```
1. Hinzufügen von `DefaultConversationState` und `TurnState`-Importen aus `@microsoft/teams-ai`
    ```typescript
    // See https://aka.ms/teams-ai-library to learn more about the Teams AI library.
    import { Application, ActionPlanner, OpenAIModel, PromptManager, DefaultConversationState, TurnState } from "@microsoft/teams-ai";
    ```
1. Fügen Sie in der Datei *src/app.ts* vor dem Abschnitt *KI-Komponenten erstellen* die `ProjectInformation`-Schnittstelle und `ApplicationTurnState`-Definition hinzu.
    ```typescript
    // Register project information item related handlers
    interface ProjectInformation {
      projectName: string;
      tasksAccomplished: string;
      tasksComing: string;
      blockingIssues: string;
    }

    // Strongly type the applications turn state
    interface ConversationState extends DefaultConversationState {
      greeted: boolean;
      projectInformation: ProjectInformation;
    }
    type ApplicationTurnState = TurnState<ConversationState>;

    // Create AI components
    ```
1. Fügen Sie in der Datei *src/app.ts* nach dem Abschnitt *Speicher und Anwendung definieren* die Antwort des Bots auf Nachrichten hinzu.
    ```typescript
    // List for /reset command and then delete the conversation state
    app.message('/reset', async (context: TurnContext, state: ApplicationTurnState) => {
      state.deleteConversationState();
      await context.sendActivity("Your project information has been cleared.");
    });

    // Define the method for updating project information
    app.ai.action("updateProjectInformation", async (context: TurnContext, state: ApplicationTurnState, parameters: ProjectInformation) => {
      const conversation = ensureStateInitialized(state);
      if (parameters){
        if (parameters.projectName) {
          conversation.projectInformation.projectName = parameters.projectName;
        }
        if (parameters.tasksAccomplished) {
          conversation.projectInformation.tasksAccomplished = parameters.tasksAccomplished;
        } 
        if (parameters.tasksComing) {
          conversation.projectInformation.tasksComing = parameters.tasksComing;
        }
        if (parameters.blockingIssues) {
          conversation.projectInformation.blockingIssues = parameters.blockingIssues;
        }
        return `Project information was updated. Think about your next action`;
      }
    });

    // This method is used to make sure that the conversation state is initialized.
    function ensureStateInitialized(state: ApplicationTurnState): ConversationState {
      if (state.conversation.projectInformation == undefined) {
        state.conversation.projectInformation = {
          projectName: "",
          tasksAccomplished: "",
          tasksComing: "",
          blockingIssues: "",
        };
      }
      return state.conversation;
    }
    ```

## Aufgabe 4: Prompt-Updates

**Ziel:** Verfeinern Sie die Gesprächsaufforderungen des Bots, und konfigurieren Sie Funktionsaufrufe, um die Interaktionsqualität und Effektivität beim Erstellen wöchentlicher Berichte zu verbessern.

1. Aktualisieren Sie die Datei `skprompt.txt` im Ordner *src/prompts/chat*.  Auf die endgültige Datei kann in [skprompt.txt](../../../Allfiles/Labs/Guided-Exercise5/skprompt.txt) verwiesen werden
    ```txt
    You are a Teams Bot. Here is how you will act.
    Team Bot will adopt an encouraging and positive tone in all its interactions. This will be reflected in the creation of status report emails, ensuring that they are not only informative but also boost morale and foster a joyous team spirit. The language used will be engaging and supportive, aiming to excite and inspire the team while maintaining a professional undercurrent appropriate for the communication between a project manager and their team and stakeholders in a professional corporate setting. The Teams Bot will always ask for information from the user when it is not provided. 
    # Teams Bot will ask for the following project information to make status report emails:
    1. project name
    2. tasks accomplished this week
    3. tasks coming next week
    4. blocking issues

    # Status report task description like SCRUM style summary

    # Then, the users will type in the parameters and the bot will make the email.

    # For the first time, users are informed that they can clear the entered ProjectInformation with /reset command.

    # THE SUMMARY MUST BE:
    - G RATED
    - WORKPLACE / FAMILY SAFE
    NO SEXISM, RACISM OR OTHER BIAS/BIGOTRY.

    project information:
    {{$conversation.projectInfomation}}

    Typescript Interfaces:
    interface ProjectInformation {
        projectName: string;
        tasksAccomplished: string;
        tasksComing: string;
        blockingIssues: string;
    }
    ```
1. Aktualisieren von `max_tokens` und `temperature`-Parametern in der `src/prompts/chat/config.json`-Datei. Fügen Sie außerdem einen Erweiterungsknotenparameter hinzu. Daraus ergibt sich folgendes Endergebnis.  Und darauf kann in [config.json](../../../Allfiles/Labs/Guided-Exercise5/config.json) verwiesen werden.
    ```json
    {
      "schema": 1,
      "description": "AI Bot",
      "type": "completion",
      "completion": {
        "max_tokens": 2500,
        "temperature": 0.1,
        "top_p": 0.0,
        "presence_penalty": 0.6,
        "frequency_penalty": 0.0
      },
      "augmentation": {
        "augmentation_type": "monologue"
      }
    }
    ```
1. Erstellen eines neuen Ordners namens `actions.json` im Ordner *src/prompts/chat*. Die Datei enthält folgende Inhalte. Diese Datei definiert die Methoden für die zu verwendende KI. Und auf darauf kann in [actions.json](../../../Allfiles/Labs/Guided-Exercise5/actions.json) verwiesen werden
    ```json
    [
        {
            "name": "updateProjectInformation",
            "description": "updates the information for the existing project",
            "parameters": {
                "type": "object",
                "properties": {
                    "projectName": {
                        "type": "string",
                        "description": "The name of the project"
                    },
                    "tasksAccomplished": {
                        "type": "string",
                        "description": "tasks that have been accomplished"
                    },
                    "tasksComing": {
                        "type": "string",
                        "description": "tasks that are coming up"
                    },
                    "blockingIssues": {
                        "type": "string",
                        "description": "any blocking issues"
                    }
                }
            }
        }
    ]
    ```

## Arbeit überprüfen

Führen Sie Ihre App lokal aus, um die Funktionalität zu testen:

1. Öffnen Sie das **TEAMS TOOLKIT**-Pannel. Wählen Sie im Menü **LEBENSZYKLUS** die Option **Vorschau Ihrer Teams-App** aus (oder verwenden Sie die Taste `F5`), und wählen Sie dann in Ihrem bevorzugten Browser **In Teams debuggen ()** aus.  
2. Das Teams-Toolkit stellt Ihre App bereit und führt sie lokal in einem Browser aus.
3. Wählen Sie im Browser im Dialogfeld für die App-Installation **Hinzufügen** aus, um Ihre Teams-App zu installieren.  Teams öffnet eine Unterhaltung mit Ihrem installierten Bot.
4. Folgen Sie nach der Eingabe der Begrüßungsinformationen den Anweisungen zur Eingabe des Projektnamens, der erledigten Aufgaben, der nicht erledigten Aufgaben und der blockierten Aufgaben. Der KI-Bot generiert dann einen wöchentlichen Bericht ähnlich dem folgenden Screenshot.
5. Stellen Sie sicher, dass der Bot wie folgt auf die richtige Antwort antwortet. ![Screenshot des von KI erstellten wöchentlichen Berichts.](../../media/ai-weekly-report.png)
