# Coordinator Nodes im ELK-Stack

Ein **Coordinator Node** in einem ELK-Stack (Elasticsearch, Logstash, Kibana) ist ein spezieller Knoten in Elasticsearch, der als Vermittler für Such- und Indexierungsanfragen dient. Seine Hauptaufgabe besteht darin, Anfragen zu koordinieren, ohne selbst Daten zu speichern oder zu verarbeiten. Nachfolgend werden die Aufgaben und Einsatzszenarien eines Coordinator Nodes detailliert beschrieben.

## Hauptaufgaben

### 1. **Anfragen verarbeiten und verteilen**
- Der Coordinator Node empfängt **Suchanfragen** und **Schreibanfragen** von Clients.
- Er analysiert die Anfrage, teilt sie in kleinere Aufgaben auf und leitet diese an die entsprechenden Datenknoten (Data Nodes) weiter, die die eigentlichen Daten speichern.

### 2. **Aggregation von Ergebnissen**
- Bei **Suchanfragen** sammelt der Coordinator Node die Teilergebnisse von verschiedenen Datenknoten ein und aggregiert diese zu einem Gesamtergebnis, das an den Client zurückgegeben wird.

### 3. **Ressourcenoptimierung**
- Coordinator Nodes führen keine eigene Last für Speicherung oder Verarbeitung aus, was bedeutet, dass sie ausschließlich für die Verteilung und Koordinierung von Anfragen genutzt werden. Dadurch wird der Cluster entlastet und Anfragen können schneller bearbeitet werden.

### 4. **Load Balancing**
- Sie verteilen Anfragen gleichmäßig über den gesamten Cluster und verhindern so, dass einzelne Datenknoten überlastet werden.

### 5. **Keine Datenhaltung**
- Coordinator Nodes haben keine eigenen Shards und speichern keine Daten. Dadurch können sie sich auf die Verarbeitung von Anfragen und die Koordination konzentrieren.

## Typische Einsatzszenarien

- **Große Cluster**: In großen Elasticsearch-Clustern mit vielen Datenknoten helfen Coordinator Nodes dabei, die Last effizient zu verteilen.
- **Optimierung von Suchanfragen**: Sie verbessern die Antwortzeiten bei komplexen Suchanfragen durch die Aggregation und Koordination von Ergebnissen.
- **Entkopplung von Funktionen**: Sie entlasten die Datenknoten, die sich dann auf Datenverarbeitung und Speicherung konzentrieren können.

## Konfiguration eines Coordinator Nodes

Ein Coordinator Node wird durch die Konfiguration festgelegt, indem alle Rollen außer der Koordinationsrolle deaktiviert werden. In der Datei `elasticsearch.yml` könnte dies wie folgt aussehen:

```yaml
node.master: false
node.data: false
node.ingest: false
```

Der Knoten fungiert dann ausschließlich als Coordinator Node.
