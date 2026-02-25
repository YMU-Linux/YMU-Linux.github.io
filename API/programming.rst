=================
Programming [prg]
=================

Einführung in F#
-------------
Datum: 20-02-2026

Content:
    F# ist eine funktionale Programmiersprache aus dem .NET-Ökosystem.
    Sie kombiniert funktionale, imperative und objektorientierte
    Programmierparadigmen, legt jedoch den Schwerpunkt klar
    auf funktionale Konzepte wie unveränderliche Daten (Immutability),
    Funktionen als First-Class Citizens und Pattern Matching.

    F# wird kompiliert und läuft auf der .NET Runtime.
    Dadurch kann F# problemlos mit C#-Bibliotheken und
    bestehenden .NET-Projekten kombiniert werden.

    Grundlegende Syntax:

    .. code-block:: fsharp

        // Variable (immutable by default)
        let number = 10

        // Funktion
        let square x = x * x

        // Funktionsaufruf
        let result = square 5

    Wichtige Konzepte:

    Immutability
        Werte sind standardmäßig unveränderlich.
        Das reduziert Seiteneffekte und erleichtert
        parallele Programmierung.

    Pattern Matching
        Ein zentrales Sprachfeature, das komplexe
        Entscheidungsstrukturen klar und lesbar macht.

    .. code-block:: fsharp

        let describeNumber x =
            match x with
            | 0 -> "Zero"
            | 1 -> "One"
            | _ -> "Other number"

    Typinferenz
        Der Compiler kann Typen automatisch erkennen,
        wodurch weniger explizite Typangaben notwendig sind.

    Listenverarbeitung

    .. code-block:: fsharp

        let numbers = [1; 2; 3; 4; 5]
        let squared = numbers |> List.map square

    Vorteile von F#:
        - Sehr kompakte und ausdrucksstarke Syntax
        - Gute Unterstützung für funktionale Programmierung
        - Starke Typisierung mit Typinferenz
        - Ideal für Datenverarbeitung und mathematische Logik

    Herausforderungen:
        - Umdenken für Entwickler mit rein objektorientiertem Hintergrund
        - Geringere Verbreitung im Vergleich zu C#

    F# eignet sich besonders für:
        - Datenanalyse
        - Finanz- und mathematische Anwendungen
        - Backend-Services mit klarer Logik

    - Was habe ich gelernt?
      Grundprinzipien der funktionalen Programmierung in F#,
      insbesondere Immutability, Pattern Matching und Typinferenz.

    - Welche Probleme gab es?
      Gewöhnung an die andere Syntax und Denkweise
      im Vergleich zu C#.

    - Wie habe ich sie gelöst?
      Durch kleine Codebeispiele und Vergleich
      derselben Logik in C# und F#.

    - Nächster Schritt?
      Async-Workflows und funktionale Error-Handling-Konzepte
      wie Option und Result vertiefen.

----------------------------------------

C# Template Writing
-------------
Datum: 03-12-2026

Content:
    Generics in Methoden
        Eine generische Methode verwendet einen Platzhalter-Typ (z.B. T),
        der zur Laufzeit durch einen konkreten Typ ersetzt wird.

    .. code-block:: csharp

        public static T FirstOrDefault<T>(List<T> items)
        {
            if (items == null || items.Count == 0)
                return default;

            return items[0];
        }

    Generics in Klassen
        Eine generische Klasse kann Daten typsicher kapseln, z.B. eine Box,
        die immer genau einen definierten Typ speichert.

    .. code-block:: csharp

        public class Box<T>
        {
            public T Value { get; set; }

            public Box(T value)
            {
                Value = value;
            }
        }

        // Usage
        var intBox = new Box<int>(42);
        var stringBox = new Box<string>("Hello");

    Constraints (Einschränkungen)
        Mit Constraints kann festgelegt werden, welche Typen erlaubt sind.
        Das ist nützlich, wenn eine Methode bestimmte Fähigkeiten erwartet
        (z.B. parameterloser Konstruktor oder Vererbung von einer Basisklasse).

    .. code-block:: csharp

        public class Repository<T> where T : class, new()
        {
            public T Create()
            {
                return new T();
            }
        }

    Template-Ansatz für wiederverwendbare Strukturen
        In Projekten wird "Template Writing" oft auch verwendet,
        um wiederholbare Patterns als Vorlage zu definieren,
        z.B. für Services, DTOs oder Controller.
        Dadurch entstehen konsistente Strukturen im Code.


