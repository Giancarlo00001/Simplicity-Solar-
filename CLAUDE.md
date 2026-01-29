# CLAUDE.md — Simplicity Solar

This file provides context for AI assistants working on this repository.

## Project Overview

Simplicity Solar is a **static marketing website** for a Texas-based solar energy company. The site is a lead-generation landing page that collects visitor information through a multi-field form. There is no backend, database, or build system — it is pure HTML/CSS/JavaScript hosted on GitHub Pages with a custom domain (`simplicitysolar.energy`).

## Repository Structure

```
/
├── CNAME            # GitHub Pages custom domain config (simplicitysolar.energy)
├── index.html       # Main website — full landing page with lead capture form
├── testpage.html    # Example/test landing page template
└── CLAUDE.md        # This file
```

- **index.html** (~45 KB): The production landing page. Contains all HTML structure, embedded CSS, and JavaScript in a single file. Sections: hero, how-it-works, benefits, testimonials, lead capture form, contact info, footer, and legal modals (Privacy Policy, Terms & Conditions).
- **testpage.html** (~15 KB): A generic test page used for deployment/layout testing. Not part of the production site.
- **CNAME**: Maps GitHub Pages deployment to `simplicitysolar.energy`.

## Tech Stack

| Layer       | Technology                          |
|-------------|-------------------------------------|
| Markup      | HTML5 (semantic elements)           |
| Styling     | CSS3 (embedded — Grid, Flexbox, animations, media queries) |
| Scripts     | Vanilla JavaScript ES6 (embedded)   |
| Hosting     | GitHub Pages                        |
| Domain      | simplicitysolar.energy (via CNAME)  |
| Build tools | None                                |
| Dependencies| None                                |
| CI/CD       | None — pushes to the default branch deploy automatically via GitHub Pages |

## Development Workflow

### Local Development

No build step required. Open `index.html` directly in a browser or use any local HTTP server:

```sh
# Python
python3 -m http.server 8000

# Node (if npx available)
npx serve .
```

### Deployment

Pushing to the default branch on GitHub automatically deploys via GitHub Pages. The `CNAME` file must remain in the repository root for the custom domain to work.

### Branching

- Feature branches follow the pattern `claude/<description>-<id>` when created by AI assistants.
- Pull requests are merged into the default branch for deployment.

## Code Architecture

### Single-File Pattern

All CSS and JavaScript are embedded directly in `index.html` within `<style>` and `<script>` tags. There are no external stylesheets, script files, or asset directories.

### CSS Conventions

- **Reset**: Universal `* { margin: 0; padding: 0; box-sizing: border-box; }`.
- **Container**: `.container` — max-width 1200px, centered with auto margins and 20px padding.
- **Responsive breakpoint**: `@media (max-width: 768px)` for mobile layouts.
- **Color palette**:
  - Primary greens: `#4CAF50`, `#66BB6A`, `#2E7D32`
  - Accent yellows: `#FFF9C4`
  - Light backgrounds: `#E8F5E9`, `#F1F8E9`
  - Text: `#333`, `#555`, `#666`
- **Gradients**: `linear-gradient(135deg, ...)` used for hero, header, CTA, and footer backgrounds.
- **Animations**: `fadeIn` and `slideUp` keyframes for section entrance effects.
- **Typography**: `'Segoe UI', Tahoma, Geneva, Verdana, sans-serif`.

### JavaScript Conventions

- All code runs in global scope (no modules or bundler).
- **Form handling**: Uses `FormData` API, client-side validation via HTML5 `required` attributes.
- **Phone formatting**: Auto-formats to `(XXX) XXX-XXXX` on input.
- **ZIP validation**: Numeric-only, max 5 digits.
- **Modals**: Toggled via `.show` CSS class; background scroll locked with `document.body.style.overflow`.
- **Smooth scrolling**: Anchor links scroll with 80px offset to account for sticky header.
- **No backend integration**: Form submission currently displays a success modal but does not send data to a server (webhook stub is present but inactive).

### HTML Structure

Sections use semantic elements (`<header>`, `<section>`, `<footer>`) with descriptive `id` attributes for anchor navigation:
- `#how-it-works`
- `#benefits`
- `#testimonials`
- `#contact-form`
- `#contact`

## Key Business Context

- **Company**: Simplicity Solar, Houston, TX
- **Target market**: Texas homeowners
- **Value proposition**: Up to 40% electricity bill savings, $0-down solar installation
- **Lead form fields**: Name, email, phone, address, city, ZIP, home ownership status, monthly electric bill range, roof condition
- **Legal**: Privacy Policy and Terms & Conditions are embedded as modals in the page

## Guidelines for AI Assistants

1. **Keep it static**: Do not introduce build tools, frameworks, or server-side code unless explicitly requested. The simplicity of the stack is intentional.
2. **Inline everything**: CSS and JS belong inside `index.html` unless the user asks to extract them.
3. **Preserve the lead form**: The form is the core conversion mechanism. Any changes to its fields, validation, or layout should be made carefully.
4. **Maintain responsiveness**: All changes must work at both desktop (>768px) and mobile (<=768px) widths.
5. **Color consistency**: Stick to the established green/yellow/white palette. Use the hex values listed above.
6. **CNAME is critical**: Never delete or modify the `CNAME` file — it controls the custom domain.
7. **No secrets in code**: The repository is public. Do not add API keys, webhook URLs, or credentials directly in HTML/JS.
8. **Test visually**: Since there are no automated tests, verify changes by opening the HTML file in a browser.
9. **Commit messages**: Use clear, concise commit messages describing what changed and why.
10. **Legal content**: Privacy Policy and Terms & Conditions text should only be modified with explicit instructions — these have legal implications.
