# VetCare Web

A full-stack veterinary clinic management system developed as a practical assignment for the **Sistemas de Base de Dados** course at **ISEL – Instituto Superior de Engenharia de Lisboa**.

The system manages appointments, clinical records, genealogical trees, and user authentication across multiple clinic locations (Lisboa, Porto, Évora), with role-based access for four user types: **Tutor**, **Receptionist**, **Veterinarian**, and **Manager**.

---

## Tech Stack

| Layer | Technology |
|---|---|
| Backend | Java 17 (OpenJDK), Jakarta Servlets 6.0, JSP 3.0 |
| Database | MySQL 8.0 via JDBC (mysql-connector-j 9.5.0) |
| Server | Apache Tomcat 10.1.x |
| Frontend | HTML5, CSS3, JavaScript (ES6+) |
| IDE | Eclipse IDE for Enterprise Java and Web Developers 2025-12 |
| Data Formats | JSON, XML (export/import of clinical records) |

---

## Project Structure

The repository is organized as follows:

```
VetCare_DataBase_System/
├── webapp/
│   └── VetCareWeb.war          ← Deployable WAR file (import this into Eclipse)
└── database/
    └── vetdataabase.sql        ← Creates schema, tables, views, triggers, procedures and inserts sample data

```

After importing the WAR file into Eclipse, the project will have the following structure:

```
VetCareWeb/
├── Deployment Descriptor: VetCareWeb
├── JAX-WS Web Services
├── Java Resources
├── build/
└── src/
    └── main/
        ├── java/               ← All backend Java code
        │   ├── dao/            ← Data Access Objects (DB queries)
        │   │   └── DBConnection.java  ← Database connection config
        │   ├── model/          ← Java model/entity classes
        │   └── servlets/       ← Servlet controllers
        └── webapp/
            ├── css/            ← Stylesheets
            ├── gerente/        ← JSP pages for Manager role
            ├── rececionista/   ← JSP pages for Receptionist role
            ├── tutor/          ← JSP pages for Tutor role
            ├── veterinario/    ← JSP pages for Veterinarian role
            ├── login.jsp       ← Login page for clinic staff
            └── loginCliente.jsp← Login page for animal tutors
```

---

## Prerequisites

Before running the project, make sure you have the following installed:

- [Java JDK 17](https://adoptium.net/)
- [Apache Tomcat 10.1.x](https://tomcat.apache.org/download-10.cgi)
- [MySQL 8.0](https://dev.mysql.com/downloads/mysql/)
- [MySQL Workbench](https://dev.mysql.com/downloads/workbench/) *(optional but recommended)*
- [Eclipse IDE for Enterprise Java and Web Developers](https://www.eclipse.org/downloads/packages/) *(2025-12 or later)*

---
## Technologies
- Java
- JSP / Servlets
- MySQL
- JDBC
- HTML
- CSS
- JavaScript
- Apache Tomcat
- JSON / XML
 
## Database Setup

> **MySQL must be running while the application is running.** The app connects to the database on every request, so if MySQL is stopped the application will fail.

1. Open **MySQL Workbench** and connect to your local MySQL instance.
2. Run the SQL scripts from the `database/` folder in this order:
   - `create.sql` — creates the schema, tables, views, triggers, and procedures
   - `populate.sql` — inserts sample data

### Configuring the Database Connection

The database credentials are defined in:

```
src/main/java/dao/DBConnection.java
```

Open that file and check the following variables:

```java
private static final String USER = "root";
private static final String PASS = "root";
```

> If your local MySQL password is different from `root`, update the `PASS` variable to match your own password before running the application. If you leave it as `root` and your password is different, the app will fail to connect to the database.

---

## Importing and Running the WAR File in Eclipse

### Step 1 – Configure Tomcat in Eclipse

1. Open Eclipse and go to **Window → Preferences → Server → Runtime Environments**.
2. Click **Add**, select **Apache Tomcat v10.1**, and point it to your Tomcat installation directory.
3. Click **Finish**.

### Step 2 – Import the WAR File

1. Go to **File → Import → Web → WAR File**.
2. Click **Browse** and select the `VetCareWeb.war` file.
3. Make sure **Target Runtime** is set to **Apache Tomcat v10.1**.
4. Click **Finish** — Eclipse will unpack the WAR and create the project.

### Step 3 – Add the MySQL JDBC Driver

If the driver is not already included in the WAR:

1. Download [mysql-connector-j 9.5.0](https://dev.mysql.com/downloads/connector/j/).
2. Copy the `.jar` file to `src/main/webapp/WEB-INF/lib/`.
3. Right-click the project → **Build Path → Configure Build Path → Libraries → Add JARs**.

### Step 4 – Deploy and Run

1. Right-click the project → **Run As → Run on Server**.
2. Select your Tomcat 10.1 server instance and click **Finish**.
3. Eclipse will deploy the application and open it in the internal browser, or navigate manually to:

```
http://localhost:8080/VetCareWeb/
```

---

## Test Credentials

### Staff Login — `http://localhost:8080/VetCareWeb/login.jsp`

| Role | NIF / ID |
|---|---|
| Receptionist | `1001` |
| Manager | `999999999` |
| Veterinarian | `111111111` |

> Staff accounts do not require a password in the current demo configuration.

### Tutor Login — `http://localhost:8080/VetCareWeb/loginCliente.jsp`

| NIF | Password |
|---|---|
| `123456789` | `MinhaPassword123` |

> Tutor passwords are stored as SHA-256 hashes in the database.

---

## Key Features

- **Automatic vet assignment** via database trigger — selects the best available vet based on specialty, location, and schedule
- **Dynamic schedule loading** — available time slots update in real time using async JavaScript fetch requests
- **Clinical record management** — full history of consultations, diagnoses, medications, and responsible vets
- **Genealogical tree** — recursive SQL queries to display multi-generation ancestry
- **Export / Import** of clinical records in JSON and XML formats (including Base64-encoded photos)
- **SQL Injection protection** via PreparedStatements and server-side type validation
- **Password security** with SHA-256 hashing — plain text passwords are never stored
- **Automatic holiday generation** via stored procedure `GerarFeriadosAno(year)`
- **Age and life-stage calculation** — automatically derived from birth date, per species

---

## Author

| Name | Student Number |
|---|---|
| João Póvoa | 51392 |


**Course:** Sistemas de Base de Dados  
**Supervisor:** Prof. Porfírio Filipe  
**Institution:** ISEL – Instituto Superior de Engenharia de Lisboa  
**Date:** January 2026
