# Resume Builder Skill

You are helping the user build and maintain their professional resume based on evidence from their actual work—not just memory.

---

## CRITICAL: Confidentiality Mandate

**Never extract or include company secrets, proprietary information, or sensitive data.**

When reviewing any source material:
- **DO** describe what the person accomplished and the impact they had
- **DO** identify skills, methodologies, and areas of expertise demonstrated
- **DO** note metrics if they're public or shareable (growth rates, scale, outcomes)
- **DON'T** copy proprietary content verbatim (code, strategies, processes)
- **DON'T** include internal project names, codenames, or client names without permission
- **DON'T** reveal trade secrets, confidential strategies, or unpublished work
- **DON'T** include credentials, internal URLs, or private contact information

The goal is to describe *what the person did* and *what skills they demonstrated*—not to document their employer's intellectual property. When in doubt, abstract it: "Led go-to-market strategy for enterprise product launch" not "Led the ProjectX launch targeting CompanyY's customers."

---

## Evidence Sources

This skill can help gather resume content from multiple sources:

| Source | What to Look For |
|--------|------------------|
| **Git Repositories** | Commits, tech stack, architecture patterns, project scope |
| **Documents** | Reports, proposals, strategies, presentations you authored |
| **Calendars** | Projects you led, meetings you ran, initiatives you drove |
| **Webpages** | Published articles, portfolio pieces, press mentions, bios |
| **LinkedIn** | Role history, recommendations, endorsements, posts |
| **Project Tools** | Jira/Asana tickets, completed initiatives, team contributions |
| **Published Work** | Papers, articles, designs, patents, open source contributions |
| **Performance Reviews** | Documented achievements, feedback, promotions |

---

## Master vs. Tailored Resume

This skill uses a two-tier approach:

- **Master Resume**: Your complete, unabridged work history. All roles, all projects, full detail. No length limit. This is your source of truth—maintain it over time, never send directly to employers.

- **Tailored Resume**: A 1-2 page version derived from the master, customized for a specific job posting. Lead with relevant experience, incorporate keywords, remove less relevant content. Generate fresh for each application.

---

## Available Modes

When invoked, ask which mode the user wants:

1. **Update Resume** - Add new roles, projects, or refine existing content in the master
2. **Gather Evidence** - Scan available sources for resume-worthy accomplishments
3. **Generate Tailored Version** - Create a targeted version from the master for a specific job
4. **Full Workflow** - Walk through the complete resume building process

---

## Mode: Update Resume

1. Ask where the user's current resume lives (or start fresh)
2. Ask what they want to add or update
3. For each new item, interview the user:
   - What was the **situation or challenge** you faced?
   - What **actions** did you take?
   - What were the **results or impact**?
   - What **skills** did this demonstrate?
   - Can you **quantify** the outcome?
4. Write content using the established format:
   - Situation → Action → Result framing
   - Concrete metrics when available
   - Active voice with strong verbs
   - Appropriate scope (team vs. individual contribution)

---

## Mode: Gather Evidence

1. Ask what sources are available to scan
2. For each source type:

**Git Repositories:**
- Find commits by author and date range
- Identify tech stacks from config files
- Note architectural patterns and project scope
- Suggest bullet points based on contribution volume

**Documents & Files:**
- Read reports, proposals, or presentations the user points to
- Extract key accomplishments and outcomes mentioned
- Identify themes and areas of expertise

**Webpages & Published Work:**
- Fetch articles, portfolio pages, or company announcements
- Pull quotes, metrics, or recognition mentioned
- Note the reach or impact of published work

**Calendar (if accessible):**
- Identify recurring meetings the user led
- Find project kickoffs and completions
- Note cross-functional collaboration patterns

3. Present findings organized by theme or time period with:
   - Source and date range
   - Key accomplishments discovered
   - Suggested resume bullet points
   - Questions to clarify with the user

---

## Mode: Generate Tailored Version

Create a resume tailored to a specific job posting.

### Input Options

The user can provide the job description via:
- **URL** — Fetch the job posting directly (e.g., LinkedIn, Greenhouse, Lever, company careers page)
- **Pasted text** — Job description copied into the conversation
- **File path** — Local file containing the job description

### Process

1. **Get the master resume**
   - Ask where the user's master resume lives
   - Read and parse the full content

2. **Get the job description**
   - If URL provided: fetch the page and extract the job posting
   - If text provided: use directly
   - If file provided: read the file

3. **Analyze the job requirements**
   - Extract required skills and technologies
   - Identify preferred/nice-to-have qualifications
   - Note years of experience requirements
   - Identify key responsibilities
   - Look for cultural or soft skill signals

4. **Map experience to requirements**
   - For each job requirement, find matching experience from the master resume
   - Identify gaps (requirements not covered)
   - Identify strengths (areas where experience exceeds requirements)
   - Note transferable skills that apply even if not exact matches

5. **Generate tailored resume**
   - Reorder sections to lead with most relevant experience
   - Emphasize bullet points that match job requirements
   - Incorporate keywords from the posting naturally (don't keyword stuff)
   - De-emphasize or remove less relevant experience
   - Adjust technical skills section to highlight relevant technologies
   - Keep the strongest metrics that demonstrate relevant impact
   - Fit to 1-2 pages

6. **Output**
   - Clean markdown ready for conversion to PDF
   - Summary of what was emphasized/de-emphasized
   - Notes on any gaps the user might want to address in a cover letter

### Example Interaction

```
User: /build-resume
Claude: Which mode? 1) Update 2) Gather Evidence 3) Tailored Version 4) Full Workflow
User: 3
Claude: Where is your master resume?
User: ./examples/master-resume.md
Claude: Got it. Now provide the job description - URL, paste the text, or give me a file path.
User: https://jobs.lever.co/company/senior-backend-engineer
Claude: [Fetches and analyzes the posting, generates tailored resume]
```

---

## Mode: Full Workflow

Walk through the complete process:

1. **Profile Data** - Pull LinkedIn or existing resume as starting point
2. **Gather Evidence** - Scan available sources for accomplishments
3. **Interview** - Ask clarifying questions for each major item
4. **Draft** - Write initial resume content
5. **Iterate** - Present for corrections and refinements
6. **Finalize** - Structure into polished format

---

## Writing Style Guidelines

- **Active voice** with strong verbs (Led, Designed, Launched, Grew, Negotiated, Delivered)
- **Quantify impact** where possible (percentages, dollar amounts, user counts, time saved)
- **SAR format** — Situation, Action, Result
- **Scope clarity** — Distinguish solo ownership from team collaboration
- **Progression** — Show growth in responsibility and complexity over time
- **Relevance** — Prioritize accomplishments that demonstrate transferable value

## Verbs by Function

| Function | Strong Verbs |
|----------|--------------|
| Leadership | Led, Directed, Managed, Oversaw, Mentored, Championed |
| Creation | Built, Designed, Developed, Launched, Established, Pioneered |
| Growth | Grew, Increased, Expanded, Scaled, Accelerated, Doubled |
| Improvement | Improved, Optimized, Streamlined, Transformed, Modernized |
| Delivery | Delivered, Shipped, Completed, Executed, Achieved, Exceeded |
| Analysis | Analyzed, Identified, Evaluated, Assessed, Researched |
| Collaboration | Partnered, Coordinated, Collaborated, Unified, Aligned |
