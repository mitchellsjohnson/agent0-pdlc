# Application Skills

This folder contains application-specific AI skills.

---

## What Are Application Skills?

Skills that are specific to this application and wouldn't apply to other applications in your organization.

---

## When to Create an App Skill

Create an app skill when:
- The skill is specific to this codebase
- The skill uses app-specific patterns or tools
- The skill wouldn't be useful to other apps

**If the skill could apply to multiple apps, put it in the organization repo instead.**

---

## Skill Structure

Each skill should be a Markdown file:

```markdown
# Skill: <Skill Name>

## Purpose
<What this skill does>

## When to Use
<Trigger conditions>

## Instructions
<Step-by-step for the agent>

## Examples
<Example usage>
```

---

## Example App Skills

### Codebase-Specific Pattern

```markdown
# Skill: API Endpoint Pattern

## Purpose
Create new API endpoints following this app's patterns.

## When to Use
When creating new REST endpoints.

## Instructions
1. Create resource class in `src/api/resources/`
2. Follow naming: `{Entity}Resource.java`
3. Use existing patterns from `UserResource.java`
4. Add to routing in `ApiRoutes.java`
5. Create corresponding DTO in `src/api/dto/`

## Examples
See `src/api/resources/UserResource.java` for reference.
```

### Build-Specific Skill

```markdown
# Skill: Debug Mode

## Purpose
Run the application in debug mode for development.

## When to Use
When debugging issues or developing new features.

## Instructions
1. Kill any running instances: `killall -9 java`
2. Start with debug: `./mvnw -Prun -Ddebug`
3. Access at: http://localhost:8081/?debug
4. Attach debugger to port 5005

## Examples
./mvnw -Prun -Ddebug > /tmp/app.log 2>&1 &
```

---

## Adding a New Skill

1. Create `<skill-name>.md` in this folder
2. Follow the structure above
3. Reference in agent prompts if needed
4. Commit with your code changes
