# Secure Configuration for `gradle.properties`

This project recommends not storing sensitive information such as passwords or tokens directly in the file `gradle.properties`.  

Instead, safer methods such as environment variables or separate, unversioned configuration files should be used.

---

##Methods for Securing Sensitive Data

### 1. Using Environment Variables

#### Step 1: Defining the Environment Variable

- **Linux/macOS:** 
  ```bash
  export ARTIFACTORY_USER=YOURUSER
  export ARTIFACTORY_PASSWORD=YOURPASSWORD
  ```
  To make the variable permanent, add this line to your `~/.bashrc`, `~/.zshrc`, or `~/.bash_profile`.

- **Windows:**
  - Open the Environment Variables section in the Control Panel.
  - Create a new user or system variables:
    - **Name:** `ARTIFACTORY_USER`
    - **Value:** `YOURUSER`
    - **Name:** `ARTIFACTORY_PASSWORD`
    - **Value:** `YOURPASSWORD`

#### Step 2: Edit `gradle.properties`
Replace sensitive values references to the environment variables:

```properties
artifactory_url=https://jfrog.devstack.vwgroup.com/artifactory
artifactory_user=${ARTIFACTORY_USER}
artifactory_password=${ARTIFACTORY_PASSWORD}
configuration_location=
server_port=
profile=local
```

#### Step 3: Make sure the environment variable is set

Make sure the environment variable is available before starting your build system.

For example, go to the projects folder of an appropriate repository and try:
```
devstack_eecost|event-transformer-backend $ gradle clean codegen assemble          

BUILD SUCCESSFUL in 6s
8 actionable tasks: 8 executed
```

---

### 2. **Use of password management tools**
Tools like **HashiCorp Vault**, **AWS Secrets Manager**, or **Azure Key Vault** enable secure storage and retrieval of passwords at runtime. 
Integration requires adjustments to the build or runtime process but provides the highest level of security.

---

## recommendation
Using **environment variables** is often the simplest and most cross-platform approach. Regardless of the chosen method, it is important to:
- Never include sensitive data in version control.
- Regularly review the project's security configuration.
- Rotate credentials in the event of a potential security incident.

# Secure Configuration for `gradle.properties`


---

---


In diesem Projekt wird empfohlen, sensible Informationen wie Passwörter oder Tokens nicht direkt in der `gradle.properties`-Datei zu speichern. 

Stattdessen sollten sicherere Methoden wie Umgebungsvariablen oder separate, nicht versionierte Konfigurationsdateien verwendet werden.


## Methoden zur Sicherung sensibler Daten

### 1. **Verwendung von Umgebungsvariablen**

#### Schritt 1: Definieren der Umgebungsvariable

- **Linux/macOS:** 
  ```bash
  export ARTIFACTORY_PASSWORD=dein_passwort
  ```
  Um die Variable dauerhaft zu setzen, füge diese Zeile in deine `~/.bashrc`, `~/.zshrc` oder `~/.bash_profile` ein.

- **Windows:**
  - Öffne die "Umgebungsvariablen" im Systemsteuerungsbereich.
  - Erstelle neue Benutzer- oder Systemvariablen:
    - **Name:** `ARTIFACTORY_USER`
    - **Wert:** `YOURUSER`
    - **Name:** `ARTIFACTORY_PASSWORD`
    - **Wert:** `YOURPASSWORD`

#### Schritt 2: Anpassen der `gradle.properties`
Ersetze sensible Werte durch Referenzen auf die Umgebungsvariablen:
```properties
artifactory_url=https://jfrog.devstack.vwgroup.com/artifactory
artifactory_user=${ARTIFACTORY_USER}
artifactory_password=${ARTIFACTORY_PASSWORD}
configuration_location=
server_port=
profile=local
```

#### Schritt 3: Sicherstellen, dass die Umgebungsvariable gesetzt ist

Stelle sicher, dass die Umgebungsvariable vor dem Start deines Build-Systems verfügbar ist.

zum Beispiel in ein Verzeichnis eines passenden Repository wechseln und testen:
```
devstack_eecost|event-transformer-backend $ gradle clean codegen assemble          

BUILD SUCCESSFUL in 6s
8 actionable tasks: 8 executed
```

---

### 2. **Verwendung von Passwort-Management-Tools**
Tools wie **HashiCorp Vault**, **AWS Secrets Manager** oder **Azure Key Vault** ermöglichen die sichere Speicherung und Abfrage von Passwörtern zur Laufzeit. 
Die Integration erfordert Anpassungen am Build- oder Laufzeitprozess, bietet jedoch höchste Sicherheit.

---

## Empfehlung
Die Verwendung von **Umgebungsvariablen** ist oft der einfachste und plattformübergreifendste Ansatz. Unabhängig von der gewählten Methode ist es wichtig:
- Sensible Daten niemals in die Versionskontrolle aufzunehmen.
- Regelmäßig die Sicherheitskonfiguration des Projekts zu überprüfen.
- Zugangsdaten zu rotieren, wenn ein potenzieller Sicherheitsvorfall auftritt.

