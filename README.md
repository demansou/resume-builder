# Resume Builder

A Claude Code skill for building evidence-based resumes by mining your actual work history—not just memory.

## Why This Exists

Most resumes are written from memory, leading to vague bullet points like "worked on projects" or "improved outcomes." This skill helps you build a resume grounded in evidence from your documented work: code you committed, documents you wrote, projects you shipped, articles you published.

## Master vs. Tailored Resume

This system uses a **two-tier approach**:

### Master Resume
Your comprehensive, unabridged work history. Include everything:
- All roles, projects, and accomplishments
- Full technical detail and context
- Complete metrics and outcomes
- No length limit

The master is your **source of truth**—you maintain it over time and never send it to employers directly. See [examples/master-resume.md](examples/master-resume.md).

### Tailored Resume
A focused 1-2 page version derived from your master, customized for a specific job:
- Cherry-pick relevant experience
- Reorder sections to lead with what matters
- Emphasize keywords from the job posting
- Remove or condense less relevant content

You generate a new tailored version for each application. See [examples/tailored-resume.md](examples/tailored-resume.md) for a version targeting a backend infrastructure role.

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

### Option 1: Plugin Marketplace (Recommended)

Add the marketplace and install the plugin:

```bash
/plugin marketplace add demansou/resume-builder
/plugin install resume-builder
```

### Option 2: Clone and Run

```bash
git clone https://github.com/demansou/resume-builder.git
cd resume-builder
claude
```

### Option 3: Manual Copy

Copy `skills/resume/SKILL.md` to your project's `.claude/commands/resume.md`

---

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
Create a targeted version for a specific job posting:
- **Accepts job description via URL, pasted text, or file**
- Fetches and analyzes job postings from LinkedIn, Greenhouse, Lever, etc.
- Maps your experience to job requirements
- Reorders and emphasizes relevant accomplishments
- Incorporates keywords naturally (no keyword stuffing)
- Identifies gaps to address in cover letter
- Outputs clean 1-2 page markdown

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

## Examples

- [examples/master-resume.md](examples/master-resume.md) — Full master resume with complete detail
- [examples/tailored-resume.md](examples/tailored-resume.md) — Condensed version for a backend infrastructure role

## Writing Style

The skill follows these principles:
- **SAR format** — Situation, Action, Result
- **Active voice** — Led, Built, Grew, Delivered
- **Concrete metrics** — Percentages, dollar amounts, scale
- **Scope clarity** — Solo ownership vs. team collaboration
- **Progression** — Show growth over time

## License

MIT
