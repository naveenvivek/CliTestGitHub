# Copilot CLI Instructions

## Default Behavior

- Always validate each step before proceeding to the next
- Use conventional commit message format (feat:, fix:, docs:, etc.)
- Default Spring Boot version: 2.7.18
- Default Java version: 8
- Default server port: 8080

## Three-Step Workflow Pattern

When executing clone → build → PR workflow:

1. **Step 1: Clone Repository**
   - Verify repository URL and branch exist before cloning
   - Clone to specified directory
   - Confirm successful checkout

2. **Step 2: Spring Boot Application**
   - Create Maven project structure
   - Include spring-boot-starter-web dependency
   - Create at least one REST controller
   - Build with `mvn clean install`
   - Run with `mvn spring-boot:run`
   - Verify application starts successfully

3. **Step 3: Create Pull Request**
   - Only proceed if Step 2 succeeds
   - Commit with descriptive message
   - Push to origin branch
   - Create PR using GitHub CLI (gh)
   - Target branch: `main` (unless specified otherwise)

## Error Handling

- Stop workflow if any step fails
- Provide clear error messages
- Suggest remediation steps
- Never force-push or delete remote branches

## Code Quality

- Use RESTful conventions for endpoints
- Include proper package structure (com.example.*)
- Add meaningful endpoint names
- Keep controllers simple and focused
