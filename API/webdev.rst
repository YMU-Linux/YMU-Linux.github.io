=====================
Web Development [web]
=====================


Titel: Python cmd Package
--------------
Datum: 11-02-2026

Content:
    Das Python-Modul ``cmd`` ist Teil der Standardbibliothek
    und ermöglicht die einfache Erstellung eigener
    Kommandozeilen-Interpreter (Command-Line Interfaces, CLI).
    Es wird häufig verwendet, um interaktive Shell-Programme
    oder Debug-/Admin-Tools zu entwickeln.

    Das Paket stellt die Klasse ``cmd.Cmd`` bereit,
    von der eine eigene Klasse erben kann.
    Befehle werden als Methoden mit dem Präfix ``do_`` definiert.

    Grundstruktur:

    .. code-block:: python

        import cmd

        class MyShell(cmd.Cmd):
            intro = "Welcome to MyShell. Type help or ? to list commands."
            prompt = "(myshell) "

            def do_greet(self, arg):
                "Greets the user"
                print(f"Hello {arg}")

            def do_exit(self, arg):
                "Exit the shell"
                print("Goodbye!")
                return True

        if __name__ == "__main__":
            MyShell().cmdloop()

    Wichtige Konzepte:

    do_<command>
        Jede Methode mit diesem Namensmuster wird
        als CLI-Befehl verfügbar.

    help_<command>
        Ermöglicht individuelle Hilfeausgaben
        für einzelne Befehle.

    default()
        Wird aufgerufen, wenn ein unbekannter
        Befehl eingegeben wird.

    cmdloop()
        Startet die interaktive Eingabeschleife.

    Vorteile:
        - Kein externes Paket notwendig
        - Einfache Struktur für CLI-Tools
        - Eingebaute Help-Funktion

    Nachteile:
        - Begrenzte moderne CLI-Features
        - Weniger flexibel als Frameworks wie argparse oder click

    Einsatzgebiete:
        - Interaktive Admin-Tools
        - Debugging-Interfaces
        - Kleine Lernprojekte
        - Prototyping von CLI-Anwendungen

    - Was habe ich gelernt?
      Aufbau eines einfachen interaktiven CLI-Programms
      mit Vererbung von cmd.Cmd und do_-Methoden.

    - Welche Probleme gab es?
      Verständnis der internen Befehlsverarbeitung
      und des Rückgabewerts für das Beenden.

    - Wie habe ich sie gelöst?
      Durch Experimentieren mit eigenen Befehlen
      und Testen der help-Funktion.

    - Nächster Schritt?
      Kombination mit Argument-Parsing
      oder Integration in größere Python-Projekte.

--------------------------------

Titel: Progressive Web Apps (PWA)
--------
Datum: 06-02-2026

Content:
    Progressive Web Apps (PWAs) sind moderne Webanwendungen, die sich wie
    native Apps anfühlen, aber mit Webtechnologien wie HTML, CSS und
    JavaScript entwickelt werden. Ziel ist es, die Vorteile von Websites
    (einfache Verteilung über eine URL, keine Installation notwendig)
    mit den Vorteilen nativer Apps (Offline-Fähigkeit, Installation,
    Push-Benachrichtigungen, Performance) zu kombinieren.

    Eine PWA besteht aus mehreren zentralen Bausteinen:

    Service Worker
        Ein Service Worker ist ein JavaScript-File, das im Hintergrund
        läuft und zwischen Anwendung und Netzwerk vermittelt.
        Er kann Requests abfangen und Ressourcen im Cache speichern.
        Dadurch kann die Anwendung auch offline funktionieren oder
        Inhalte deutlich schneller laden.
        Typische Aufgaben:
        - Caching von HTML, CSS, JS und Bildern
        - Offline-Fallback-Seiten bereitstellen
        - Push Notifications verwalten

    Web App Manifest
        Das Manifest ist eine JSON-Datei (z.B. manifest.json),
        die Metadaten über die Anwendung enthält.
        Es definiert unter anderem:
        - name und short_name der App
        - Icons in verschiedenen Größen
        - start_url
        - display-Modus (z.B. standalone)
        - theme_color und background_color

        Durch das Manifest erkennt der Browser,
        dass die Website "installierbar" ist.
        Nutzer können die PWA dann wie eine normale App
        auf dem Homescreen speichern.

        Beispiel:

        .. code-block:: json

            {
                "name": "Meine PWA",
                "short_name": "PWA",
                "start_url": "/index.html",
                "display": "standalone",
                "background_color": "#ffffff",
                "theme_color": "#000000",
                "icons": [
                    {
                        "src": "icon-192.png",
                        "sizes": "192x192",
                        "type": "image/png"
                    }
                ]
            }

    HTTPS
        Eine PWA muss über HTTPS ausgeliefert werden,
        da Service Worker nur in sicheren Kontexten funktionieren.

    Vorteile von PWAs:
        - Plattformunabhängig (läuft auf Desktop und Mobile)
        - Keine App-Store-Abhängigkeit
        - Offline-Nutzung möglich
        - Schnellere Ladezeiten durch Caching
        - Installierbar wie eine native App

    Typische Einsatzgebiete sind Webshops, News-Portale,
    interne Firmen-Tools oder Web-Apps mit wiederkehrenden Nutzern.


