# Masterthesis Musa Tanirak 
Manuall vs ChatGPT C4 modeling

Execution 3:
1st try with ChatGpt Input:
### Input 1 – Kontextlevel
#### Wissenschaftliche und detaillierte Beschreibung: Validierungs- und Fehlerkommunikation bei individualisierten Produktanpassungen
#### Hintergrund
Für bestimmte digitale Produkte mit individuellen Anpassungsoptionen – etwa im Bereich Gesundheit, Optik oder Technik – ist es notwendig, dass Kund\:innen vor der Produktion spezifische Konfigurationsdaten (z. B. biometrische oder messtechnische Werte) bereitstellen. Diese Daten werden häufig als Bild- oder Dokumentdateien hochgeladen und müssen automatisiert geprüft und weiterverarbeitet werden.

Der folgende Use Case beschreibt die **Kommunikations- und Fehlerbehandlungsprozesse** sowie den **technischen Datenfluss** zwischen einem externen Handelspartner, einer Middleware-Plattform und den internen Verarbeitungs- und Supportsystemen eines Produktherstellers. Ziel ist es, die Korrektheit und Vollständigkeit der eingereichten Daten sicherzustellen, Fehler frühzeitig zu identifizieren und die Kund\:innen gezielt bei der Korrektur zu unterstützen.

---
### Systemübersicht
1. **Externer Vertriebspartner**
   * **Bestellplattform**: Webseite zur Produktauswahl und zum Hochladen individueller Daten.
   * **Datenbank**: Speicherung der übermittelten Bestell- und Konfigurationsdaten, die anschließend an das interne Validierungssystem weitergeleitet werden.
2. **Middleware**
   * Vermittelt den Datentransfer zwischen dem externen System und dem internen **Order Processing System** (OP).
   * Steuert den weiteren Datenfluss zwischen OP und den internen Backend-Systemen (bestehend aus Funktionen, Automatisierung und Datenspeicherung).
3. **Interne Systeme**
   * **Order Processing System (OP)**: Automatisierte Prüfung der übermittelten Konfigurationsdaten.
   * **Backend-Komponenten (z. B. Logic Apps, Functions, Storage)**: Auswertung, Kategorisierung und Speicherung von Fehlern.
   * **Webportal für Kund\:innen**: Darstellung von Prüfergebnissen und Korrekturmöglichkeiten.
   * **CRM-System**: Verwaltung von Supportanfragen und direkter Kundenkommunikation.
   * **Regelbasierte Datenbank (z. B. Excel)**: Hinterlegte länderspezifische Validierungsregeln.
---
### Prozessbeschreibung
1. **Datenübermittlung**
   Kund\:innen bestellen ein individualisiertes Produkt über das externe Bestellportal und laden dazu erforderliche Konfigurationsdaten hoch. Diese werden gespeichert und über die Middleware an das interne Order Processing System weitergeleitet.
2. **Automatisierte Datenprüfung**
   Das OP-System analysiert die eingereichten Daten und identifiziert mögliche Fehler wie:
   * Fehlende oder unvollständige Angaben
   * Unleserliche Inhalte (z. B. in gescannten Dokumenten)
   * Formatierungs- oder Plausibilitätsfehler
   Die Ergebnisse, inklusive Fehlercodes und Identifikatoren, werden an das Backend zur weiteren Verarbeitung übergeben.
3. **Verarbeitung und Klassifikation**
   Die Backend-Systeme werten die Fehler entsprechend länderspezifischer Regelwerke aus, speichern valide Informationen und leiten relevante Fehlerdaten an das Kundenportal und das CRM-System weiter.
4. **Kundenspezifisches Webportal**
   Für jede Bestellung wird automatisch ein personalisiertes Webportal generiert, das:
   * Den Status der Prüfung anzeigt
   * Identifizierte Fehler nachvollziehbar auflistet
   * Ein Formular zur Korrektur oder Neueinreichung bietet
5. **CRM-gestützte Kundenkommunikation**
   Die vom Kunden eingereichten Korrekturen werden über das Portal an das CRM-System übermittelt, wo ein neues Ticket angelegt oder ein bestehendes aktualisiert wird. Supportmitarbeitende können direkt Rückfragen stellen und offene Punkte klären.
6. **Freigabe zur Produktion**
   Nach erfolgreicher Korrektur und abschließender Validierung wird der Datensatz freigegeben und sicher im System gespeichert. Die anschließende Produktion kann beginnen.
7. **Systempflege und Fehleroptimierung**
   Fehlerhafte Prüfprozesse werden regelmäßig überprüft, manuell angepasst und kontinuierlich verbessert, um die Qualität der automatisierten Analyse zu erhöhen.
---
### Vorteile der Middleware im Datenfluss
1. **Zentrale Systemintegration**
   Die Middleware fungiert als Vermittlungsinstanz zwischen externen und internen Systemen und gewährleistet einen stabilen, modularen Datentransfer.
