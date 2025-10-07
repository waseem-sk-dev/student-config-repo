# 🧩 Student Config Server

[![Spring Boot](https://img.shields.io/badge/Spring%20Boot-3.x-brightgreen)](https://spring.io/projects/spring-boot)
[![Spring Cloud](https://img.shields.io/badge/Spring%20Cloud-2023.x-blue)](https://spring.io/projects/spring-cloud)
[![Java](https://img.shields.io/badge/Java-17%2B-orange)](https://openjdk.org/)

The **Student Config Server** is the **centralized configuration service** for the Student Microservices architecture.  
It manages external configuration for all microservices from a single Git-based source, enabling consistency and flexibility across environments.

---

## 🧠 Purpose

In a distributed system, maintaining configurations for multiple microservices can be challenging.  
This service provides a **central source of truth** for configuration data used by:

- 🏦 `student-api-gateway`  
- 🧭 `student-eureka-server`  
- 🎓 `student-course-service`  
- 👨‍🎓 `student-service`

---

## 🏗️ Architecture Overview

- **student-config-server**  
  - Port: 8888

- **Other Microservices**  
  - Fetch their configs from Config Server



---

## ⚙️ Tech Stack

| Technology | Purpose |
|-------------|----------|
| **Java 17+** | Programming language |
| **Spring Boot** | Application framework |
| **Spring Cloud Config Server** | Externalized configuration management |
| **Git / GitHub** | Configuration repository |
| **Maven** | Dependency management and build tool |

---

## 🧩 Configuration Repository

Create a separate GitHub repository (e.g., `student-config-repo`) to store configuration files for all environments.

**Example structure:**

- `student-config-repo/`
  - `student-api-gateway-dev.properties`
  - `student-eureka-server-dev.properties`
  - `student-course-service-dev.properties`
  - `student-service-dev.properties`



Each file holds configuration for its respective service and environment.

---

## 🧠 Example `application.properties`

> ```properties
> server.port=8888
> spring.application.name=student-config-server
>
> # Your config Git repository
> spring.cloud.config.server.git.uri=https://github.com/YOUR_GITHUB_USERNAME/student-config-repo
> spring.cloud.config.server.git.clone-on-start=true
> ```

---

## 🚀 Running the Application

> **Using Maven**
> ```bash
> mvn clean install
> mvn spring-boot:run
> ```
> The server will start on **port 8888**.

---

## 🔍 Testing the Configuration Endpoint

> Once the Config Server is running, verify it by accessing:  
> `http://localhost:8888/student-service/dev`
>
> You should see a JSON response containing configuration details:
>
> ```json
> {
>   "name": "student-service",
>   "profiles": ["dev"],
>   "propertySources": [
>     {
>       "name": "https://github.com/YOUR_GITHUB_USERNAME/student-config-repo/student-service-dev.properties",
>       "source": {
>         "server.port": "8082",
>         "spring.datasource.url": "jdbc:mysql://localhost:3306/student_db"
>       }
>     }
>   ]
> }
> ```

---

## 📦 Project Structure

> ```
> student-config-server/
> ├── src/
> │   ├── main/
> │   │   ├── java/com/student/configserver
> │   │   │   └── StudentConfigServerApplication.java
> │   │   └── resources/
> │   │       └── application.properties
> │   └── test/
> ├── pom.xml
> └── README.md
> ```

---

## 🤝 Contributing

> Contributions are welcome!  
> If you’d like to improve configuration management, add documentation, or extend environments, feel free to open a PR.

---

## 👨‍💻 Author

> **Waseem Shaikh**  
> Backend Developer – Java | Spring Boot | Microservices  
> GitHub: [@waseem-sk-dev](https://github.com/waseem-sk-dev)

---

## 🪪 License

> This project is licensed under the **MIT License** – see the LICENSE file for details.
