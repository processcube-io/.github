# ProcessCube® — Prozesse modellieren, automatisieren, von Agenten ausführen lassen

> Wiederkehrende Aufgaben, Abläufe und Entscheidungen — digital, automatisiert und nachvollziehbar.
> BPMN 2.0 als gemeinsame Sprache für Fachbereich, Entwicklung und KI-Agenten.

---

## Was ist ProcessCube?

ProcessCube ist eine **selbst hostbare Plattform für Prozessorchestrierung**. Kern ist eine BPMN-2.0-Workflow-Engine: Was im Diagramm steht, wird genau so ausgeführt — kein verstecktes Verhalten, keine Blackbox.

Vier Wege, Logik anzubinden:

- **Modellieren** — BPMN im Studio, deployen auf die Engine
- **LowCode** — Node-RED-basierte Flows für Integrationen und UIs ohne eigenen Service
- **Code** — External Task Worker in TypeScript, Python oder .NET
- **KI-Agenten** — ein Agent übernimmt einen External Task, die Engine behält die Kontrolle

Läuft als Docker Compose auf dem Laptop und als Kubernetes-Deployment in Produktion. On-Premises oder in der eigenen Cloud — die Prozessdaten bleiben dort, wo sie hingehören.

📚 Alles im Detail: **[docs.processcube.io](https://docs.processcube.io)**

---

## 🤖 Agent Runtime — KI-Agenten im Prozess

Die **[ProcessCube Agent Runtime](https://docs.processcube.io/agents)** (`@processcube-io/agents`) bringt eine CLI (`pc-runtime`), ein generisches Runtime-Image und darauf aufsetzende Agenten-Images auf Basis von [OpenClaw](https://openclaw.ai) mit.

Der Einstieg dauert etwa 15 Minuten: `docker compose up`, mit `pc-runtime setup` ein Backend aktivieren (Claude, Codex oder Hybrid) und den Agenten `main` direkt aus einem LowCode-Flow ansprechen. Die Anmeldung läuft über eine Subscription — **kein eigener KI-Provider-API-Key nötig**.

### [Agent Runtime](https://docs.processcube.io/agents/runtime)

Das generische Basis-Image mit genau einem Agenten (`main`). Ausgangspunkt für eigene Agenten.

### [Coding-Agenten](https://docs.processcube.io/agents/coding-agents)

Automatisiertes Coding über Pull Requests — für **GitHub und Azure DevOps**:

- Aus einer Aufgabenbeschreibung entsteht ein **Draft-PR**
- Ein Worker implementiert im eigenen **Git-Worktree**
- Ein **PR-Watcher** reagiert auf Review-Kommentare
- Der vorgeschaltete **`code-selector`** ordnet ein Ticket automatisch dem passenden Repository zu

Der Mensch bleibt am Merge-Button. Der Agent arbeitet, das Review entscheidet.

### [Support-Agent](https://docs.processcube.io/agents/support)

First-Level-Support per E-Mail, zyklisch getaktet: Der Agent sucht die Antwort in der Wissensbasis und legt sie **als Entwurf zur Freigabe** ab. Findet er nichts, eskaliert er in die Engine — als regulärer Prozess mit Zuständigkeit und Frist.

### Betrieb

- **[Docker](https://docs.processcube.io/agents/docker)** — drei Images: Runtime, Coding-Agenten, Support-Agent
- **[Kubernetes / k3s](https://docs.processcube.io/agents/kubernetes)** — Betrieb als StatefulSet mit initContainer-Registrierung (PoC)

> ⚠️ **Preview:** Die Agent Runtime steht aktuell bei `1.1.0-develop.x`. Schnittstellen, Image-Tags und Verhalten können sich bis zum ersten Stable-Release noch ändern.

📖 Wie das aus LowCode heraus aussieht, zeigt der Blogbeitrag [OpenClaw-Agenten aus ProcessCube® LowCode ansprechen](https://docs.processcube.io/blog/openclaw-lowcode) — konzeptionell dazu: [Agenten als External Task](https://docs.processcube.io/blog/agent-runtime-external-task).

---

## Plattform-Komponenten

| Komponente | Aufgabe |
|---|---|
| **[Engine](https://docs.processcube.io/engine)** | Speichert und führt BPMN-Prozessmodelle aus — inkl. MQTT, RabbitMQ, Azure Service Bus, Prometheus/Grafana |
| **[Studio](https://docs.processcube.io/studio)** | Modellieren, deployen, debuggen — erweiterbar über Extensions |
| **[Authority](https://docs.processcube.io/authority)** | Identity Provider mit Anbindung an ADFS, Entra ID, Google |
| **[Cuby](https://docs.processcube.io/cuby)** | Installation und Verwaltung der Plattform, Marketplace, Plugin-System |
| **[LowCode](https://docs.processcube.io/lowcode)** | Node-RED-Umgebung mit Engine-Nodes, UI-Widgets und OpenClaw-Nodes |
| **[Agent Runtime](https://docs.processcube.io/agents)** | KI-Agenten als External Task Worker |
| **[KnowledgeSDK](https://docs.processcube.io/knowledge-sdk)** | Wissensbasis mit Such- und Klassifikations-Pipeline, Ticket-Classifier, Wiki-Layer |
| **[CLI](https://docs.processcube.io/cli)** | `pc` für Deployment, Prozesssteuerung und CI/CD |
| **[AppSDK & AppTemplate](https://docs.processcube.io/app-sdk)** | Next.js/React-Grundlage für eigene Prozess-Anwendungen |
| **[Client Libraries](https://docs.processcube.io/clients)** | TypeScript, Python und .NET für External Tasks, User Tasks und Events |

---

## 🔌 MCP: Werkzeuge für Coding-Agenten

Prozessautomatisierung sollte auch aus dem Editor heraus funktionieren. Deshalb sprechen unsere Komponenten MCP:

- **[Engine MCP-Server](https://docs.processcube.io/engine/mcp)** — Prozesse auflisten, starten, inspizieren
- **[Studio MCP-Server](https://docs.processcube.io/studio/mcp-server)** (Preview) — BPMN-Diagramme lesen und erzeugen
- **[Docs MCP-Server](https://docs.processcube.io/docs-mcp-public)** — die Dokumentation als Werkzeug
- **[KnowledgeSDK MCP](https://docs.processcube.io/knowledge-sdk/mcp)** — Zugriff auf die Wissensbasis
- **[Entwickler-Skills](https://docs.processcube.io/agent-skills)** — vorgefertigte Skills für Coding-Agenten

---

## 📦 Produkte

| Produkt | Für wen |
|---|---|
| **[ProcessCube Lokal](https://docs.processcube.io/produkte/processcube-lokal)** | Erste Schritte auf dem eigenen Rechner |
| **[ProcessCube Docker](https://docs.processcube.io/produkte/processcube-docker)** | Compose-Setup für Team und Test |
| **[ProcessCube K8s](https://docs.processcube.io/produkte/processcube-k8s)** | Produktivbetrieb im Cluster |
| **[RemoteConnect / Cuby Connect](https://docs.processcube.io/produkte/processcube-remoteconnect)** | Verteilte Umgebungen anbinden |
| **[Ticketpilot](https://docs.processcube.io/produkte/ticketpilot)** | Support-Tickets, BPMN-Orchestrierung und KI-Unterstützung in einem Produkt |

---

## Typische Einsatzfelder

Dokumentenverarbeitung · Freigabe- und Genehmigungsketten · Onboarding · Servicemanagement & Ticketing · Auftrags- und Produktionsprozesse · Audit-Trails für Compliance-Anforderungen

Konkret zum Beispiel:

- Rechnungseingang: erfassen, prüfen, eskalieren, freigeben
- Ticket kommt rein → Agent recherchiert und schlägt eine Antwort vor → Mensch gibt frei
- Bugreport → `code-selector` findet das Repo → Coding-Agent legt einen Draft-PR an
- Genehmigungskette mit Fristen, Wiedervorlagen und Vertretungsregelung
- Systemübergreifende Integration per API, MQTT oder Service Bus

---

## Warum ProcessCube?

- **Standard statt Lock-in** — BPMN 2.0, keine proprietäre Prozesssprache
- **Selbst hostbar** — Docker, Kubernetes, eigene Infrastruktur, DSGVO-konform
- **LowCode *und* Code** — je nach Aufgabe und Team, nicht als Entweder-oder
- **Nachvollziehbar** — jeder Prozessschritt ist einsehbar und auditierbar
- **KI mit Leine** — Agenten mit klarem Auftrag, klarer Grenze und einem Menschen am Freigabe-Button
- **Kurze Wege** — kleines Team, direkter Kontakt, echte Antworten

---

## Repositories

| Repository | Inhalt |
|---|---|
| **ProcessCube.Deployment** | Deployment-Setups für Docker Compose und Kubernetes |
| **ProcessCube.Claude.Development.Marketplace** | Skills und Werkzeuge für KI-gestützte Entwicklung |
| **node-red-contrib-email-actions** | Node-RED-Nodes für E-Mail-Aktionen |
| **ticket-pilot.de** | Website zum Ticketpilot |

---

## Über die ProcessCube UG

Wir kommen aus der Praxis: BPMN-Workshops, Engine-Entwicklung, Automatisierung in echten Kundenumgebungen. Unser Anspruch ist, **Technik nahbar zu machen** — Prozesse so darzustellen, dass Fachbereich und Entwicklung dasselbe Bild vor Augen haben.

Und weil „done is better than perfect" gilt: lieber ein laufender Prozess heute als ein perfektes Konzept nächstes Jahr.

---

## Mitmachen

Issues, Pull Requests und Fragen sind willkommen — auch „das verstehe ich nicht" ist wertvolles Feedback.

- 🌐 [processcube.io](https://www.processcube.io)
- 📚 [docs.processcube.io](https://docs.processcube.io)
- 💬 [Support](https://www.processcube.io/support-1)

**Viel Spaß beim Stöbern!**