2. **Effizienter Informationsfluss**
   Die Entkopplung der externen Plattform von internen Verarbeitungssystemen ermöglicht eine klare Verantwortungsverteilung und flexible Anpassbarkeit.
3. **Erhöhte Fehlererkennung und Transparenz**
   Fehler werden frühzeitig erkannt, strukturiert verarbeitet und den Kund\:innen klar kommuniziert.
4. **Skalierbarkeit und Zukunftsfähigkeit**
   Durch die modulare Architektur der Middleware können zusätzliche Funktionen oder neue Zielsysteme problemlos integriert werden.
---
Dieser Use Case verdeutlicht, wie eine strukturierte Middleware-Architektur den Datenfluss zwischen **externer Bestellung und interner Verarbeitung** effizient, nachvollziehbar und fehlertolerant gestalten kann. Die klare Trennung von externen und internen Zuständigkeiten ermöglicht eine **skalierbare, sichere und benutzerfreundliche** Abwicklung individualisierter Produktprozesse.
---

### Input Execution 4
### Here is the description of the system: 
This system handles customer orders that include uploaded documents. The process begins when a customer submits an order
via an external website. The website performs basic file checks (e.g., size, format) and stores the order data in an external database. The document is then transmitted
to the internal infrastructure through Azure ESB, which serves as a secure middleware bridging external and internal components. Within the internal system, Azure
ESB forwards the document to the Order Processing module. This component uses AI-based analysis to examine the document and detect any potential errors. If
errors are identified, the classified data is passed on to the Error Handling module. Error Handling manages country-specific validation rules, generates unique token
IDs for tracking purposes, and forwards the error data to Salesforce. Salesforce is the internal CRM system and is responsible for both internal case tracking and
direct communication with the customer. Based on the received information, Salesforce creates support tickets and sends status updates. To support customer
interaction, there is an internal web interface based on Adobe Experience Manager (AEM). Through this interface, customers can access detailed error information
using their token ID. Additionally, an integrated web form within the AEM interface allows customers to submit corrections or support requests, which are then
routed to Salesforce for customer support handling. The entire process is monitored by Azure Monitor, which continuously tracks performance and ensures early
detection of technical issues or bottlenecks. The system follows a modular architecture, with each component handling a clearly defined responsibility. This approach
ensures high scalability, maintainability, and operational reliability.

### Component Diagram
Focus: Error Handling – Architecture and Data Flow This section outlines the flow and processing of error-related information within the system, with a specific
focus on the responsibilities of the Error Handling component. 1. Data Transfer from Order Processing Once Order Processing has analyzed the uploaded document,
any identified error data is sent to the Error Handling module via an Azure Service Bus interface. This provides a reliable and asynchronous communication channel
between system components. 2. Processing Within Logic Apps The Error Handling logic is implemented through several Azure Logic Apps, each with a dedicated
role: Token Generation: A Logic App generates a unique Token ID for each record to ensure traceability throughout the system. Country-Specific URL Construction:
A second Logic App combines the generated Token ID with a country-specific static base URL, resulting in a unique access link for each case. This is commonly
referred to as the “Country URL.” 3. Data Collector: Routing and Persistence The generated information – including the Country URL, Token ID, error codes, and
metadata – is then forwarded to a central Logic App known as the Data Collector, which performs two key functions: Forwarding to Salesforce: The data is
structured and transmitted to Salesforce, where it is used to create support cases or inform customer communication. Centralized Storage: In parallel, the Data
Collector stores all records in a centralized Azure Table Storage instance referred to as “All Data,” serving as the system’s main persistent data store for all tokenbased
error data. 4. Integration with Country-Specific Excel Data A complementary service known as the Excel Service allows regional stakeholders to maintain
translations and localized configurations using an Excel file. This file is uploaded to Azure Storage and used by the Data Collector to enrich records with localized
content. To ensure consistency, a dedicated Logic App listens for changes to the Excel file. When updates occur, it triggers a synchronization routine that updates
both Azure Storage and the All Data table, ensuring that all information remains aligned with the most current Excel content. 5. Presentation on the AEM Website
The processed error information is presented to customers via a web page built using Adobe Experience Manager (AEM), with the following architecture: The AEM
page itself does not fetch the data directly. Instead, it contains an embedded React application. The React app extracts the Token ID from the URL and sends a
request to an Azure Function. This function queries the All Data table, retrieves the matching data, and returns it to the React app. The React app then dynamically
renders the error information within the AEM web interface. 6. Submission via Web Form The AEM-based page also includes a button that redirects the user to a
separate web form, designed for submitting corrections or inquiries: This form is an independent web application. It communicates directly with Salesforce,
bypassing the AEM system entirely.


