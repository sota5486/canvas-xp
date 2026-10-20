# canvas-xp
# Canvas XP

**Turn academic progress into rewards.**

Canvas XP is a student-focused web application designed to encourage better time management by rewarding students with XP tokens for submitting assignments early or within 24 hours of their due dates. Students can use earned tokens to customize avatars, unlock virtual incentives, and personalize the appearance of their Canvas experience.

Participation is completely optional, and the system does not affect course grades.

## Table of Contents

- [Project Overview](#project-overview)
- [Project Goals](#project-goals)
- [Key Features](#key-features)
- [System Architecture](#system-architecture)
- [Technology Stack](#technology-stack)
- [Project Structure](#project-structure)
- [XP Award System](#xp-award-system)
- [Security and Privacy](#security-and-privacy)
- [Development Roadmap](#development-roadmap)
- [Getting Started](#getting-started)
- [Testing](#testing)
- [Project Status](#project-status)
- [Team Collaboration](#team-collaboration)

## Project Overview

Canvas XP aims to make completing coursework more engaging by introducing a reward system connected to Canvas assignment activity.

The application uses read-only Canvas access to retrieve course, assignment, and submission information. A backend service verifies this information and determines whether a student qualifies for XP rewards.

Students can then view their XP balance, purchase virtual items, customize avatars, and unlock supported Canvas interface changes.

The project uses a hybrid architecture consisting of a web application, a Chrome extension, Supabase backend services, and a Canvas integration.

## Project Goals

- Encourage students to submit assignments on time or early.
- Make academic progress more engaging through virtual rewards.
- Allow students to personalize their Canvas experience.
- Provide a secure and reliable method of calculating XP.
- Protect student information and maintain read-only access to Canvas.
- Support development and testing through mock Canvas data.
- Deliver a functional pilot version by the end of the Spring semester.

## Key Features

### XP Rewards
- Award XP for eligible assignment submissions.
- Calculate rewards using verified Canvas data.
- Maintain a record of earned and spent XP tokens.
- Display student balances and reward history.

### Virtual Store and Customization
- Purchase avatars and virtual incentives using XP.
- Customize supported aspects of the Canvas interface.
- Unlock additional visual features through earned points.
- Explore future reward options, including boosters.

### Canvas Integration
- Connect to Canvas through a server-managed OAuth 2.0 authorization flow.
- Retrieve courses, assignments, and submissions using read-only access.
- Display assignment due-date countdowns through a Chrome extension.
- Use backend data to display XP balances and unlocked features.

### Student Privacy
- Make participation opt-in.
- Provide consent and onboarding controls.
- Support account disconnection and data deletion.
- Keep the reward system separate from course grades.

## System Architecture

Canvas XP uses a hybrid architecture that separates data collection, reward calculations, storage, and user interface functionality.

| Component | Responsibility |
|---|---|
| Canvas OAuth 2.0 | Authorizes read-only access and enables the server to retrieve Canvas data. |
| Supabase | Stores XP records, purchases, avatars, boosters, and consent information. |
| Supabase Edge Functions | Handle server-side authorization callbacks, synchronization, and XP award calculations. |
| Web Application | Provides the dashboard, virtual store, avatar customization, and onboarding experience. |
| Chrome Extension | Displays countdowns, XP information, and supported Canvas interface customizations. |
| Mock Canvas Fixtures | Provide simulated courses, assignments, and submissions for development and testing. |

### How the System Works

1. A student opts in and authorizes Canvas access.
2. The server retrieves relevant Canvas course, assignment, and submission information.
3. The backend verifies eligibility and calculates XP.
4. The resulting XP transactions are stored in Supabase.
5. The web application displays the student's balance, purchases, and available rewards.
6. The Chrome extension displays supported information and interface customizations.

**Important:** XP must be calculated and awarded by trusted backend services. Neither the web application nor the Chrome extension should be able to directly grant XP.

## Technology Stack

The proposed technology stack includes:

- **Frontend:** Web technologies appropriate to the existing application.
- **Browser Integration:** Chrome Extension using Manifest V3.
- **Backend and Database:** Supabase.
- **Server-Side Processing:** Supabase Edge Functions.
- **Canvas Integration:** Canvas LMS API with OAuth 2.0 authorization.
- **Testing:** Automated tests, mock Canvas fixtures, and integration testing.
- **Version Control:** Git and GitHub.

The exact frontend framework, package manager, and development commands should be confirmed by reviewing the existing repository files.

## Project Structure

The repository currently follows a monorepo-style layout.

```text
Canvas-XP/
├── apps/                 # Application projects
├── packages/             # Shared packages and Canvas integration
├── supabase/             # Database and backend functions
├── docs/                 # Project documentation
├── temp-web-app/         # Temporary web application
├── .github/              # GitHub configuration and workflows
├── manifest.json         # Chrome extension configuration
├── content.js            # Canvas extension content script
└── README.md             # Project documentation
```

*Note: This structure is based on the initial repository review. Existing files and directories should be inspected before adding or reorganizing components.*

## XP Award System

The XP engine determines whether a submission qualifies for a reward.

The proposed eligibility window includes assignments submitted early or within 24 hours of their due dates. The precise reward amounts, handling of late submissions, resubmissions, missing due dates, and other edge cases must be finalized by the team.

The award process should:

1. Retrieve submission and assignment information from Canvas.
2. Compare the submission timestamp with the assignment due date.
3. Apply the agreed XP eligibility and reward rules.
4. Prevent duplicate awards for the same eligible submission.
5. Record each award in the XP ledger.
6. Update the student's balance through trusted backend logic.

The XP engine should be tested against mock data before connecting to live Canvas accounts.

## Security and Privacy

Security is a core requirement of Canvas XP because the application interacts with student academic information.

- **Read-only access:** Request only the Canvas permissions necessary for the project.
- **Server-side verification:** Retrieve and verify assignment submissions on the server rather than trusting browser requests.
- **Protected credentials:** Keep OAuth secrets and sensitive tokens out of client-side code and GitHub.
- **Encrypted token storage:** Protect stored authorization tokens using appropriate encryption and key management.
- **Database security:** Configure Supabase Row Level Security (RLS) policies for every table containing protected application data.
- **Opt-in participation:** Obtain consent before connecting student accounts.
- **Account controls:** Provide appropriate disconnection and data-deletion functionality.
- **Repository hygiene:** Remove accidentally committed local paths and avoid committing personal information, secrets, or environment files.

The project should also be reviewed for privacy, accessibility, and institutional requirements before a student pilot begins.

## Development Roadmap

The roadmap targets a functional pilot by the end of the Spring semester. The exact calendar dates and task owners should be confirmed by the team.

| Phase | Focus | Target | Main Deliverables |
|---|---|---|---|
| 0 | Planning and Cleanup | Initial phase | Agreed architecture, repository cleanup, README, GitHub Issues board, Canvas developer key request |
| 1 | Canvas Data Layer | October–November | Shared Canvas client and mock data fixtures |
| 2 | XP Engine | October–December | Finalized reward rules, tested XP calculation, Supabase schema |
| 3 | Backend | January | Edge Functions, scheduled synchronization, consent, deletion, and disconnection endpoints |
| 4 | Web Application | January–February | Dashboard, virtual store, avatars, boosters, and onboarding |
| 5 | Chrome Extension | March | Canvas customization, background worker, and settings popup |
| 6 | Testing and Finalization | April | Automated tests, CI, security review, pilot, accessibility improvements, demo, and documentation |

Phases 0–2 can overlap because the Canvas data layer and XP engine can be developed independently using mock fixtures.

## Getting Started

### Prerequisites

Before setting up the project, confirm that you have:

- Git installed.
- Node.js and npm if required by the selected application packages.
- Access to the Canvas XP GitHub repository.
- A Supabase project for backend development, if applicable.
- Access to mock Canvas fixtures or the project's development data.
- A Canvas developer key and institutional approval for live OAuth integration, when required.

### Installation

Clone the repository:

```bash
git clone <repository-url>
cd <repository-folder>
```

Inspect the repository and locate the application you intend to run:

```bash
ls
```

Install dependencies using the package manager and instructions associated with the relevant application. For an npm-based application, this may involve:

```bash
npm install
```

Configure environment variables using the project's example environment file, if available. Never commit actual secrets or `.env` files.

**Setup status:** Complete application-specific run commands, database migration instructions, and environment variable names still need to be documented after reviewing the existing application and Supabase files.

## Testing

Testing should cover the main application components and their interactions.

Recommended test areas include:

- Canvas API client behavior.
- Mock and live Canvas data compatibility.
- XP eligibility and calculation rules.
- Duplicate-award prevention.
- XP ledger and balance consistency.
- Supabase database access and RLS policies.
- OAuth authorization and account disconnection.
- Chrome extension countdown and display behavior.
- Web dashboard, store, and avatar customization.
- Accessibility and end-to-end workflows.

Development should use mock Canvas fixtures whenever live institutional access is unavailable.

## Project Status

Canvas XP is in the planning and development stage, with an existing repository and an initial Chrome extension prototype.

The proposed hybrid architecture, backend integration, XP engine, web application, and final pilot still require implementation or verification.

The current review covered the repository front page, README, `manifest.json`, and `content.js`. Other directories have not yet been fully reviewed, so their implementation status remains unverified.

### Initial Priorities

- [ ] Finalize the hybrid architecture and XP rules.
- [ ] Assign owners and statuses to roadmap tasks.
- [ ] Request the required Canvas developer key.
- [ ] Review and clean up the repository.
- [ ] Document application-specific installation and run commands.
- [ ] Implement the shared Canvas client and mock fixtures.
- [ ] Develop and test the server-side XP engine.
- [ ] Implement Supabase security policies and backend functions.
- [ ] Build the dashboard, virtual store, and avatar system.
- [ ] Integrate the Chrome extension with the backend.
- [ ] Complete testing, accessibility review, and pilot preparation.

## Team Collaboration

The team should use GitHub Issues and project tracking to assign responsibilities, record progress, and resolve outstanding questions.

When contributing:

1. Review existing issues and project documentation.
2. Create or select an issue describing the task.
3. Coordinate ownership and expected outcomes with the team.
4. Create a feature branch when appropriate.
5. Implement and test the changes.
6. Submit a pull request for review.
7. Update the issue and project documentation when the work is complete.

Important architectural and scope decisions should be recorded in the project's decision log so the team has a shared reference.

## License

A project license has not yet been specified. Add a license once the team has agreed on the terms for sharing and reusing the project.

---

**Canvas XP — Making academic progress more engaging, one submission at a time.**
