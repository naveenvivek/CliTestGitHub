# Agent Instructions

## Project Context

This is a Spring Boot Maven project for demonstrating automated workflow patterns with GitHub Copilot CLI.

## Workflow Automation Rules

### Three-Step Automated Workflow

When user requests automated workflow (clone → build → PR):

1. **Clone & Checkout**
   - Accept: repository URL, branch name, target directory
   - Execute: `git clone -b <branch> <repo-url> <directory>`
   - Validate: branch exists, clone successful
   - Stop if fails

2. **Build & Run Spring Boot Application**
   - Generate: pom.xml, src structure, Application class, Controller
   - Build: `mvn clean install`
   - Run: `mvn spring-boot:run` (async mode)
   - Test: verify application starts, endpoint responds
   - Stop application after verification
   - Stop if fails

3. **Commit & Create PR**
   - Stage: `git add .`
   - Commit: use conventional commit format
   - Push: `git push origin <branch>`
   - PR: use GitHub CLI `gh pr create`
   - Return: PR URL to user

## Spring Boot Standards

- **Java Version**: 8
- **Spring Boot Version**: 2.7.18
- **Port**: 8080 (default)
- **Base Package**: com.example.demo
- **Controller Pattern**: REST endpoints under `/api/*`
- **Dependencies**: spring-boot-starter-web (minimum)

## Git & GitHub Standards

- **Commit Format**: `<type>: <description>` (conventional commits)
  - Types: feat, fix, docs, chore, refactor, test
- **Branch Naming**: feature/*, bugfix/*, hotfix/*
- **PR Target**: main (unless specified)
- **PR Title**: Match commit message format
- **PR Body**: Include summary of changes

## Development Practices

- Always run `mvn clean install` before running application
- Check for port conflicts before starting Spring Boot app
- Use async mode for long-running processes (mvn spring-boot:run)
- Verify application health before proceeding to PR
- Never commit without testing build first

## Error Recovery

- If Maven build fails: show error, suggest fix, ask user
- If port in use: suggest stopping process or changing port
- If git push fails: check remote exists, verify authentication
- If PR creation fails: verify gh CLI auth, check branch protection

## Security & Safety

- Never commit secrets or credentials
- Always preview changes before committing
- Require user approval for destructive operations
- Don't force-push to remote branches
- Don't delete files without explicit confirmation

## Behavioral Guidelines

- Be concise and action-oriented
- Show progress for long operations
- Validate each step before proceeding
- Stop workflow on any failure
- Provide clear success/failure messages
- Include relevant URLs (repo, PR) in output