----------------------------------------

Custom Connector in der Microsoft Power Platform
---------------
Datum: 20-11-2025

Content:
    Ein Custom Connector ermöglicht die Anbindung
    einer eigenen REST-API an Power Apps oder Power Automate.
    Dadurch können externe Systeme integriert werden,
    die nicht standardmäßig als Konnektor vorhanden sind.

    Grundlage:
        - OpenAPI (Swagger) Definition
        - REST API mit HTTPS
        - Authentifizierung (z.B. API Key, OAuth2)

    Aufbau eines Custom Connectors:

    1. API-Definition importieren (Swagger/OpenAPI)
    2. Authentifizierung konfigurieren
    3. Aktionen und Parameter definieren
    4. Testen im Connector-Designer
    5. Veröffentlichung für Umgebung

    Beispiel einer einfachen REST-Definition:

    .. code-block:: json

        {
            "paths": {
                "/hello": {
                    "get": {
                        "summary": "Returns greeting",
                        "responses": {
                            "200": {
                                "description": "OK"
                            }
                        }
                    }
                }
            }
        }

    Nach Veröffentlichung kann der Custom Connector
    in Power Apps oder Power Automate wie ein
    Standard-Konnektor verwendet werden.

    Vorteile:
        - Integration proprietärer Systeme
        - Erweiterung der Plattform
        - Wiederverwendbarkeit in mehreren Apps/Flows

    Herausforderungen:
        - Authentifizierung korrekt konfigurieren
        - Fehlerbehandlung bei API-Responses

    - Was habe ich gelernt?
      Erstellung und Konfiguration eines eigenen Connectors
      auf Basis einer REST-API.

    - Welche Probleme gab es?
      Authentifizierungsfehler und CORS-Probleme.

    - Wie habe ich sie gelöst?
      Anpassung der API-Security und Testen mit Postman
      vor Integration in die Power Platform.

    - Nächster Schritt?
      Komplexere API-Strukturen mit mehreren Endpunkten anbinden.

----------------------------------------


Titel: Microsoft Power Automate
-----------------------
Datum: 13-11-2025

Content:
    Microsoft Power Automate ist ein Workflow-Automatisierungstool
    innerhalb der Microsoft Power Platform.
    Es ermöglicht die Automatisierung von Prozessen
    zwischen verschiedenen Diensten und Anwendungen.

    Zentrale Konzepte:

    Trigger
        Ein Ereignis, das einen Flow startet
        (z.B. "Wenn eine neue Datei in SharePoint erstellt wird").

    Actions
        Schritte, die nach dem Trigger ausgeführt werden
        (z.B. E-Mail senden, Datensatz erstellen, API aufrufen).

    Typen von Flows:
        - Cloud Flows
        - Desktop Flows (RPA)
        - Scheduled Flows

    Beispiel:
        Trigger: Neue E-Mail erhalten
        Aktion: Speichere Anhang in OneDrive
        Aktion: Sende Benachrichtigung in Teams

    Vorteile:
        - Keine Programmierkenntnisse notwendig
        - Viele vorgefertigte Konnektoren
        - Integration mit Microsoft 365

    Einschränkungen:
        - Lizenzabhängigkeit
        - Komplexe Flows werden schnell unübersichtlich

    - Was habe ich gelernt?
      Erstellung automatisierter Workflows
      und Nutzung von Trigger-Action-Strukturen.

    - Welche Probleme gab es?
      Fehleranalyse bei verschachtelten Bedingungen.

    - Wie habe ich sie gelöst?
      Nutzung von Testläufen und Flow-Run-Historie.

    - Nächster Schritt?
      Integration externer APIs in einen Flow.

----------------------------------------

Microsoft Power Apps
------------
Datum: 5-11-2025

