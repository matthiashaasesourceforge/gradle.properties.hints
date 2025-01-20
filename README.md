# Secure Configuration for `gradle.properties`

This project recommends not storing sensitive information such as passwords or tokens directly in the file `gradle.properties`.  

Instead, safer methods such as environment variables or separate, unversioned configuration files should be used.

---

##Methods for Securing Sensitive Data

### 1. Using Environment Variables

#### Step 1: Defining the Environment Variable

- **Linux/macOS:** 
  ```bash
  export ARTIFACTORY_PASSWORD=YOURPASSWORD
  ```
  To make the variable permanent, add this line to your `~/.bashrc`, `~/.zshrc`, or `~/.bash_profile`.

- **Windows:**
  - Open the Environment Variables section in the Control Panel.
  - Create a new user or system variable:
    - **Name:** `ARTIFACTORY_PASSWORD`
    - **Wert:** `YOURPASSWORD`

#### Step 2: Edit `gradle.properties`
Replace sensitive values references to the environment variables:

```properties
artifactory_url=https://jfrog.devstack.vwgroup.com/artifactory
artifactory_user=YOURUSERID
artifactory_password=${ARTIFACTORY_PASSWORD}
configuration_location=
server_port=
profile=local
```

#### Step 3: Make sure the environment variable is set

Make sure the environment variable is available before starting your build system.

---

### 2. **Using a separate file**

#### Step 1: Create a separate file
Create a file `secrets.properties` containing the sensitive information: 
```properties
artifactory_password=YOURPASSWORD
```

#### Step 2: Edit `gradle.properties`
Include separate file in `gradle.properties`:
```properties
artifactory_url=https://jfrog.devstack.vwgroup.com/artifactory
artifactory_user=YOURUSERID
configuration_location=
server_port=
profile=local

# load the password from separate file
include file:secrets.properties
```

#### Step 3: Exclusion from version control
Add the file `secrets.properties` to the .gitignore to exclude it from version control.
```plaintext
secrets.properties
```

---

### 3. **Use of password management tools**
Tools like **HashiCorp Vault**, **AWS Secrets Manager**, or **Azure Key Vault** enable secure storage and retrieval of passwords at runtime. Integration requires adjustments to the build or runtime process but provides the highest level of security.

---

## recommendation
Using **environment variables** is often the simplest and most cross-platform approach. Regardless of the chosen method, it is important to:
- Never include sensitive data in version control.
- Regularly review the project's security configuration.
- Rotate credentials in the event of a potential security incident.

# Secure Configuration for `gradle.properties`

---

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
  - Erstelle eine neue Benutzer- oder Systemvariable:
    - **Name:** `ARTIFACTORY_PASSWORD`
    - **Wert:** `YOURPASSWORD`

#### Schritt 2: Anpassen der `gradle.properties`
Ersetze sensible Werte durch Referenzen auf die Umgebungsvariablen:
```properties
artifactory_url=https://jfrog.devstack.vwgroup.com/artifactory
artifactory_user=YOURUSERID
artifactory_password=${ARTIFACTORY_PASSWORD}
configuration_location=
server_port=
profile=local
```

#### Schritt 3: Sicherstellen, dass die Umgebungsvariable gesetzt ist

Stelle sicher, dass die Umgebungsvariable vor dem Start deines Build-Systems verfügbar ist.

---

### 2. **Verwendung einer separaten Datei**

#### Schritt 1: Erstellen einer separaten Datei
Lege eine Datei `secrets.properties` an, die die sensiblen Informationen enthält:
```properties
artifactory_password=dein_passwort
```

#### Schritt 2: Anpassen der `gradle.properties`
Binde die separate Datei in `gradle.properties` ein:
```properties
artifactory_url=https://jfrog.devstack.vwgroup.com/artifactory
artifactory_user=YOURUSERID
configuration_location=
server_port=
profile=local

# Lade das Passwort aus einer separaten Datei
include file:secrets.properties
```

#### Schritt 3: Ausschluss aus der Versionskontrolle
Füge die Datei `secrets.properties` zur `.gitignore` hinzu, um sie nicht in die Versionskontrolle aufzunehmen:
```plaintext
secrets.properties
```

---

### 3. **Verwendung von Passwort-Management-Tools**
Tools wie **HashiCorp Vault**, **AWS Secrets Manager** oder **Azure Key Vault** ermöglichen die sichere Speicherung und Abfrage von Passwörtern zur Laufzeit. Die Integration erfordert Anpassungen am Build- oder Laufzeitprozess, bietet jedoch höchste Sicherheit.

---

## Empfehlung
Die Verwendung von **Umgebungsvariablen** ist oft der einfachste und plattformübergreifendste Ansatz. Unabhängig von der gewählten Methode ist es wichtig:
- Sensible Daten niemals in die Versionskontrolle aufzunehmen.
- Regelmäßig die Sicherheitskonfiguration des Projekts zu überprüfen.
- Zugangsdaten zu rotieren, wenn ein potenzieller Sicherheitsvorfall auftritt.

