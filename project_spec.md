# Project Specification

> **This document is the product definition.** Everything gets built from this spec.
> Everything gets tested against this spec. If the spec is complete and correct,
> the implementation is a mechanical process that can be handed to an agent.
>
> **The quality of this document determines the quality of the output.**
> Vague specs produce vague results. Precise specs produce precise results.
> If you cannot describe it clearly enough for a machine to build it,
> you do not understand it well enough yet.
>
> **This is a living document.** Update it as the project evolves. If a feature
> is cut, a data model changes, or a constraint is added, update this file immediately.
> The spec must always reflect the current truth of the project.
>
> **Test for completeness:** Could someone (or something) build this without asking
> you a single question? If no, the spec has gaps. Fill them before starting work.
>
> **For visual production projects:** This spec has a required companion document,
> `brand_dna.md`, which defines the visual production standards (image quality,
> product taxonomy, rejection criteria, prompt rules). The project spec defines
> what the system does. The Brand DNA defines what the system produces. Both
> documents are required. Behavioral scenarios in Section 4 should reference
> the Brand DNA as the evaluation rubric where applicable.

---

## 1. Project Overview

### What Is Being Built

<!-- One to three sentences. What is this thing? Not how it works, not why -->
<!-- it matters. Just what it is. -->
<!-- Example: "A web-based image approval portal where clients review, approve, -->
<!-- or reject AI-generated product images organized by SKU." -->

[Define what is being built]

### Why It Exists

<!-- What problem does this solve? Who has that problem? What are they doing -->
<!-- today instead of using this? -->
<!-- Example: "Clients currently receive images via email and approve via reply. -->
<!-- This is slow, unorganized, and produces no audit trail." -->

[Define the problem and context]

### Who It Is For

<!-- Primary users and their technical comfort level. -->
<!-- Example: "Primary user: Marketing coordinator at a food distribution company. -->
<!-- Comfortable with web apps but not technical. Reviews images in batches of -->
<!-- 20-50. Accesses the portal 2-3 times per week." -->

[Define the users]

### Success Criteria

<!-- How do you know this project is done AND working? Measurable outcomes. -->
<!-- Use numbers where possible. -->
<!-- Example: -->
<!-- - Clients complete image reviews in the portal instead of email within -->
<!--   2 weeks of launch -->
<!-- - Average review turnaround drops from 5 days to 2 days -->
<!-- - Zero images are lost or misattributed -->
<!-- - API response time under 200ms for all client-facing endpoints -->

- [Measurable outcome 1]
- [Measurable outcome 2]
- [Measurable outcome 3]

---

## 2. Scope

### In Scope

<!-- Explicit list of what this project includes. One line per capability. -->
<!-- These capabilities define what the system does. Section 4 defines how -->
<!-- it behaves in detail, including edge cases and failure handling. -->
<!-- Example: -->
<!-- - Email link authentication (no passwords) -->
<!-- - Image gallery grouped by SKU -->
<!-- - Single-image approve/reject -->
<!-- - Rejection with required reason -->
<!-- - Batch approve for multiple selected images -->
<!-- - Admin dashboard with approval status across all SKUs -->

- [Capability 1]
- [Capability 2]
- [Capability 3]

### Out of Scope

<!-- What this project does NOT include. Things someone might reasonably -->
<!-- assume are included but are not. Prevents scope creep from both -->
<!-- humans and agents. -->
<!-- Example: -->
<!-- - Image editing or cropping within the portal -->
<!-- - User role management (single role: reviewer) -->
<!-- - Mobile-native app (responsive web only) -->

- [Exclusion 1]
- [Exclusion 2]
- [Exclusion 3]

### Future Considerations

<!-- Intentionally deferred. Current implementation should not make these -->
<!-- harder to add later. -->

- [Future item 1]
- [Future item 2]

---

## 3. Data Model and Schema

> This section defines the data structures that the system operates on.
> The data model is often the single most important architectural decision.
> Get this right before writing code.

### Primary Entities

<!-- Define each data entity the system works with. Include field names, -->
<!-- types, and constraints. Use the format native to your stack -->
<!-- (TypeScript interfaces, Firestore document structure, etc.). -->

