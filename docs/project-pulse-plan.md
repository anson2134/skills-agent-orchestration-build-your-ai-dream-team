# Mona's Project Pulse dashboard plan

## Summary

Mona's Project Pulse dashboard is a single-page project health overview for a portfolio of workstreams. The implementation should feel polished and dashboard-first, with a clear hierarchy for project status, delivery risk, and operational health. The work will be orchestrated through GitHub Copilot CLI in a Codespace, with the Orchestrator coordinating a Designer for UX and a Coder for implementation and runtime support.

The dashboard will use a static data file as the source of truth, render structured HTML for the layout, and apply a responsive visual system through CSS. The app should be easy to preview locally from the Codespace using a lightweight browser launch configuration.

## Ordered implementation steps

1. Confirm the dashboard information model and data contract
   - Define the required fields in the project dataset: project title, owner, status, health, priority, completion, milestone, and any risk or dependency metadata.
   - Keep the data model deterministic and static so the dashboard can be previewed without a backend.

2. Create the project data source
   - Populate `app/project-data.json` with realistic example projects and status values.
   - Ensure each project entry includes the fields needed by the HTML and CSS hooks for cards, badges, and metrics.

3. Build the dashboard structure in `app/index.html`
   - Create the top-level dashboard wrapper, header, KPI summary area, and project cards grid.
   - Render project cards by reading the dataset and mapping fields to semantic HTML elements such as headings, status badges, and numeric values.
   - Keep the HTML clean and accessible, with consistent class names that match the CSS design system.

4. Design the dashboard visual system in `app/styles.css`
   - Define the dashboard shell, spacing scale, typography, color palette, status colors, and card treatment.
   - Ensure the first view clearly reads as a Dashboard, not as a generic page.
   - Add responsive behavior for narrow screens, tablet widths, and desktop layouts without breaking card readability.

5. Add runtime support in `.vscode/launch.json`
   - Configure a trivial local preview that opens `index.html` from the `app` folder.
   - Keep the config deterministic and easy for a learner to launch from VS Code in the Codespace.

6. Validate the full experience
   - Verify the static page renders without broken layout or missing data.
   - Check that the dashboard remains readable with varying content lengths and statuses.
   - Confirm the launch configuration opens the intended preview and the project cards display correctly.

## File assignments

- `app/project-data.json`
  - Primary owner: Coder
  - Responsibility: define the dataset shape, sample values, and project metadata needed by the dashboard.
  - Dependencies: should be finalized before HTML structure is locked so the markup matches available data fields.

- `app/index.html`
  - Primary owner: Coder
  - Responsibility: semantic markup for dashboard shell, summary metrics, and project cards.
  - Dependencies: relies on the final JSON schema and uses CSS classes designed by the Designer.

- `app/styles.css`
  - Primary owner: Designer
  - Responsibility: visual styling, hierarchy, status treatment, spacing, responsive layout, and accessibility contrast.
  - Dependencies: should follow the final HTML structure and the data model, but can evolve in parallel after the initial layout is stable.

- `.vscode/launch.json`
  - Primary owner: Coder
  - Responsibility: ensure the app can be previewed directly in the Codespace.
  - Dependencies: follows the final app folder structure and should be created once the dashboard file paths are confirmed.

## Designer responsibilities

- Establish the dashboard visual language: hierarchy, card styling, badge treatment, readability, and spacing.
- Ensure the first view reads as a genuine Project Pulse dashboard with high clarity and cross-device responsiveness.
- Maintain strong contrast, accessible typography, and consistent status color coding.
- Review the HTML and data structure for design-fit and propose adjustments before final styling locks.

## Coder responsibilities

- Build the static data contract and ensure it is valid JSON.
- Implement the semantic HTML layout to match the dashboard structure.
- Wire the HTML to the dataset in a way that remains easy to maintain.
- Create the VS Code launch configuration to preview the app in the Codespace.
- Validate the page renders and that it stays resilient to empty or edge-case project data.

## Dependencies

- Data contract must be agreed before finalizing the HTML.
- HTML structure should be stable before the Designer finalizes CSS selectors and styling details.
- Launch configuration can be created after the `app` folder structure is confirmed, but before final validation.
- The dashboard should not depend on a backend; all project data must be static and local.

## Parallel work decisions

- Parallelizable:
  - Designer can draft the visual system and a CSS mockup while the Coder prepares the JSON schema and the initial HTML skeleton.
  - Coder can create `.vscode/launch.json` once the app folder structure is set, even while visual refinement continues.
- Sequential:
  - Final HTML must be stable before advanced CSS polish.
  - Final data model must be locked before the dashboard is considered complete.
  - Validation should occur only after HTML, CSS, and data files are aligned.

## Edge cases to handle

- Empty project arrays or missing values in `project-data.json`
- Long project names that could overflow cards or wrap awkwardly
- Status values that do not match common categories such as On Track, At Risk, Delayed, or Complete
- Mixed priority labels and inconsistent capitalization
- Very small viewport widths where project cards must stack cleanly
- Color-only status signaling that could cause accessibility issues without text labels or icons

## Validation expectations

- `app/project-data.json` parses successfully as valid JSON.
- The dashboard page loads in a browser without console errors or broken assets.
- All cards render with consistent spacing and readable text.
- Status badges and priority labels remain visually distinct.
- The layout stays usable at mobile, tablet, and desktop widths.
- The `.vscode/launch.json` preview opens the dashboard directly in the app folder instead of a directory listing.
- The dashboard clearly communicates project health at a glance and matches the “Project Pulse” brief.

## Open questions

- Is the dashboard expected to include only example data for the prototype, or does it need to match a larger data source or naming convention already used by Mona’s team?
- Are there required status labels or KPI metrics beyond project health, priority, and completion?
- Should the final dashboard include interactive filtering or remain a static summary page for the initial version?

This plan keeps the implementation scoped, testable, and easy to orchestrate with GitHub Copilot CLI in a Codespace while preserving clear ownership between the Designer and the Coder.
