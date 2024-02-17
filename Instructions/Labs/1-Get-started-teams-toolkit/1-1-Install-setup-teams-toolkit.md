# Übung 1: Installieren und Einrichten von Teams-Toolkit für Visual Studio Code

In dieser Übung installieren Sie das Teams-Toolkit für Visual Studio Code und richten Ihre Umgebung ein.

## Aufgabe 1: Installieren von Teams-Toolkit für Visual Studio Code

1. Öffnen Sie **Visual Studio Code**.
2. Wählen Sie in der Seitenleiste das Symbol für **Erweiterungen** aus.
3. Suchen Sie im Bereich **Erweiterungen** mithilfe der Suchleiste nach „Teams-Toolkit“. Wählen Sie dann **Installieren** aus.

:::image type="content" source="../../media/teams-toolkit-install.png" alt-text="Screenshot: Installation des Teams-Toolkits in Visual Studio Code.":::

**Hinweis:**  Für die Übungen in diesem Modul wird das Teams-Toolkit V5.0.0 verwendet.

Sie können das Teams-Toolkit auch von [Visual Studio Marketplace](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension) installieren.

## Aufgabe 2: Vorbereiten Ihres Geschäfts-, Schul- oder Unikontos für Microsoft 365

Wenn Sie bereits über Administratorzugriff auf ein Geschäfts-, Schul- oder Unikonto für Microsoft 365 verfügen, das für Entwicklung und Tests geeignet ist, können Sie dieses Konto verwenden, um Ihre App auszuführen und zu debuggen. Verwenden Sie unbedingt einen Mandanten, in dem Vorgänge sicher ausgeführt werden können, ohne dass echte Benutzer:innen beeinträchtigt werden.

Andernfalls können Sie ein kostenloses Testkonto mit dem [Microsoft 365-Entwicklerprogramm](https://aka.ms/m365developers) erstellen.  Nach Abschluss der Einrichtung bietet das Microsoft 365-Entwicklerprogramm Ihnen Administratorzugriff auf einen Mandanten, den Sie zum Erstellen von Teams-Apps verwenden können.

## Aufgabe 3: Konfigurieren eines Microsoft 365-Mandanten zum Hochladen von Apps für Teams

Aktivieren Sie das Querladen von benutzerdefinierten Apps für Ihren Mandanten, indem Sie die folgenden Schritte ausführen:

1. Melden Sie sich mit Ihren Microsoft 365-Administratoranmeldeinformationen beim [Microsoft Teams Admin Center](https://admin.teams.microsoft.com) an.

2. Wählen Sie in der Seitenleiste **Teams-Apps** aus, und wählen Sie dann **Einrichtungsrichtlinien** aus.

3. Wählen Sie die **Globale Richtlinie (organisationsweite Standardeinstellung)** aus, und aktivieren Sie dann die Umschaltfläche **Benutzerdefinierte Apps hochladen**. 
   :::image type="content" source="../../media/configure-upload-apps.png" alt-text="Screenshot: Konfiguration von Uploads für benutzerdefinierte Apps.":::

4. Wählen Sie die Schaltfläche **Speichern** aus, um Ihre Änderungen zu speichern. Ihr Mandant ist jetzt so konfiguriert, dass das Querladen von benutzerdefinierten Apps zulässig ist.

In der nächsten Lerneinheit erfahren Sie, wie Sie eine Teams-App erstellen und lokal in Teams ausführen.
