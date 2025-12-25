# Automated Workflow: Clone → Build → Deploy → PR

This document outlines a three-step automated workflow process for GitHub Copilot CLI.

## Workflow Overview

### Step 1: Clone Repository & Branch
**Inputs Required:**
- Repository URL (e.g., `https://github.com/user/repo.git`)
- Branch name (e.g., `feature/new-feature`)
- Target directory

**Actions:**
```bash
git clone -b <branch-name> <repository-url> <target-directory>
cd <target-directory>
```

**Validation:**
- Verify git clone successful
- Confirm branch checkout
- Display current branch and repository info

---

### Step 2: Create & Run Spring Boot Application
**Actions:**
1. Generate Spring Boot Maven project structure
   - Create `pom.xml` with dependencies
   - Create standard Maven directory structure
   - Create main application class
   - Create REST controller with endpoint

2. Build the application
   ```bash
   mvn clean install
   ```

3. Run application locally
   ```bash
   mvn spring-boot:run
   ```

4. Verify application health
   - Check if application started successfully
   - Test endpoint (e.g., `curl http://localhost:8080/api/hello`)
   - Verify logs for errors

**Validation:**
- Maven build succeeds (exit code 0)
- Application starts without errors
- Endpoint returns expected response
- No port conflicts

---

### Step 3: Create Merge Request (Pull Request)
**Actions:**
1. Stage all changes
   ```bash
   git add .
   ```

2. Commit with descriptive message
   ```bash
   git commit -m "feat: Add Spring Boot application with REST controller"
   ```

3. Push to remote branch
   ```bash
   git push origin <branch-name>
   ```

4. Create pull request using GitHub CLI
   ```bash
   gh pr create --title "feat: Add Spring Boot application" \
                --body "Automated PR: Spring Boot app with REST endpoint" \
                --base main \
                --head <branch-name>
   ```

**Validation:**
- All files committed successfully
- Push successful to remote
- PR created with valid URL
- PR link returned to user

---

## Usage Example

**Command to Copilot CLI:**
```
Execute the automated workflow:
1. Clone branch 'feature/spring-app' from https://github.com/myuser/myrepo.git to D:\Projects\NewApp
2. Create a Spring Boot application with a REST controller at /api/status
3. If successful, commit and raise a PR to main branch
```

---

## Error Handling

### Step 1 Failures:
- Repository not found → Verify URL and access permissions
- Branch doesn't exist → Create branch or verify name
- Directory already exists → Use different directory or clean existing

### Step 2 Failures:
- Build fails → Check Java/Maven versions, review errors
- Port already in use → Stop conflicting process or use different port
- Runtime errors → Review application logs, check dependencies

### Step 3 Failures:
- No changes to commit → Verify files were created/modified
- Push rejected → Check branch permissions, pull latest changes
- PR creation fails → Verify GitHub CLI auth, check branch policies

---

## Environment Prerequisites

✅ **Required:**
- Git installed and configured
- Java 17+ installed
- Maven 3.6+ installed
- GitHub CLI (gh) installed and authenticated
- Active GitHub Copilot subscription

✅ **Recommended:**
- PowerShell 7+ (Windows)
- curl or similar tool for endpoint testing
- Sufficient disk space for dependencies

---

## Customization Options

You can customize this workflow by:
- Modifying the Spring Boot version in `pom.xml`
- Adding additional controllers or services
- Changing the base branch for PR (default: `main`)
- Adding custom commit message templates
- Including tests in the build process
- Adding code quality checks before PR creation

---

## Notes

- Each step is dependent on the previous step's success
- The workflow stops if any step fails
- Application runs in async mode during validation
- PR is only created if application successfully runs
- All actions preview before execution for approval