<!-- Example: -->
<!-- -->
<!-- **Image Record** -->
<!-- ```typescript -->
<!-- interface ImageRecord { -->
<!--   id: string;              // Auto-generated -->
<!--   sku: string;             // From client CSV -->
<!--   batchId: string;         // Groups images by generation run -->
<!--   filePath: string;        // Firebase Storage path -->
<!--   status: 'pending' | 'approved' | 'rejected'; -->
<!--   verdict?: { -->
<!--     decision: 'approved' | 'rejected'; -->
<!--     reason?: string;       // Required if rejected -->
<!--     reviewerId: string; -->
<!--     timestamp: Date; -->
<!--   }; -->
<!--   generation: { -->
<!--     model: string;         // e.g., 'nano_banana' -->
<!--     prompt: string;        // Full prompt used -->
<!--     attempt: number;       // Retry count (1 = first try) -->
<!--     referenceImagePath?: string; // If generated from reference -->
<!--   }; -->
<!--   evalResult?: { -->
<!--     verdict: 'pass' | 'fail'; -->
<!--     violations: string[];  // Specific failures from eval gate -->
<!--     confidence: number;    // 1-10 -->
<!--   }; -->
<!--   createdAt: Date; -->
<!--   updatedAt: Date; -->
<!-- } -->
<!-- ``` -->

```
[Define primary data entities]
```

### Data Sources

<!-- Where data comes in from. Format, structure, and any transformation needed. -->
<!-- Example: -->
<!-- - Client SKU list: CSV with columns (itemNo, brand, webItemShortDesc, -->
<!--   category, manufacturerItemNo). Uploaded manually per batch. -->
<!-- - Reference images: PNG files from Serper.dev search, stored in -->
<!--   Firebase Storage at clients/{clientId}/references/{itemNo}.png -->

- [Data source 1: format, structure, how it enters the system]
- [Data source 2: format, structure, how it enters the system]

### Storage Structure

<!-- How and where data is stored. Be explicit about paths, collections, -->
<!-- and naming conventions. -->
<!-- Example: -->
<!-- -->
<!-- Firestore: -->
<!-- - clients/{clientId}/batches/{batchId} - Batch metadata -->
<!-- - clients/{clientId}/batches/{batchId}/images/{imageId} - Image records -->
<!-- -->
<!-- Firebase Storage: -->
<!-- - clients/{clientId}/references/{itemNo}.png - Reference images -->
<!-- - clients/{clientId}/generated/{batchId}/{itemNo}_{attempt}.png - Generated -->
<!-- - clients/{clientId}/approved/{itemNo}.png - Final approved images -->

```
[Define storage structure]
```

---

## 4. Behavioral Scenarios

> These are the executable test cases for the project. Written in
> Given/When/Then format so they can be directly translated into
> automated tests.
>
> **This section is what makes Level 4 work.** When you walk away and come
> back hours later, these scenarios are what you check. If they all pass,
> the project is working correctly regardless of how the code is written.

### Happy Path Scenarios

<!-- Normal, expected user and system flows. -->
<!-- Example: -->
<!-- -->
<!-- **Scenario: Reviewer approves a single image** -->
<!-- - Given: A reviewer is logged in and viewing a batch with 10 pending images -->
<!-- - When: The reviewer clicks "Approve" on the first image -->
<!-- - Then: The image status changes to "approved" in Firestore -->
<!-- - And: The dashboard count updates to show 9 pending, 1 approved -->
<!-- - And: The approval is recorded with reviewer ID and timestamp -->
<!-- -->
<!-- **Scenario: Pipeline generates image from reference** -->
<!-- - Given: A SKU has a verified reference image in Firebase Storage -->
<!-- - And: The Brand DNA spec defines photography rules for this category -->
<!-- - When: The pipeline processes this SKU -->
<!-- - Then: A prompt is constructed using the Brand DNA prompt rules -->
<!-- - And: The image is generated using the reference image as input -->
<!-- - And: The eval gate scores the image against Brand DNA rejection criteria -->
<!-- - And: The result (pass/fail with details) is logged to the production log -->

**Scenario: [Name]**
- Given: [Initial state]
- When: [Action taken]
- Then: [Expected result]
- And: [Additional expected result]

**Scenario: [Name]**
- Given: [Initial state]
- When: [Action taken]
- Then: [Expected result]

### Edge Case Scenarios

