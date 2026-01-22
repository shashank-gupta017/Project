# Spring PetClinic Application

## Overview

The Spring PetClinic is a sample application designed to demonstrate Spring framework capabilities. It's a web-based application for managing a veterinary clinic, including:

- **Veterinarians**: Manage vet information and specialties
- **Pet Owners**: Track customer details and contact information
- **Pets**: Maintain pet records with types and birth dates
- **Visits**: Schedule and track veterinary visits with descriptions

This application showcases best practices in Spring development, including:
- Spring Boot for rapid application setup
- Spring MVC for web layer
- Spring Data JPA for data persistence
- Hibernate as the ORM framework
- HSQLDB as the embedded database (MySQL support available)
- Dandelion for datatables functionality
- JUnit, Mockito, and AssertJ for testing

## Technology Stack

- **Java**: 1.7
- **Framework**: Spring Boot, Spring MVC, Spring Data JPA
- **Build Tool**: Maven 3.x
- **Database**: HSQLDB (default), MySQL (configurable)
- **ORM**: Hibernate
- **Testing**: JUnit, Mockito, AssertJ, Spring Test
- **Code Coverage**: JaCoCo, Cobertura
- **Server**: Apache Tomcat 7
- **Packaging**: WAR file

## Prerequisites

Before building and running the application, ensure you have:

- Java Development Kit (JDK) 1.7 or higher
- Maven 3.x (or use the included Maven Wrapper)
- Apache Tomcat 7 or higher (for standalone deployment)
- Git (for version control)

## Building the Project

### Using Maven Wrapper (Recommended)

```bash
# On Unix/Linux/Mac
chmod +x mvnw
./mvnw clean install

# On Windows
mvnw.cmd clean install
```

### Using Local Maven Installation

```bash
mvn clean install
```

### Build Artifacts

After a successful build, you'll find:
- WAR file: `target/petclinic.war`
- Test reports: `target/surefire-reports/`
- Code coverage: `target/site/cobertura/`

## Running the Project

### Option 1: Using Tomcat Maven Plugin (Quick Start)

```bash
# Using Maven Wrapper
./mvnw tomcat7:run

# Using local Maven
mvn tomcat7:run
```

The application will start on: **http://localhost:9966/petclinic**

### Option 2: Deploy WAR to Tomcat Server

1. Build the project to generate the WAR file:
   ```bash
   ./mvnw clean package
   ```

2. Copy the WAR file to Tomcat's webapps directory:
   ```bash
   cp target/petclinic.war $TOMCAT_HOME/webapps/
   ```

3. Start Tomcat server:
   ```bash
   $TOMCAT_HOME/bin/startup.sh  # Unix/Linux/Mac
   $TOMCAT_HOME/bin/startup.bat  # Windows
   ```

4. Access the application at: **http://localhost:8080/petclinic**

### Option 3: Run with Specific Database

By default, the application uses HSQLDB. To use MySQL:

1. Uncomment the MySQL dependency in `pom.xml`
2. Configure database connection in `src/main/resources/spring/data-access.properties`
3. Rebuild and run the application

## Testing

### Run All Tests

```bash
./mvnw test
```

### Run Tests with Code Coverage

```bash
# Using Cobertura
./mvnw cobertura:cobertura

# View coverage report
open target/site/cobertura/index.html
```

### Run Specific Test Classes

```bash
./mvnw test -Dtest=YourTestClassName
```

## Deployment

### Production Deployment Checklist

1. **Update Configuration**:
   - Configure production database settings
   - Update logging levels in `logback.xml`
   - Review security configurations

2. **Build Production WAR**:
   ```bash
   ./mvnw clean package -DskipTests=false
   ```

3. **Deploy to Application Server**:
   - Deploy `target/petclinic.war` to Tomcat, JBoss, or any Java EE container
   - Ensure server has sufficient memory (recommended: -Xmx512m or higher)
   - Configure JDBC connection pool settings if using external database

4. **Verify Deployment**:
   - Check application logs for errors
   - Verify database connectivity
   - Test key functionality (view vets, owners, pets)

### CI/CD Integration

The project includes `.travis.yml` for continuous integration with Travis CI. The build process:
- Compiles the source code
- Runs all unit and integration tests
- Generates code coverage reports
- Packages the application as a WAR file

## Project Structure

```
├── src/
│   ├── main/
│   │   ├── java/                  # Java source files
│   │   ├── resources/             # Configuration files
│   │   └── webapp/                # Web resources (JSP, CSS, JS)
│   └── test/                      # Test files
├── gatling/                       # Performance test scenarios
├── pom.xml                        # Maven build configuration
├── sonar-project.properties       # SonarQube configuration
└── bower.json                     # Frontend dependencies

```

## Additional Commands

### Install Frontend Dependencies (Bower)

```bash
./mvnw install -Pbower-install
```

### Generate Eclipse Project

```bash
./mvnw eclipse:eclipse
```

### Clean Build Artifacts

```bash
./mvnw clean
```

## Troubleshooting

**Issue**: `Permission denied` when running `./mvnw`  
**Solution**: Make the wrapper executable: `chmod +x mvnw`

**Issue**: Port 9966 already in use  
**Solution**: Change the port in `pom.xml` (tomcat7-maven-plugin configuration) or stop the process using the port

**Issue**: Database connection errors  
**Solution**: Verify database configuration in `src/main/resources/spring/data-access.properties`

## License

This is a sample application for demonstration purposes.

## Support

For issues and questions, please refer to the Spring PetClinic community resources.