----------------------------------------

Titel: Go Web Server mit go:embed und html/template
-------
Datum: 08-01-2026

Content:
    Go (Golang) eignet sich sehr gut für schlanke,
    performante Webserver. Mit dem Standardpaket
    ``net/http`` lassen sich HTTP-Server ohne
    externe Frameworks erstellen.

    Seit Go 1.16 gibt es das Feature ``go:embed``.
    Damit können statische Dateien (z.B. HTML,
    CSS oder Templates) direkt in das kompilierte
    Binary eingebettet werden. Dadurch entsteht
    eine eigenständige ausführbare Datei ohne
    zusätzliche Template-Dateien im Dateisystem.

    Für serverseitiges Rendering wird häufig
    das Paket ``html/template`` verwendet.
    Es ermöglicht sicheres HTML-Templating
    mit automatischem Escaping gegen XSS.

    Beispiel eines minimalen Webservers
    mit eingebettetem Template:

    .. code-block:: go

        package main

        import (
            "embed"
            "html/template"
            "net/http"
        )

        //go:embed templates/index.html
        var templateFS embed.FS

        func main() {
            tmpl := template.Must(
                template.ParseFS(templateFS, "templates/index.html"),
            )

            http.HandleFunc("/", func(w http.ResponseWriter, r *http.Request) {
                data := struct {
                    Title string
                    Message string
                }{
                    Title:   "Go Baby Server",
                    Message: "Hello from embedded template!",
                }

                tmpl.Execute(w, data)
            })

            http.ListenAndServe(":8080", nil)
        }

    Beispiel eines einfachen Templates (index.html):

    .. code-block:: html

        <!DOCTYPE html>
        <html>
        <head>
            <title>{{ .Title }}</title>
        </head>
        <body>
            <h1>{{ .Message }}</h1>
        </body>
        </html>

    Wichtige Punkte:

    go:embed
        - Dateien werden zur Compile-Zeit eingebettet
        - Keine Abhängigkeit vom Dateisystem zur Laufzeit
        - Ideal für kleine Deployments

    html/template
        - Automatisches Escaping von HTML
        - Platzhalter mit {{ .FieldName }}
        - Daten werden über Structs übergeben

    Vorteile dieses Ansatzes:
        - Ein einziges ausführbares Binary
        - Keine externen Template-Dateien notwendig
        - Sehr schnelle Startzeit
        - Keine externen Abhängigkeiten

    Dieser Aufbau eignet sich besonders für:
        - Kleine APIs mit HTML-Frontend
        - Interne Tools
        - Microservices mit einfacher UI
        - Lernprojekte

    - Was habe ich gelernt?
      Verwendung von go:embed zur Einbettung
      von Templates sowie sicheres Rendering
      mit html/template.

    - Welche Probleme gab es?
      Verständnis der Template-Pfade
      und des ParseFS-Aufrufs.

    - Wie habe ich sie gelöst?
      Durch Testen der Ordnerstruktur
      und Analyse der Fehlermeldungen beim Kompilieren.

    - Nächster Schritt?
      Static Files (CSS/JS) ebenfalls einbetten
      und Routing erweitern.

----------------------------------------


C# Blazor – Server, WebAssembly und Hybrid Architektur
------------------
Datum: 09-11-2025