<!-- Unusual or unexpected situations. Where most bugs live. -->
<!-- Example: -->
<!-- -->
<!-- **Scenario: No reference image found for SKU** -->
<!-- - Given: The Serper search returns no results for a SKU -->
<!-- - And: Gemini Flash verification has no image to evaluate -->
<!-- - When: The pipeline reaches this SKU -->
<!-- - Then: The SKU is flagged as "no reference" in the batch log -->
<!-- - And: The pipeline generates an image from description only -->
<!-- - And: The image is tagged as "description-generated" (not "reference-generated") -->
<!-- - And: This image is routed to mandatory human review (not auto-approved) -->

**Scenario: [Name]**
- Given: [Initial state]
- When: [Action or unexpected event]
- Then: [Expected system behavior]

### Failure Scenarios

<!-- What happens when the system itself fails. -->
<!-- Example: -->
<!-- -->
<!-- **Scenario: Image generation API returns an error** -->
<!-- - Given: The pipeline is processing a batch of 50 SKUs -->
<!-- - When: The Nano Banana API returns a 500 error for SKU #23 -->
<!-- - Then: The error is logged with SKU, timestamp, and error response -->
<!-- - And: SKU #23 is marked as "generation-failed" in the batch log -->
<!-- - And: The pipeline continues processing SKUs #24-50 -->
<!-- - And: Failed SKUs are retried at the end of the batch (max 3 retries) -->

**Scenario: [Name]**
- Given: [Initial state]
- When: [System failure occurs]
- Then: [Expected graceful behavior]

### Verification Commands

<!-- How to run the tests that validate these scenarios. -->
<!-- Example: -->
<!-- - Unit tests: `npm run test` -->
<!-- - Behavioral tests: `npm run test:behavior` -->
<!-- - Full suite: `npm run test:all` -->
<!-- - Coverage report: `npm run test:coverage` (target: >80%) -->

```
[Test commands]
```

---

## 5. Boundary Rules

> Three tiers of constraints governing what the agent can and cannot do.
> The "Ask First" tier explicitly shrinks over time as confidence in the
> system grows. Items migrate from "Ask First" to "Always Do" or "Never Do"
> as the project matures. This migration IS the progression from Level 3
> to Level 4.

### Always Do

<!-- Hard rules. Non-negotiable. The agent follows these without exception. -->
<!-- Example: -->
<!-- - Run the full test suite before every commit -->
<!-- - Use environment variables for all API keys and secrets -->
<!-- - Log all errors with timestamp, context, and stack trace -->
<!-- - Update state.md after completing any task -->
<!-- - Follow commit message format defined in CLAUDE.md -->

- [Always rule 1]
- [Always rule 2]
- [Always rule 3]

### Ask First

<!-- Judgment calls that still need human approval at the current level. -->
<!-- Review this tier regularly. If an item has been approved the same way -->
<!-- three times in a row, it is a candidate for "Always Do." -->
<!-- Example: -->
<!-- - Modify any database schema or data model -->
<!-- - Add a new dependency or package -->
<!-- - Change any API endpoint signature -->
<!-- - Delete any existing file -->
<!-- - Modify authentication or authorization logic -->

- [Ask first item 1]
- [Ask first item 2]
- [Ask first item 3]

### Never Do

<!-- Absolute prohibitions. Protect security, data, and system integrity. -->
<!-- Example: -->
<!-- - Never commit secrets, API keys, or credentials to the repository -->
<!-- - Never modify files in node_modules or dependency directories -->
<!-- - Never delete or overwrite production data -->
<!-- - Never bypass authentication checks -->
<!-- - Never expose internal error details to end users -->

- [Never rule 1]
- [Never rule 2]
- [Never rule 3]

---

## 6. Technical Constraints

> For standard AD-5 stack decisions (framework, styling, linting, commit
> format, workflow), refer to the global CLAUDE.md and project CLAUDE.md.
> This section only contains project-specific constraints that go beyond
> or differ from the AD-5 standard.

### Stack Additions or Overrides

<!-- Only list technologies that are NOT already in CLAUDE.md, or cases -->
<!-- where this project deviates from the standard. -->
<!-- Example: -->
<!-- - Serper.dev API for image search (not standard AD-5, specific to this project) -->
<!-- - Nano Banana (standard tier, not Pro) for image generation -->
<!-- - Gemini Flash for reference image verification -->
<!-- If the project uses the standard AD-5 stack with no additions, write: -->
<!-- "Standard AD-5 web stack per CLAUDE.md. No project-specific additions." -->

[Stack additions or "Standard AD-5 stack per CLAUDE.md"]

