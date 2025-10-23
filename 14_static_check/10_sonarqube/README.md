# SonarQube

SonarQube is an open-source platform for continuous inspection of code quality. It performs static code analysis to detect bugs, vulnerabilities, and code smells, and provides detailed reports to improve code quality.

## Key Features
- **Static Analysis**: Detects bugs, security vulnerabilities, and code smells.
- **Multi-Language Support**: Supports over 25 programming languages, including C and C++.
- **Quality Gates**: Enforces coding standards and quality thresholds.
- **Integration**: Works with popular CI/CD tools like Jenkins, GitHub Actions, and GitLab CI.
- **Extensibility**: Allows custom rules and plugins.

## Installation
SonarQube requires Java and a database (e.g., PostgreSQL) to run. Follow these steps to install it:

### 1. **Download and Install SonarQube**
1. Download SonarQube from the [official website](https://www.sonarqube.org/downloads/).
2. Extract the archive:
   ```bash
   tar -xvf sonarqube-<version>.zip
   ```
3. Navigate to the SonarQube directory:
   ```bash
   cd sonarqube-<version>
   ```
4. Start the SonarQube server:
   ```bash
   ./bin/<os>/sonar.sh start
   ```

### 2. **Access the Web Interface**
Open your browser and navigate to `http://localhost:9000`. Log in with the default credentials:
- Username: `admin`
- Password: `admin`

### 3. **Configure the Database**
Edit the `sonar.properties` file to configure the database connection.

## Usage

### Analyzing a C Project
1. Install the SonarScanner:
   ```bash
   brew install sonar-scanner  # On macOS
   sudo apt-get install sonar-scanner  # On Linux
   ```
2. Navigate to your project directory.
3. Create a `sonar-project.properties` file:
   ```properties
   sonar.projectKey=my_project
   sonar.sources=.
   sonar.host.url=http://localhost:9000
   sonar.login=<your_token>
   ```
4. Run the scanner:
   ```bash
   sonar-scanner
   ```

### Example `sonar-project.properties`
```properties
sonar.projectKey=my_c_project
sonar.projectName=My C Project
sonar.sources=src
sonar.language=c
sonar.host.url=http://localhost:9000
sonar.login=<your_token>
```

## Integration with CI/CD
SonarQube integrates with Jenkins, GitHub Actions, GitLab CI, and other CI/CD tools. Use the SonarScanner CLI or plugins to automate analysis in your pipeline.

## Best Practices
- Run SonarQube regularly to maintain code quality.
- Use Quality Gates to enforce coding standards.
- Address issues promptly to prevent technical debt.
- Combine SonarQube with other tools like Valgrind and Coverity for comprehensive analysis.

## Additional Resources
- [SonarQube Documentation](https://docs.sonarqube.org/)
- [SonarScanner CLI](https://docs.sonarqube.org/latest/analysis/scan/sonarscanner/)
- [SonarQube Community](https://community.sonarsource.com/)