Content:
    Microsoft Power Apps ist Teil der Microsoft Power Platform
    und ermöglicht die Erstellung von Low-Code-/No-Code-Anwendungen
    für Web und Mobile. Ziel ist es, Geschäftsprozesse schnell
    digital abzubilden, ohne klassische Softwareentwicklung.

    Es gibt zwei Haupttypen:
        - Canvas Apps (freie UI-Gestaltung)
        - Model-Driven Apps (datengetrieben, basierend auf Dataverse)

    Power Apps verwendet eine Excel-ähnliche Formelsprache.
    Wichtig ist dabei der Unterschied zwischen der englischen
    und europäischen Version:

    Unterschiedliche Syntax (EN vs EU):

    - Trennzeichen für Funktionsparameter:
        EN-Version: Komma ","
        EU-Version: Semikolon ";"

    - Dezimaltrennzeichen:
        EN-Version: Punkt (.)
        EU-Version: Komma (,)

    Beispiel EN:

    .. code-block:: powerfx

        If(Sum(Orders, Amount) > 1000, "High", "Low")

    Beispiel EU:

    .. code-block:: powerfx

        If(Sum(Orders; Amount) > 1000; "High"; "Low")

    Dieser Unterschied kann zu Fehlern führen,
    wenn Formeln aus Dokumentationen kopiert werden.

    - Was habe ich gelernt?
      Erstellung einfacher Business-Apps,
      Nutzung von Power Fx und Datenanbindung (z.B. SharePoint, Dataverse).

    - Welche Probleme gab es?
      Syntaxfehler durch unterschiedliche Ländereinstellungen.

    - Wie habe ich sie gelöst?
      Anpassung der Formeln an regionale Einstellungen
      und Überprüfung der App-Sprache.

    - Nächster Schritt?
      Komplexere Logik mit Collections und Variablen umsetzen.

----------------------------------------

Microsoft Entity Framework Core (EF Core)
----------
Datum: 23-10-2025

Content:
    Entity Framework Core (EF Core) ist ein modernes
    Object-Relational Mapping (ORM) Framework von Microsoft
    für .NET und C#. Es ermöglicht die Arbeit mit Datenbanken
    über C#-Klassen, ohne direkt SQL schreiben zu müssen.

    EF Core bildet Tabellen auf Klassen (Entities) ab
    und Datensätze auf Objekte. Die Kommunikation mit
    der Datenbank erfolgt über einen sogenannten DbContext.

    Zentrale Konzepte:

    Entity
        Eine normale C#-Klasse, die eine Datenbanktabelle
        repräsentiert.

    .. code-block:: csharp

        public class Product
        {
            public int Id { get; set; }
            public string Name { get; set; }
            public decimal Price { get; set; }
        }

    DbContext
        Der DbContext verwaltet die Verbindung zur Datenbank
        sowie das Tracking von Änderungen.

    .. code-block:: csharp

        using Microsoft.EntityFrameworkCore;

        public class AppDbContext : DbContext
        {
            public DbSet<Product> Products { get; set; }

            public AppDbContext(DbContextOptions<AppDbContext> options)
                : base(options)
            {
            }
        }

    Registrierung in ASP.NET Core (Program.cs):

    .. code-block:: csharp

        builder.Services.AddDbContext<AppDbContext>(options =>
            options.UseSqlServer(
                builder.Configuration.GetConnectionString("DefaultConnection")
            )
        );

    CRUD-Beispiel:

    .. code-block:: csharp

        // Create
        var product = new Product { Name = "Laptop", Price = 999.99m };
        context.Products.Add(product);
        context.SaveChanges();

        // Read
        var products = context.Products.ToList();

        // Update
        product.Price = 899.99m;
        context.SaveChanges();

        // Delete
        context.Products.Remove(product);
        context.SaveChanges();

    Migrations
        EF Core unterstützt Code-First-Migrations.
        Damit können Datenbankstrukturen direkt
        aus dem C#-Modell generiert werden.

    .. code-block:: bash

        dotnet ef migrations add InitialCreate
        dotnet ef database update

    Vorteile von EF Core:
        - Starke Typisierung
        - LINQ-Unterstützung
        - Datenbankunabhängig (SQL Server, PostgreSQL, SQLite, etc.)
        - Integriert in ASP.NET Core

    Nachteile:
        - Performance kann bei komplexen Queries leiden
        - Abstraktion kann SQL-Verständnis verdecken

    EF Core eignet sich besonders für
    Web-APIs, Unternehmensanwendungen
    und datengetriebene Systeme

----------------------------------------

   **DATA MIGRATION IN PROGRESS**

   - Legacy (old) data will be added gradually over time.
   - This notice will remain visible until all previous data has been fully migrated.
   - Content may continue to update during this transition period.