### Integration Points

<!-- External systems this project connects to. For each: what data flows, -->
<!-- which direction, and what happens if the integration fails. -->
<!-- Example: -->
<!-- - Serper.dev: Outbound image search queries. Returns image URLs. -->
<!--   If unavailable: SKU is flagged for manual reference image sourcing. -->
<!-- - Firebase Storage: Read/write generated and reference images. -->
<!--   If unavailable: Pipeline halts and logs the outage. -->
<!-- - Nano Banana API: Outbound image generation requests. -->
<!--   If unavailable: SKU is queued for retry. Max 3 retries, then flagged. -->

- [Integration 1: system, data flow, failure behavior]
- [Integration 2: system, data flow, failure behavior]

### Performance and Limits

<!-- Specific numbers. Not "should be fast." -->
<!-- Example: -->
<!-- - Batch processing: handle 50 SKUs per run without timeout -->
<!-- - Image generation: under 30 seconds per image -->
<!-- - Firebase free tier: 1GB storage, 50K reads/day -->
<!-- - Serper.dev: 2,500 searches/month on current plan -->

- [Limit 1]
- [Limit 2]

---

## 7. User Interface Specification

> **For non-UI projects** (pipelines, APIs, CLIs): Replace this entire section
> with "Output Format Specification" defining what the system produces, in
> what format, where it goes, and what the output looks like. See the
> alternative template below.
>
> **For web/app projects:** Define what the user sees and interacts with.
> For projects using the JSONC Design Brief workflow, reference the brief here.

<!-- ================================================================== -->
<!-- OPTION A: UI PROJECTS (websites, portals, dashboards)              -->
<!-- ================================================================== -->

### Pages / Views

<!-- List every distinct page or view. For each: what it shows, what the -->
<!-- user can do. -->
<!-- Example: -->
<!-- -->
<!-- **Login Page** -->
<!-- - Email input field, "Send login link" button -->
<!-- - No password. Auth via email magic link. -->
<!-- - After submitting: "Check your email" confirmation -->
<!-- -->
<!-- **Review Dashboard** -->
<!-- - Header: client name, batch ID, progress bar (X of Y reviewed) -->
<!-- - Grid of image thumbnails (4 columns desktop, 2 mobile) -->
<!-- - Each thumbnail: image, SKU, product name -->
<!-- - Click thumbnail to open full-size review view -->
<!-- - Filter tabs: All / Pending / Approved / Rejected -->

[Define pages and views]

### Design Reference

<!-- Link to JSONC design brief, mockup, or design system. -->
<!-- Example: "See design_brief.jsonc for full token specification." -->
<!-- Or: "Clean, minimal. White background. Images are the focus. -->
<!-- Professional review tool aesthetic, not consumer app." -->

[Design direction or reference link]

<!-- ================================================================== -->
<!-- OPTION B: NON-UI PROJECTS (pipelines, APIs, CLIs)                  -->
<!-- Delete Option A above and use this instead.                        -->
<!-- ================================================================== -->

<!-- ### Output Format Specification -->
<!--  -->
<!-- What the system produces, in what format, and where. -->
<!-- Example: -->
<!--  -->
<!-- **Generated Images** -->
<!-- - Format: PNG, 2048x2048, 72 DPI, sRGB -->
<!-- - Location: Firebase Storage at clients/{clientId}/generated/{batchId}/ -->
<!-- - Naming: {itemNo}_{brand}_{attempt}.png -->
<!--  -->
<!-- **Batch Report** -->
<!-- - Format: JSON -->
<!-- - Location: clients/{clientId}/batches/{batchId}/report.json -->
<!-- - Contents: total SKUs, successful, failed, flagged for review, -->
<!--   per-SKU status with generation details -->
<!--  -->
<!-- **Production Log** -->
<!-- - Format: JSONL (one JSON object per line) -->
<!-- - Location: clients/{clientId}/logs/{batchId}.jsonl -->
<!-- - Per entry: SKU, prompt used, model, attempt number, eval result, -->
<!--   retry adjustments, final status -->

---

## 8. Environment and Deployment

### Deployment Target

<!-- Where this runs in production. -->
<!-- Example: -->
<!-- - Hosting: Vercel (web app) or Hostinger VPS (pipeline/API) -->
<!-- - Region: US East -->
<!-- - Domain: portal.ad5creative.com or internal only -->

