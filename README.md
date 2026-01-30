# Resume Builder

A Claude Code skill for building comprehensive, evidence-based resumes by mining your actual work history from git repositories.

## Why This Exists

Most resumes are written from memory, leading to vague bullet points like "worked on microservices" or "improved performance." This skill helps you build a resume grounded in evidence—your actual commits, the code you wrote, the architecture decisions you made.

## Installation

Copy the `.claude/commands/resume.md` file to your own project's `.claude/commands/` directory, or clone this repo and run Claude Code from here.

```bash
git clone https://github.com/yourusername/resume-builder.git
cd resume-builder
claude
```

Then invoke with:
```
/resume
```

## Modes

### 1. Update Resume
Add new projects or refine existing content. The skill interviews you with targeted questions:
- What legacy system did you replace?
- What problem did it solve?
- What did you specifically build?
- What metrics can you cite?

### 2. Mine Repos
Scan your local git repositories to find evidence for your resume:
- Commit history by date range
- Tech stack from package files
- Architecture from code structure
- Pipeline configs for DevOps experience

### 3. Generate Tailored Version
Create a 1-2 page version targeted at a specific job description. The skill:
- Analyzes which experiences are most relevant
- Incorporates keywords naturally
- Keeps your strongest metrics
- Outputs clean markdown

### 4. Full Workflow
Walk through the entire resume building process interactively, from data gathering to final formatting.

## The Process

See [PROCESS.md](PROCESS.md) for the methodology behind evidence-based resume building.

## Example

See [examples/senior-software-engineer.md](examples/senior-software-engineer.md) for a complete resume built using this process.

## Confidentiality by Design

The skill is built to **describe what you did, not expose what you built**. When mining repos:

- Extracts patterns, technologies, and architectural approaches
- Never copies actual code into your resume
- Abstracts internal project names and proprietary terms
- Focuses on transferable skills and accomplishments

Your resume should demonstrate your capabilities without revealing your employer's intellectual property.

## Writing Style

The skill follows these principles:
- **Problem/Solution framing** — Show what was broken and how you fixed it
- **Evolution sections** — Demonstrate architectural growth over time
- **Concrete metrics** — Adoption rates, time savings, user counts
- **Ownership clarity** — Solo developer vs. team collaboration
- **Strong verbs** — Led, Designed, Built, Pioneered, Architected

## License

MIT
