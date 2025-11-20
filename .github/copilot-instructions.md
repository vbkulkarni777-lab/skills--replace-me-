# Copilot Instructions for GitHub Skills Exercise Template

## Project Overview

This is a **GitHub Skills exercise template** repository that serves as a boilerplate for creating interactive, GitHub-hosted learning exercises. It's not a typical software project—it's a template for educators to customize and deploy learning experiences.

## Key Architecture

### Repository Structure
- **`README.md`**: Landing page with placeholder content (replace: exercise title, description, prerequisites, learning objectives)
- **`.github/steps/`**: Exercise content files (1-step.md, 2-step.md, 3-step.md, x-review.md) that learners progress through
- **`.github/workflows/`**: GitHub Actions automation that manages the exercise lifecycle and learner progression

### Content Flow
Each step file follows a consistent pattern:
```markdown
## Step N: [Title]
[Optional scenario/story]

### 📖 Theory: [Title]
[Background knowledge or concept explanation]

### ⌨️ Activity: [Title]
1. [Instruction 1]
2. [Instruction 2]
...

<details>
<summary>Having trouble? 🤷</summary>
- [Troubleshooting hint]
</details>
```

## Critical Workflows & Commands

### Exercise Deployment (Automated)
- **Trigger**: Repository setup + initial push to `main` branch
- **Process**: GitHub Actions workflows in `.github/workflows/` automatically:
  1. Create an issue for learner interaction (0-start-exercise.yml)
  2. Post step content sequentially as learners progress
  3. Validate learner submissions against step requirements

**Key workflows**:
- `0-start-exercise.yml`: Initializes the exercise, creates the first issue
- `1-step.yml`, `2-step.yml`, `3-last-step.yml`: Step progression triggers
- Each workflow validates completion criteria and posts the next step

### No Local Build/Test
This template doesn't have a build process. Changes are validated via:
- Content structure compliance (proper markdown formatting in steps)
- Workflow YAML syntax
- Template variable replacement consistency

## Project-Specific Conventions

### Placeholder Replacement Pattern
All customizable content uses `(replace-me: description)` markers. When customizing:
- **README.md**: Replace exercise title, description, prerequisites, time estimate, learning objectives
- **Step files**: Replace activity instructions, theory content, troubleshooting tips
- **Workflow files**: Update exercise title and intro message in workflow env vars

Example: `"(replace-me: Exercise title)"` becomes `"Introduction to Git Basics"`

### File Naming Conventions
- Step files: Sequential (`1-step.md`, `2-step.md`, `3-step.md`)
- Review file: Always `x-review.md` (final step)
- Workflows: Correspond to step numbers (`1-step.yml` for step 1)
- Keep this 1-to-1 mapping between step files and workflows

### Markdown Structure in Steps
- Use GitHub-flavored markdown with notification blocks for emphasis:
  ```markdown
  > [!NOTE]
  > Important information
  > [!WARNING]
  > Alert content
  > [!TIP]
  > Helpful hint
  ```
- Always include `<details>` with troubleshooting section
- Maintain consistent emoji usage (📖 for theory, ⌨️ for activity)

## Integration Points & External Dependencies

### GitHub Skills Toolkit
- Workflows use `skills/exercise-toolkit` (currently v0.7.0)
- Provides reusable workflow actions for common exercise patterns
- Reference: Exercise workflow templates in `.github/workflows/`

### GitHub API Integration
- Workflows interact with GitHub API to:
  - Create/update issues for learner tracking
  - Post step content as comments
  - Validate file changes in learner repositories
- Uses `actions/checkout@v5` and custom comment actions

### Template Repository Feature
- When set as a template (`is_template: true`), users can click "Use this template" to create their own exercise
- Workflows check `!github.event.repository.is_template` to avoid running on the template itself

## When Modifying This Repository

### Adding a New Step
1. Create `N-step.md` in `.github/steps/` following the standard template
2. Create corresponding `N-step.yml` in `.github/workflows/`
3. Update workflow to include validation criteria for step completion
4. Update README with new step reference

### Updating Workflows
- Never remove the `skills/exercise-toolkit` dependency without understanding the implications
- Maintain the workflow naming pattern (number-based sequencing)
- Keep environment variable `STEP_N_FILE` synchronized with actual file paths

### Content Guidelines for AI Agents
- Prioritize clarity and brevity—exercises should be completable in stated time
- Each step should have one clear learning objective
- Theory sections should explain "why", activity sections should focus on "how"
- Troubleshooting should address common beginner mistakes
