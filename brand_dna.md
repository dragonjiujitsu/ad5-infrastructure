# Brand DNA Specification

> **Dual-purpose document.** This file is both human documentation and LLM evaluation rubric.
> A human reads this to understand every creative decision for this client's visual production.
> An LLM evaluator reads this to score generated images for quality and brand compliance.
> Write all criteria in plain, specific natural language so an automated evaluator can make
> pass/fail judgments without asking a human.

---

## Client Overview

<!-- One paragraph max. Company name, industry, what they sell, who their customer is. -->
<!-- Example: "Acme Industrial is a B2B distributor of safety equipment and industrial supplies. -->
<!-- Their customers are facility managers, safety officers, and procurement teams at manufacturing -->
<!-- plants, construction sites, and warehouses." -->

[Fill in client overview here]

---

## Output Requirements

<!-- Hard technical specs. These are numbers, not subjective guidelines. -->

| Parameter | Value |
|-----------|-------|
| Format | [e.g., PNG, JPEG, WebP] |
| Resolution | [e.g., 2048x2048px minimum] |
| DPI | [e.g., 300 for print, 72 for web] |
| Aspect Ratio | [e.g., 1:1 square, 4:3 landscape] |
| Color Space | [e.g., sRGB for web, Adobe RGB for print] |
| Background | [e.g., pure white (#FFFFFF), transparent, gradient] |
| File Size | [e.g., under 2MB per image] |
| Naming Convention | [e.g., {sku}_{angle}_{version}.png] |

---

## Product Taxonomy

<!-- List every category of product this client sells. Each category gets its own subsection -->
<!-- with photography rules specific to that category. Be explicit about angle, orientation, -->
<!-- lighting, surface appearance, what to show, and what NOT to show. -->

### [Category Name]

<!-- Example: "Boot Covers" -->

- **Typical products:** [Brief description of what falls in this category]
- **Camera angle:** [e.g., 3/4 front view, straight-on profile, top-down]
- **Orientation:** [e.g., single item centered, pair shown, laid flat vs standing]
- **Lighting:** [e.g., soft diffused, hard directional, studio white]
- **Surface appearance:** [e.g., show texture detail, matte finish, reflective allowed]
- **Must show:** [e.g., brand label visible, full product including sole, closure mechanism]
- **Must NOT show:** [e.g., no human model, no background environment, no competing brand logos]
- **Special notes:** [e.g., size markings should be legible, color must match catalog swatch]

### [Category Name]

<!-- Repeat the above structure for each product category -->

---

## Universal Rejection Criteria

<!-- Conditions that cause ANY image to fail regardless of product category. -->
<!-- These are non-negotiables. Write each criterion as a clear, testable statement -->
<!-- that an LLM evaluator can apply as a pass/fail check. -->

<!-- Remove any that do not apply to this client. Add client-specific criteria below. -->

- REJECT if the product is cropped or cut off at any edge of the frame.
- REJECT if the background is not uniform (gradients, shadows, or color variation visible).
- REJECT if visible artifacts, noise, or compression damage is present.
- REJECT if text, watermarks, or generated logos appear anywhere in the image.

<!-- Add client-specific rejection criteria below this line -->

---

## Prompt Construction Rules

<!-- How prompts should be built for this client's image generation. -->
<!-- These rules apply to all models unless overridden in the Anti-Prior Registry. -->

### Base Pattern

<!-- The standard prompt structure. Example: -->
<!-- "[Product type] by [Brand], [specific model/part number], [angle], [lighting], -->
<!-- [background], professional product photography, studio lighting, catalog quality" -->

```
[Define the base prompt pattern here]
```

### Always Include

<!-- Elements that must appear in every prompt for this client. -->
<!-- Example: "studio lighting", "pure white background", "catalog quality" -->

- [List required prompt elements]

### Never Include

<!-- Elements that must never appear in prompts for this client. -->
<!-- Example: "lifestyle", "in use", "person wearing", "outdoor setting" -->

- [List forbidden prompt elements]

### Length Guidance

<!-- Recommended prompt length and structure. -->
<!-- Example: "Keep prompts between 30-60 words. Front-load the product identity -->
<!-- (brand + part number + product type). Put style/quality keywords at the end." -->

[Define length and structure guidance here]

---

## Anti-Prior Registry

<!-- Known model behaviors that cause problems for this client's content. -->
<!-- This section grows over time as you discover new failure patterns during production. -->
<!-- For each entry, document: which model, what it does wrong, and the corrective prompt -->
<!-- language that fixes it. -->

<!-- Example format: -->
<!-- ### Nano Banana Pro: Adds fake brand text -->
<!-- - **Problem:** When prompted with brand names, NBPro sometimes generates fictional -->
<!--   text overlays that look like logos but contain wrong or garbled text. -->
<!-- - **Corrective language:** Add "no text overlays, no generated logos, no watermarks" -->
<!--   to the prompt. Use a reference image with the real logo visible. -->
<!-- - **Discovered:** 2026-02-15, during Lawson glove batch -->

### [Model Name]: [Brief problem description]

- **Problem:** [What the model does wrong]
- **Corrective language:** [Prompt additions or modifications that fix or mitigate it]
- **Discovered:** [Date and context]

---

## Reference Asset Index

<!-- List of approved reference images, character references, environment references, -->
<!-- or style references. Include file paths and descriptions of when each is used. -->
<!-- These are the "ground truth" images that generation and evaluation compare against. -->

| Asset | File Path | Description | Used For |
|-------|-----------|-------------|----------|
| [Name] | [path/to/file.png] | [What this reference shows] | [Which products or categories use it] |

---

## Revision History

<!-- Date, what changed, why. This document is living and gets updated as you learn -->
<!-- from production. Every change should have a reason. -->

| Date | Change | Reason |
|------|--------|--------|
| [YYYY-MM-DD] | Initial creation | [Why this client's Brand DNA was created] |
