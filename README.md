# IC Workforce Portal — Frontend

A custom-built recruitment and workforce management platform developed for a federal intelligence community agency. The platform serves as the organization's primary staffing initiative, connecting employees across multiple IC components with internal vacancy postings, application workflows, and HR management tools.

**Status:** Phase 1 delivered. Phase 2 in active development.  
**Environment:** Deployed on a classified high-side government network (air-gapped, no external CDN access)  
**Clearance required:** TS/SCI

---

## Overview

The IC Workforce Portal replaced a fragmented, manual hiring process with a unified web application supporting the full candidate lifecycle — from unauthenticated vacancy browsing through application submission, HR screening, manager review, and acceptance or rejection with automated notifications at each stage.

The platform was elevated to a **top-5 strategic priority** for the sponsoring agency and is on roadmap to expand IC-wide.

My role: **Frontend Developer and UI/UX Designer** — responsible for the complete frontend architecture, component system, user flows, wireframes, and ServiceNow portal implementation.

---

## Technical Constraints

Building for a classified high-side network introduced constraints that shaped every technical decision:

- **No external CDNs** — all fonts, icons, and libraries must be locally installed or system-native
- **No JavaScript in the resume builder** — classified network security scanning policies required a pure HTML/CSS implementation; interactivity handled entirely via CSS `:checked` selectors and hidden inputs
- **No AI/ML modules** — JWICS JavaScript restrictions make skills-matching modules non-viable
- **AngularJS 1.x** — ServiceNow Service Portal widget architecture requires AngularJS, not modern Angular
- **WCAG 2.1 AA compliance** — mandatory across all components
- **OWASP zero critical vulnerabilities** — enforced via Azure DevOps CI/CD pipeline
- **99.9% uptime SLA** — 10,000 concurrent users, 2-second load target

---

## Tech Stack

| Layer | Technology |
|---|---|
| Portal framework | ServiceNow Service Portal |
| Widget scripting | AngularJS 1.x |
| Markup | HTML5 |
| Styling | CSS3 / SCSS |
| Client scripting | JavaScript (ES6+) |
| Data handling | JSON / RESTful API integration |
| CI/CD | Azure DevOps |
| Auth | CAC/PIV + PIN (IC PKI) |

---

## Architecture

The platform uses a **ServiceNow hybrid model** — HRSD as the backend workflow engine with a fully custom Service Portal frontend delivering a purpose-built IC design system. The custom frontend is the primary value driver; the out-of-box ServiceNow UI was explicitly rejected in favor of a tailored experience meeting IC-specific UX requirements.

### User Roles

| Role | Access |
|---|---|
| Employee | Browse vacancies, apply, manage applications and profile |
| Manager / Approver | Panel review, interview scheduling |
| HR Manager | Full application pipeline, bulk export, status management |
| IC Admin | Platform configuration, elevated privileges |
| Vacancy Admin / POC | Post and manage vacancies, apply on behalf of candidates |
| Agency POC | Cross-agency coordination |

---

## Design System

The ICJobs design system was built from scratch to meet IC visual standards and WCAG 2.1 AA requirements.

### Color Tokens

```css
/* Core palette */
--slate:   #1B3A4B;   /* Primary nav / header */
--terra:   #C4622D;   /* Primary CTA / action */
--sage:    #3A6B4C;   /* Positive / open status */
--sky:     #1E6FA6;   /* Informational */
--amber:   #B87A1A;   /* Clearance / caution */
--violet:  #5C3D8F;   /* Featured */
--red:     #C13030;   /* Error / closed */

/* Surface */
--bg:         #F4F1EC;
--bg-white:   #FDFCFA;
--border:     #D8D2C8;
```

### Typography

```css
/* Display */
font-family: 'DM Serif Display', 'Georgia', serif;

/* Body */
font-family: 'Plus Jakarta Sans', 'Segoe UI', sans-serif;
```

### Grid

- 8pt base grid
- 1440px max-width, 48px padding
- Two-column layout: `1fr + 300px` sidebar

---

## Key Features

### Phase 1 — Delivered

- **Splash / landing page** — unauthenticated vacancy browsing with keyword search and multi-filter panel (agency, job title, location, type, grade)
- **CAC/PIV authentication flow** — IC PKI integration with silent profile pre-population from certificate DN
- **Employee profile / dashboard** — resume management, application history, account settings
- **Resume builder** — pure HTML/CSS implementation (no JavaScript) with 7-section structured form, sticky sidebar navigation, completion tracking via CSS, and PDF export
- **Vacancy listings** — dynamic filtering, multi-select, real-time result updates
- **Application flow** — pre-populated from profile, cover letter + resume required, SF-50 conditional logic, favorites, withdrawal

### Phase 2 — In Development

- Returning user dashboard
- Candidate pipeline flow (HR screening → manager review → interview → acceptance/rejection)
- Automated email notifications at each status transition (≤5 minute delivery SLA)
- Manager and HR dashboards with bulk export

---

## Notable Implementation Details

**CSS-only resume builder**  
The resume builder required zero JavaScript due to classified network security scanning policies. All interactivity — section toggling, progress tracking, conditional field display — is implemented using CSS `:checked` selectors with hidden checkbox inputs. This was a non-trivial constraint that required rethinking standard form UX patterns entirely.

**Local font fallback chain**  
With no CDN access, every font reference uses a local install first, falling back to system fonts that approximate the design intent. The fallback chain was tested against the specific OS environments present on classified workstations.

**ServiceNow widget architecture**  
Each UI section is implemented as a discrete AngularJS 1.x widget within the ServiceNow Service Portal. Widget-to-widget communication uses ServiceNow's broadcast/on event system rather than shared scope to maintain component isolation.

**Authentication flow**  
CAC/PIV authentication sits at the JWICS network layer. The application receives the authenticated user's PKI Distinguished Name and silently pre-populates name, agency, and email fields on first login, eliminating manual entry of identity fields that are already cryptographically verified.

---

## Repository Contents

```
ic-workforce-portal/
├── README.md
├── tokens.css
├── design-system/
│   └── index.html
├── splash/
│   └── index.html
├── landing/
│   └── index.html
├── search/
│   └── index.html
├── job-detail/
│   └── index.html
└── components/
    ├── component-library.html
    └── component-forms.html
```

---

## Screenshots

*Coming soon — sanitized screenshots of component library and user flows*

---

## Related Work

- **[IRIS Budgeting System](#)** — Angular 17 / TypeScript / Angular Material modernization of a Congressional Hill reporting application for a separate IC agency *(separate repository)*
- **[Federal Digital Infrastructure](#)** — AWS-based secure web infrastructure work *(separate repository)*

---

## Contact

**Jennifer L. Bosworth**  
Frontend Web & Application Developer  
Active TS/SCI | CI Polygraph | CompTIA Security+  
[linkedin.com/in/jennybosworth](https://linkedin.com/in/jennybosworth) · [github.com/JLBosworth](https://github.com/JLBosworth)
