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