Content:
    Blazor ist ein Webframework aus dem ASP.NET-Core-Ökosystem,
    mit dem interaktive Webanwendungen vollständig in C# entwickelt
    werden können. Die UI wird mit Razor-Komponenten (.razor)
    definiert und als Komponentenbaum gerendert.

    Es existieren drei offizielle Hosting-Modelle:

    Blazor Server
        Bei Blazor Server läuft die gesamte Anwendungslogik
        auf dem Server. Der Browser erhält eine dynamisch
        aktualisierte UI über eine permanente SignalR-Verbindung.

        Ablauf:
        - Benutzer klickt im Browser
        - Event wird an den Server gesendet
        - Server verarbeitet Logik
        - UI-Diff wird zurück an den Client gesendet

        Vorteil:
            Geringe Initial-Downloadgröße

        Nachteil:
            Permanente Serververbindung notwendig

    Blazor WebAssembly (Client)
        Bei Blazor WebAssembly wird die .NET-Runtime
        in den Browser geladen (WebAssembly).
        Die Anwendung läuft vollständig clientseitig.
        Backend-Kommunikation erfolgt optional über HTTP APIs.

        Vorteil:
            Keine dauerhafte Verbindung erforderlich

        Nachteil:
            Größerer Initial-Download

    Blazor Hybrid
        Blazor Hybrid wird typischerweise mit .NET MAUI,
        WPF oder WinForms kombiniert. Die Razor-Komponenten
        werden in einer nativen Anwendung gerendert
        (über ein WebView-Control).

        Wichtig:
            In einer Hybrid-Anwendung laufen Client-Logik
            (UI, Interaktionen) und Server- bzw. Backend-Logik
            parallel innerhalb derselben .NET-Anwendung.
            Es existiert keine klassische Trennung wie
            bei WebAssembly + externem Server.

        Das bedeutet:
            - UI-Code läuft lokal im Prozess der App
            - Geschäftslogik kann direkt im selben Projekt
              oder über gemeinsame Services genutzt werden
            - Kein Netzwerk-Overhead zwischen UI und Logik

        Dadurch eignet sich Hybrid besonders für
        Desktop- und Mobile-Apps mit gemeinsamer C#-Codebasis.

    Beispiel einer Razor-Komponente:

    .. code-block:: csharp

        @page "/counter"

        <h3>Counter</h3>

        <p>Current count: @currentCount</p>

        <button @onclick="IncrementCount">Click me</button>

        @code {
            private int currentCount = 0;

            private void IncrementCount()
            {
                currentCount++;
            }
        }

    Beispiel eines Services (gemeinsame Logik):

    .. code-block:: csharp

        public class CounterService
        {
            public int Count { get; private set; }

            public void Increment()
            {
                Count++;
            }
        }

    Registrierung (z.B. in Program.cs):

    .. code-block:: csharp

        builder.Services.AddSingleton<CounterService>();

    In Blazor Hybrid kann dieser Service direkt
    innerhalb der gleichen Anwendung genutzt werden,
    ohne HTTP oder SignalR-Kommunikation.

    Architektur-Vergleich:

        Blazor Server:
            UI-Diff über SignalR
            Server verarbeitet Events

        Blazor WebAssembly:
            Runtime im Browser
            API-Aufrufe über HTTP

        Blazor Hybrid:
            UI und Logik laufen im selben Prozess
            Gemeinsame Services ohne Netzwerk

----------------------------------------

Web Socket example
-------------
Datum: 2025-05-12

Content:

    .. code-block:: js

        import express from 'express';
        import http from 'http';
        import WebSocket, { WebSocketServer } from 'ws';

        // Create Express app and HTTP server
        const app = express();
        const server = http.createServer(app);

        // Create WebSocket server
        const wss = new WebSocketServer({ server });

        // Handle WebSocket connections
        wss.on('connection', (ws) => {
            console.log('New client connected');

            // Handle incoming messages
            ws.on('message', (message) => {
                console.log(`Received: ${message}`);

                // Echo message to all connected clients
                wss.clients.forEach(client => {
                    if (client.readyState === WebSocket.OPEN) {
                        client.send(`Echo: ${message}`);
                    }
                });
            });

            ws.on('close', () => {
                console.log('Client disconnected');
            });
        });

        // Basic HTTP route
        app.get('/', (_req, res) => {
            res.send('WebSocket server is running');
        });

        // Start server
        const PORT = 3000;
        server.listen(PORT, () => {
            console.log(`Server listening at http://localhost:${PORT}`);
        });

----------------------------------------

.. important::

   **DATA MIGRATION IN PROGRESS**

   - Legacy (old) data will be added gradually over time.
   - This notice will remain visible until all previous data has been fully migrated.
   - Content may continue to update during this transition period.