[Define deployment target]

### Environment Variables

<!-- Every environment variable the system needs. Do not include values. -->
<!-- Values go in .env (gitignored). This documents what is required. -->
<!-- Example: -->
<!-- - FIREBASE_PROJECT_ID - Firebase project identifier -->
<!-- - FIREBASE_STORAGE_BUCKET - Storage bucket name -->
<!-- - SERPER_API_KEY - Serper.dev API key for image search -->
<!-- - NANO_BANANA_API_KEY - Nano Banana image generation API key -->
<!-- - GEMINI_API_KEY - Google Gemini API key for verification -->

- [ENV_VAR_1 - description]
- [ENV_VAR_2 - description]

### CI/CD

<!-- How code gets from repository to production. -->
<!-- Example: -->
<!-- - Push to main triggers Vercel deployment -->
<!-- - Preview deployments on pull requests -->
<!-- - No deployment without passing test suite -->
<!-- Or for simpler projects: -->
<!-- - Manual deployment via `npm run deploy` -->
<!-- - No CI/CD pipeline (single developer, manual verification) -->

[Define deployment process]

---

## 9. Implementation Plan

> **This section is completed by the agent, not by you.**
> After reading sections 1-8 and reviewing the Acceptance Checklist in
> Section 10, the agent drafts its implementation plan here.
> You review and approve the plan before any code is written.
> This is the "Explore, Plan" phase of the Explore, Plan, Code, Commit workflow.

### Proposed File Changes

<!-- Agent lists every file it plans to create or modify. -->

| Action | File Path | Purpose |
|--------|-----------|---------|
| [Create/Modify] | [path] | [What this file does] |

### Approach

<!-- Agent describes its implementation strategy. How it plans to satisfy -->
<!-- the requirements. Architecture decisions. Build order. -->

[Agent completes this section]

### Rationale

<!-- Agent explains why it chose this approach over alternatives. -->
<!-- If the rationale does not make sense, reject the plan before -->
<!-- code is written. -->

[Agent completes this section]

---

## 10. Acceptance Checklist

> Final pass/fail gate for the entire project. When all items are checked,
> the project is done. The /phase-gate slash command should reference this
> checklist as the authoritative definition of "done" for spec-driven projects.

### Automated (Behavioral Scenarios Pass)

<!-- These map directly to Section 4. If the test suite passes, these are done. -->

- [ ] All happy path scenarios pass
- [ ] All edge case scenarios pass
- [ ] All failure scenarios pass
- [ ] Test coverage meets target (define %)

### Manual Verification

<!-- Things that require human eyes or judgment. Keep this list as short -->
<!-- as possible. Every item here is a task you must do personally. The -->
<!-- goal over time is to migrate items from here into automated scenarios. -->
<!-- Example: -->
<!-- - [ ] UI looks correct on mobile (375px) and desktop (1920px) -->
<!-- - [ ] Dark mode renders correctly (if applicable) -->
<!-- - [ ] Generated images match expected quality (spot-check 10%) -->

- [ ] [Manual check 1]
- [ ] [Manual check 2]

### Deployment Verification

<!-- Post-deploy checks confirming the system works in production. -->
<!-- Example: -->
<!-- - [ ] Production URL is accessible -->
<!-- - [ ] Authentication flow works end to end -->
<!-- - [ ] First real batch processes successfully -->

- [ ] [Deployment check 1]
- [ ] [Deployment check 2]

---

## 11. Attachments and References

<!-- The project spec is the master document. Everything else is an -->
<!-- attachment. For visual production projects, brand_dna.md is REQUIRED, -->
<!-- not optional. -->

| Document | Location | Required | Purpose |
|----------|----------|----------|---------|
| Brand DNA Specification | `brand_dna.md` | Yes (visual production) / No (other) | Visual production standards, eval rubric |
| JSONC Design Brief | `design_brief.jsonc` | If UI project | UI design tokens |
| State File | `state.md` | Yes | Current project state and progress |
| Global Standards | `~/.claude/CLAUDE.md` | Reference only | AD-5 standard stack and workflow |
| [Other reference] | [path or URL] | [Yes/No] | [What it is used for] |

---

## Revision History

<!-- Date, what changed, why. Every change has a reason. -->

| Date | Change | Reason |
|------|--------|--------|
| [YYYY-MM-DD] | Initial creation | [Context for why this spec was written] |
