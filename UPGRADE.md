# UPGRADE.md

## Overview
Briefly describe the purpose of this file: tracking local modifications to boilerplate files, especially those that may conflict with vendor updates.

---

## Table of Contents# UPGRADE.md

## Overview
Briefly describe the purpose of this file: tracking local modifications to boilerplate files, especially those that may conflict with vendor updates.

---

## Table of Contents

- [General Upgrade Notes](#general-upgrade-notes)
- [Template Override](#template-override)
    - [templates/teams/components/team_invitations.html](#templatesteamscomponentsteam_invitationshtml)
    - [templates/teams/team_membership_details.html](#templatesteamsteam_membership_detailshtml)
    - [templates/web/base.html](#templateswebbasehtml)
    - [templates/web/app/app_base.html](#templateswebappapp_basehtml)
    - [templates/web/app_home.html](#templateswebapp_homehtml)
    - [templates/web/components/app_nav.html](#templateswebcomponentsapp_navhtml)
    - [templates/web/components/footer.html](#templateswebcomponentsfooterhtml)
    - [templates/web/components/messages.html](#templateswebcomponentsmessageshtml)
    - [templates/web/components/team_nav.html](#templateswebcomponentsteam_navhtml)
    - [templates/web/components/top_nav.html](#templateswebcomponentstop_navhtml)
- [## Custom Template](#custom-template)
    - [templates/teams/list_teams.html](#templatesteamslist_teamshtml)
    - [templates/teams/manage_team.html](#templatesteamsmanage_teamhtml)    
- [Merge Conflict History](#merge-conflict-history)
- [Upgrade Checklist](#upgrade-checklist)
- [References & Resources](#references--resources)

---

## General Upgrade Notes

This project uses a vendor boilerplate (SaaS Pegasus) as a foundation. Local customizations are tracked for all templates and files that are likely to conflict with vendor updates.

**Upgrade process:**  
- Review vendor release notes for breaking changes and new features.
- Compare local files against vendor updates, focusing on files listed in "Template Overrides & Customizations".
- Summarize differences and resolutions in this file.
- Resolve conflicts by retaining local business logic and UI improvements, while integrating necessary vendor changes.
- Test all affected features after merging.

---

## Template Override

### templates/teams/components/team_invitations.html

- **Local Changes:**  
  - Added conditional logic to the invitation button:  
    - If team has active Paddle subscription or is under demo user limit, show submit button.
    - Else, show button that opens license modal.
- **Vendor Changes (since last upgrade):**  
  - No changes to this logic; vendor always shows submit button.
- **Merge Resolution Notes:**  
  - Retained local conditional logic to enforce subscription/user limits and provide upgrade prompt via modal.



---

### templates/teams/team_membership_details.html

- **Local Changes:**  
  - Add class="app-card" for styling.
- **Vendor Changes (since last upgrade):**  

- **Merge Resolution Notes:**

---

### templates/web/base.html

- **Local Changes:**  
  - Switched to custom theme CSS and JS:
    - Added links to `theme/css/vendor.min.css`, `theme/vendor/bootstrap-icons/font/bootstrap-icons.css`, and `theme/css/theme.min.css`.
    - Added theme JS: `theme/js/vendor.min.js` and `theme/js/theme.min.js`.
    - Added `{% block theme_js %}` to include additional theme JS partial.
  - Commented out Pegasus Bootstrap CSS and JS (`site-bootstrap.css`, `site-bootstrap-bundle.js`).
  - Added a progress bar (`progress-htmx`) at the top of the body for loading indication.
  - Wrapped main content in a `<main id="content" role="main">` tag.
  - Added `{% block additional %}` to include extra components (e.g., `go-to.html`).
  - Minor formatting and structure changes for clarity and theme integration.
- **Vendor Changes (since last upgrade):**  
  - Uses only Pegasus CSS (`site-base.css`, `site-bootstrap.css`) and JS (`site-bundle.js`, `site-bootstrap-bundle.js`).
  - No theme CSS/JS or progress bar.
  - No `{% block additional %}` or `{% block theme_js %}`.
  - Main content not wrapped in `<main>` tag.
- **Merge Resolution Notes:**  
  - Retained local theme integration and progress bar.
  - Kept vendor meta tag logic and favicon.
  - Ensured all vendor blocks (top_nav, messages, footer, page_js) remain functional and extensible.

---


### templates/web/app/app_base.html

- **Local Changes:**  
  - Added breadcrumb navigation at the top with `{% include "web/components/breadcrumb.html" %}`.
  - Changed container class from `container my-3` to `container-xxl mx-5 mt-lg-n10` for wider layout and custom spacing.
  - Updated grid layout:
    - Sidebar uses `col-lg-3 col-xxl-2` (was `col-auto`).
    - Main content uses `col-lg-9 col-xxl-10` (was `col-md`).
    - Added `d-grid gap-3 gap-lg-5` for spacing between content blocks.
  - Removed `{% block notifications %}`.
- **Vendor Changes (since last upgrade):**  
  - Uses standard Bootstrap grid with `container my-3`, `col-auto` for sidebar, and `col-md` for main content.
  - Includes `{% block notifications %}` at the top of the body.
  - No breadcrumb navigation or custom grid spacing.
- **Merge Resolution Notes:**  
  - Retained local layout and navigation improvements for better UX and responsiveness.
  - Ensured sidebar and main content blocks remain functional and extensible.

---

### templates/web/app_home.html

- **Local Changes:**  
  - Added custom template tags: `primary_stage`, `product_classes_has_no_primary_productivity` from `core_extras`.
  - Changed hero image to `undraw_outer_space.svg` (was `rocket-laptop.svg`).
  - Added a multi-step "Getting started" card with progress steps for:
    - Registering stages and setting a primary stage.
    - Registering product classes and defining characteristics.
    - Creating products.
    - Generating schedules and sharing Gantt charts.
  - Each step includes dynamic badges, tooltips, and links based on user/team data.
  - Added a "Get help" card with links to support and documentation, including SVG icons and descriptions.
- **Vendor Changes (since last upgrade):**  
  - Simple welcome section with static image and basic team info.
  - Basic instructional card referencing the template file location.
  - No dynamic steps, badges, tooltips, or help card.
- **Merge Resolution Notes:**  
  - Retained all local onboarding, progress, and help features for improved user guidance.
  - Ensured vendor welcome and team info remain visible and integrated.

---

### templates/web/components/app_nav.html

- **Local Changes:**  
  - Redesigned sidebar as a vertical navbar inside a card, using Bootstrap classes for layout and styling.
  - Added user avatar, verification badge, display name, and email at the top.
  - Split navigation into sections: Team, Account, and Resource.
    - Team section uses `{% include "web/components/team_nav.html" %}`.
    - Account section includes links for Profile, Licenses, Manage Teams, Security (change password), and Sign out, with Bootstrap Icons.
    - Resource section includes links for Document and Support.
  - Uses Bootstrap Icons (`bi-*`) instead of Font Awesome.
  - Added tooltips and improved visual hierarchy.
- **Vendor Changes (since last upgrade):**  
  - Sidebar uses simple `<aside>` with nav-pills and includes team selector, app menu items, account links, and admin links.
  - No avatar, verification badge, or email display.
  - Uses Font Awesome icons.
  - No dedicated Resource section or support/document links.
- **Merge Resolution Notes:**  
  - Retained local sidebar redesign for improved UX and branding.
  - Ensured all vendor navigation links are present and mapped to new sections.

---

### templates/web/components/footer.html

- **Local Changes:**  
  - Redesigned footer with a horizontal list of links: Contact us, Privacy Statement, Terms of Use.
  - Copyright line uses "©" and shows the current year and project name.
  - Uses Bootstrap utility classes for spacing (`content-space-2`, `list-inline`, etc.).
  - Removed Pegasus branding and translation block.
  - Kept JS to update copyright year.
- **Vendor Changes (since last upgrade):**  
  - Simple footer with project name, copyright, and Pegasus branding.
  - Uses translation for copyright and Pegasus attribution.
  - No contact, privacy, or terms links.
- **Merge Resolution Notes:**  
  - Retained local footer design and navigation links for improved usability and compliance.
  - Ensured copyright year and project name remain dynamic.

---

### templates/web/components/messages.html

- **Local Changes:**  
  - Modified alert messages to use `position-fixed start-50 translate-middle-x` classes for centered, fixed positioning.
  - Set alert width to `60vw` and increased `z-index` for visibility.
- **Vendor Changes (since last upgrade):**  
  - Standard Bootstrap alert messages with dismiss button.
  - No custom positioning or width.
- **Merge Resolution Notes:**  
  - Retained local styling for improved visibility and user experience.
  - Ensured all vendor logic for message rendering and dismiss remains functional.


---

### templates/web/components/team_nav.html

- **Local Changes:**  
  - Expanded team navigation to include:
    - Dashboard link with house icon (`bi-house`).
    - Settings link to manage team (`bi-toggles`).
    - Preferences link for team preferences (`bi-sliders`).
  - Uses Bootstrap Icons (`bi-*`) instead of Font Awesome.
  - Improved naming and iconography for clarity.
- **Vendor Changes (since last upgrade):**  
  - Single link to "Example App" with rocket icon (`fa-rocket`).
  - Uses Font Awesome icons.
  - No dashboard, settings, or preferences links.
- **Merge Resolution Notes:**  
  - Retained local navigation for better team management and user experience.
  - Ensured all vendor navigation logic is replaced or mapped to new links.

---

### templates/web/components/top_nav.html

- **Local Changes:**  
  - Redesigned navigation as a header with custom logo and Bootstrap Icons (`bi-*`).
  - Uses a mega menu structure for dropdowns (Model, Schedule, My Account) with grouped links and icons.
  - Added links for team-specific actions (Stages, Product Classes, Products, Productivity matrix, Schedules).
  - "My Account" dropdown includes profile, change password, sign out, and superuser actions (impersonate, examples gallery).
  - For unauthenticated users, added links for Home, Pricing, Documentation, Contact, and styled Sign up/Login buttons.
  - Improved responsive behavior and visual hierarchy.
- **Vendor Changes (since last upgrade):**  
  - Standard Bootstrap navbar with project name as text.
  - Simple dropdown for account actions, examples gallery, and admin menu.
  - Uses Font Awesome icons.
  - No mega menu, custom logo, or grouped dropdowns.
  - No pricing, documentation, or contact links for unauthenticated users.
- **Merge Resolution Notes:**  
  - Retained local navigation redesign for improved branding, usability, and feature access.
  - Ensured all vendor navigation logic is present or mapped to new structure.


---

## Custom Template


### templates/teams/list_teams.html
### => templates/teams/list_teams_schantt.html

- **Local Changes:**  
  - Added a "License" column to the teams table, showing a key icon with a tooltip for Paddle subscription or demo plan name.
  - Changed "Add Team" button logic:
    - If `user_has_unlimited_subscription`, show regular button to create a team.
    - Else, show button that opens a license modal (`#licenseModal`).
  - Included `{% block additional %}` to render the license modal partial.
  - Minor: Changed button container class from `my-2` to `mt-2`.
- **Vendor Changes (since last upgrade):**  
  - No license column; only "Name" and action columns.
  - "Add Team" button always allows direct team creation.
  - No modal logic or license modal included.
- **Merge Resolution Notes:**  
  - Retained local logic to display license status and restrict team creation based on subscription.
  - Ensured license modal is available for users who hit the team creation limit.
  - Update correct template in teams/views/manage_team_views.py

---

### templates/teams/manage_team.html
### => templates/teams/manage_team_schantt.html

- **Local Changes:**  
  - Added team logo upload and preview functionality, including avatar display and upload button (with tooltip and JS for preview/upload).
  - Added a "License" section with a form to apply or update the team's Paddle subscription.
  - Rendered form fields for team name, slug, and (hidden) Paddle subscription.
  - Included `{% block additional %}` to render a license modal partial.
  - Added custom JS for handling logo uploads.
  - Minor layout changes: used columns for logo and details, kept consistent classes/IDs.
- **Vendor Changes (since last upgrade):**  
  - No logo upload or preview feature.
  - No "License" section or Paddle subscription form.
  - Only renders basic team details and members, with invitation and delete modal for admins.
- **Merge Resolution Notes:**  
  - Retained all local enhancements for logo upload, license management, and improved layout.
  - Ensured vendor features (team details, members, invitations, danger zone) remain functional and integrated with new features.
  - Update correct template in teams/views/manage_team_views.py

---


## Merge Conflict History

- Track significant merge conflicts here, including:
  - Date of conflict
  - File(s) affected
  - Summary of resolution (e.g., "Retained local logic for license modal, merged vendor bugfix for invitation form.")
  - Optionally, include git commit hashes or PR links for reference.

**Example:**
- 2025-07-14: `templates/teams/components/team_invitations.html` – Resolved logic conflict, kept local subscription check, merged vendor translation update.


---

## Upgrade Checklist

- [ ] Review vendor release notes
- [ ] Compare local vs vendor changes for tracked files
- [ ] Update this file with new differences and resolutions
- [ ] Test all affected features
- [ ] Document any new conflicts or customizations

---

## References & Resources

- [SaaS Pegasus Documentation](https://www.saaspegasus.com/docs/)
- [Django Upgrade Guide](https://docs.djangoproject.com/en/stable/releases/)
- [Bootstrap Documentation](https://getbootstrap.com/docs/)
- Internal notes, PRs, or issue trackers as needed