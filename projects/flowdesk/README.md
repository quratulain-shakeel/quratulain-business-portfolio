# FlowDesk — project delivery workspace

A functional, browser-based project management application created with AI assistance for Quratulain Shakeel’s business portfolio.

**[Launch FlowDesk](https://quratulain-shakeel.github.io/quratulain-business-portfolio/projects/flowdesk/)** · **[Portfolio](https://quratulain-shakeel.github.io/quratulain-business-portfolio/)**

## What you can do

- Create multiple projects with objectives, currencies and budgets.
- Plan tasks with owners, acceptance criteria, estimated and actual costs.
- Move tasks across To do, In progress, Review and Done.
- Set dependencies; unfinished predecessors block starting or completing successors. Circular dependencies are rejected.
- View a calendar-day timeline and overdue work.
- Prioritize risks using probability × impact and record responses.
- Review change requests with cost and schedule impacts and a decision rationale.
- Monitor completion, recorded spending, remaining approved budget and open risks.
- Export/import JSON backups and download a Markdown status report.

The Gul Bakes workspace contains **synthetic practice data**, not measured business results. Every visitor receives their own browser-local workspace.

## Start in two minutes

1. Open the live app and explore the demo.
2. Choose **+ New project** to record your own objective and budget.
3. Add tasks, acceptance criteria and dependencies.
4. Update actual costs and task status as you complete real work.
5. Export a backup after each session. Work is saved only in this browser.

See [PRACTICE_GUIDE.md](PRACTICE_GUIDE.md) for a practical project and evidence checklist, and [LINKEDIN.md](LINKEDIN.md) for an editable announcement.

## Run locally

No installation or build step is required for the website. Serve this directory with a local HTTP server (ES modules need HTTP):

```sh
python -m http.server 8000
```

Then open `http://localhost:8000`. From the repository root, open `http://localhost:8000/projects/flowdesk/` instead.

For the domain-logic tests, use Node.js 22 or later from this directory:

```sh
npm test
```

## Architecture

| File | Responsibility |
| --- | --- |
| index.html | Accessible navigation, dialogs and app shell |
| styles.css | Responsive dashboard, board and timeline |
| app.js | UI rendering, forms, local persistence and downloads |
| core.js | Dependency validation, budget metrics and backup validation |
| tests.mjs | Domain rules and backup regression tests |

Plain HTML, CSS and JavaScript modules. No third-party runtime libraries, analytics, external fonts or backend. Deployment uses the repository’s existing GitHub Pages configuration.

## Calculation rules

Completion = completed task count / total task count, rounded to a whole percent. This is not earned value or effort-weighted progress. Actual cost is the sum of task actual costs. Approved budget = original budget + approved change amounts; pending/rejected requests do not affect it. Remaining budget = approved budget − actual cost. Risk scores use integer probability and impact values from 1 to 5; scores 12–25 are high, 6–11 medium, 1–5 low. Overdue means an unfinished task due before the browser’s local date.

Task dates are manually scheduled. Dependencies govern status, not automatic rescheduling or critical-path calculation. Schedule impacts on change requests are recorded but must be applied to task dates manually. Currency changes are blocked after tasks or changes exist; there is no exchange-rate conversion.

## Data and limitations

- Single-user local application, not a multi-user service. No accounts, cloud sync, notifications, real approval routing or server-side access control.
- Browser storage can be cleared or unavailable. Use **Export backup** regularly; importing appends copies and preserves existing projects.
- Maximum 30 projects, 500 tasks/project, 200 risks and 200 changes/project, and 5 MB per imported backup. Activity retains the newest 200 events and is not a tamper-proof audit trail.
- Reviewed change requests are read-only in the UI. Revise through a new compensating request. Local data can still be edited outside the app.
- Opening another browser/device creates a separate workspace. Transfer work with a JSON backup. Avoid simultaneous edits in multiple tabs.
- Project data remains on the device unless you export/share it. Use fictional or non-confidential information when demonstrating the app.

## Development roadmap

Possible future extensions: database-backed accounts, team roles and real approval routing, automated scheduling, attachments, and accessible drag-and-drop with keyboard alternatives. These are not implemented in this release.

## Portfolio attribution

This is an AI-assisted software project. The owner can demonstrate project-management skills by using it to plan and deliver real work, recording decisions and explaining results. The demo is not evidence of employment, client delivery or achieved business savings.
