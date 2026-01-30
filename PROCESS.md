# Resume Building Process

A repeatable process for building a comprehensive, evidence-based resume.

## 1. Start with LinkedIn Profile

- Pull public LinkedIn data (basic info, certifications, education)
- View full profile while logged in to get complete work history
- Extract dates, titles, and full job descriptions
- Click "see more" on each role to get expanded descriptions

## 2. Mine Local Repositories for Evidence

- Scan all repos in your working directory
- Run `git log --author="YourName" --since="YYYY-MM-01"` to find commits
- Identify projects by commit volume and content
- Read CLAUDE.md files and READMEs for project context
- Note commit counts per project for quantification

## 3. Deep Dive Each Project

For each major project, explore:
- Codebase structure (directories, key files)
- Pipeline configs (bitbucket-pipelines.yml, GitHub Actions) for CI/CD details
- Tech stack from package.json, .csproj, go.mod files
- Architectural patterns from code organization
- Database migrations for data model understanding
- API controllers for functionality overview

## 4. Interview Yourself

For each project, answer these questions:
- What was the **legacy system** you replaced?
- What **problem** did it solve for the business?
- What did **you specifically build** (solo vs. with team)?
- What **architectural decisions** did you make and why?
- What **metrics or impact** can you cite?
- What was the **evolution** of the architecture over time?

## 5. Iterate with Corrections

- Correct assumptions about scope and ownership
- Add business context that isn't visible in code
- Clarify technical nuances and tradeoffs
- Note what's complete vs. still in progress

## 6. Structure the Resume

### Framing Techniques
- **Problem/Solution** framing for major projects
- **Evolution sections** showing architectural journey
- **Pioneering language** where you were first to do something
- **Metrics** where available (adoption rates, time savings, user counts)

### Detail Levels
- **Master version**: Full detail with all context (this repo)
- **Application version**: 1-2 pages, distilled bullet points
- **Verbal version**: Key talking points for interviews

---

## Key Insight

The best resume details come from *your memory* of the business context, not just the code. The code shows *what* was built; you provide *why* and *what it replaced*.

---

## Tools Used

- **WebFetch**: Pull public web profile data
- **Browser automation**: View authenticated pages (LinkedIn logged-in view)
- **Git log**: Find commits by author and date range
- **Explore agent**: Scan codebases for structure and patterns
- **File reading**: READMEs, pipeline configs, package files
