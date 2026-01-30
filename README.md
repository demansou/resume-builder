# Resume Builder

A Claude Code skill for building evidence-based resumes by mining your actual work history—not just memory.

## Why This Exists

Most resumes are written from memory, leading to vague bullet points like "worked on projects" or "improved outcomes." This skill helps you build a resume grounded in evidence from your documented work: code you committed, documents you wrote, projects you shipped, articles you published.

## Who This Is For

Anyone with a body of work they can point to:
- **Engineers** — Git repos, architecture docs, technical specs
- **Product Managers** — PRDs, roadmaps, launch announcements
- **Marketers** — Campaigns, reports, published content
- **Designers** — Portfolios, case studies, shipped products
- **Salespeople** — Closed deals, presentations, pipeline reports
- **Researchers** — Papers, patents, conference talks
- **Anyone** — Performance reviews, project docs, LinkedIn history

## Installation

Copy `.claude/commands/resume.md` to your project's `.claude/commands/` directory, or clone this repo:

```bash
git clone https://github.com/demansou/resume-builder.git
cd resume-builder
claude
```

Then invoke with:
```
/resume
```

## Evidence Sources

The skill can gather resume content from:

| Source | What to Look For |
|--------|------------------|
| Git Repositories | Commits, tech stack, architecture patterns |
| Documents | Reports, proposals, presentations you authored |
| Calendars | Projects led, meetings run, initiatives driven |
| Webpages | Published articles, portfolio pieces, press mentions |
| LinkedIn | Role history, recommendations, posts |
| Project Tools | Jira/Asana tickets, completed initiatives |
| Published Work | Papers, articles, designs, patents |

## Modes

### 1. Update Resume
Add new roles or refine existing content. The skill interviews you:
- What was the situation or challenge?
- What actions did you take?
- What were the results?
- Can you quantify the outcome?

### 2. Gather Evidence
Scan your available sources for resume-worthy accomplishments:
- Git commit history and tech stacks
- Documents and reports you've written
- Published work and portfolio pieces
- Calendar patterns showing leadership

### 3. Generate Tailored Version
Create a targeted version for a specific opportunity:
- Analyzes which experiences are most relevant
- Incorporates keywords naturally
- Keeps your strongest metrics
- Outputs clean markdown

### 4. Full Workflow
Walk through the complete process from gathering evidence to polished resume.

## Confidentiality by Design

The skill describes **what you did**, not what you built for your employer:

- Extracts patterns, skills, and accomplishments
- Never copies proprietary content verbatim
- Abstracts internal project names and client names
- Focuses on transferable skills and impact

Your resume demonstrates your capabilities without revealing your employer's intellectual property.

## The Process

See [PROCESS.md](PROCESS.md) for the methodology behind evidence-based resume building.

## Example

See [examples/senior-software-engineer.md](examples/senior-software-engineer.md) for a resume built using this process.

## Writing Style

The skill follows these principles:
- **SAR format** — Situation, Action, Result
- **Active voice** — Led, Built, Grew, Delivered
- **Concrete metrics** — Percentages, dollar amounts, scale
- **Scope clarity** — Solo ownership vs. team collaboration
- **Progression** — Show growth over time

## License

MIT
