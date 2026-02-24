---
name: rapid-prototype
description: "Build UI prototypes using the zero-build HTML system $ARGUMENTS"
---

# Rapid Prototype Skill

## Overview

Build interactive UI prototypes in seconds using a zero-build HTML prototyping system. No npm, no webpack, no waiting. Edit → Save → Refresh = 2 seconds.

**Source Kit Location:** `[YOUR_PROTOTYPE_TEMPLATES_PATH]/`

## When to Use This Skill

- Creating interactive mockups for stakeholder review
- Validating UI concepts quickly
- Testing user flows before implementation
- Building throwaway demos for presentations
- Documenting design patterns

## Invocation

```
/rapid-prototype "Create a user management screen with search, add button, and user list with actions"
```

Or natural language:
- "Build a prototype for..."
- "Create a quick mockup of..."
- "Prototype the..."

---

## Workflow: Single Agent (Default)

For straightforward prototypes (1-3 sections, <10 components):

### Step 1: Parse Requirements

Extract from the user's brief:
- **Page title** - What is this screen called?
- **Components needed** - Buttons, cards, lists, forms, tabs, modals?
- **Layout structure** - Header? Sidebar? Main content sections?
- **Interactivity** - Tabs? Modals? Filters? Form validation?

### Step 2: Read Source Materials

```
Read: [YOUR_PROTOTYPE_TEMPLATES_PATH]/blank_prototype_template.html
Read: [YOUR_PROTOTYPE_TEMPLATES_PATH]/DesignSystem.html
```

### Step 3: Assemble Prototype

1. Copy `blank_prototype_template.html` structure
2. Update `<title>` and main heading
3. Replace main content area with assembled components
4. Add any required JavaScript interactions
5. Save to user's working directory

### Step 4: Deliver

```bash
# macOS - Open in browser
open [prototype_filename].html
```

Provide user with:
- File path
- Key interactions to test
- Suggested iterations

---

## Workflow: Parallel Agents (Complex Prototypes)

For complex prototypes (4+ sections, 10+ components, multiple interactions):

**Spawn parallel agents using Task tool with these specialized roles:**

### Agent 1: Layout Architect
**Prompt:**
```
You are building a prototype. Your job: CREATE THE PAGE STRUCTURE.

Read: [YOUR_PROTOTYPE_TEMPLATES_PATH]/blank_prototype_template.html

Task: Build the HTML skeleton for [DESCRIBE LAYOUT]
- Keep the full <head> section with Tailwind config
- Keep header and sidebar from template
- Create empty placeholder sections in <main> with comments like:
  <!-- SECTION: User List -->
  <!-- SECTION: Filter Bar -->
- Do NOT add component details yet

Output: The complete HTML file with placeholder sections.
```

### Agent 2: Component Extractor
**Prompt:**
```
You are extracting components from the design system.

Read: [YOUR_PROTOTYPE_TEMPLATES_PATH]/DesignSystem.html

Task: Extract and adapt these components: [LIST COMPONENTS]

For each component:
1. Find it in DesignSystem.html
2. Copy the markup
3. Adapt content/labels for the use case
4. Ensure focus-ring class on all interactive elements

Output: A markdown document with each component's adapted HTML, ready to paste.
```

### Agent 3: Interaction Engineer
**Prompt:**
```
You are adding JavaScript interactivity to a prototype.

Reference patterns from: [YOUR_PROTOTYPE_TEMPLATES_PATH]/CLAUDE.md

Task: Write vanilla JavaScript for: [LIST INTERACTIONS]
- Tabs switching
- Modal open/close
- Form validation
- Filter/search functionality
- Checkbox selection states

Rules:
- Vanilla JavaScript only (no frameworks)
- Use event delegation for lists
- All JS goes at end of <body> in single <script> block

Output: Complete <script> block ready to paste.
```

### Agent 4: Accessibility Validator
**Prompt:**
```
You are validating accessibility for a prototype.

Reference: [YOUR_PROTOTYPE_TEMPLATES_PATH]/CLAUDE.md (Accessibility section)

Task: Review this HTML and provide fixes:
[PASTE ASSEMBLED HTML]

Check for:
- focus-ring class on ALL interactive elements
- ARIA attributes (aria-label, aria-current, aria-expanded)
- Semantic HTML (<nav>, <main>, <header>, proper heading hierarchy)
- Alt text on images (empty alt="" with aria-hidden="true" for decorative)
- Skip link at top of page

Output: List of issues with corrected HTML snippets.
```

### Assembly (After Parallel Agents Complete)

1. Take Layout Architect's skeleton
2. Insert Component Extractor's components into placeholder sections
3. Add Interaction Engineer's <script> block
4. Apply Accessibility Validator's fixes
5. Save and test

---

## Component Reference (Quick Lookup)

### Navigation
- **Breadcrumb** - Page hierarchy trail
- **Link** - Text links with optional icons
- **Header** - Top navigation bar
- **Tabs** - Bordered or pill variants
- **Menu** - Action menus (Edit, Delete, etc.)

### Forms
- **Input** - Text, search, number variants
- **Checkbox** - Single or group
- **Radio** - Radio button groups
- **Form Field** - Label + input + helper text
- **Date Picker** - Date/time selection
- **File Upload** - File input with preview

### Actions
- **Button** - Primary, Secondary, Tertiary, Destructive
- **Action Bar** - Bulk action toolbar
- **Filter Button** - Filter toggle
- **Filter Tag** - Active filter chip

### Display
- **Card** - Basic, interactive, stat card
- **List Item** - Entity rows with avatars
- **Avatar** - User/entity images
- **Badge** - Status indicators
- **Type Label** - Category labels

### Feedback
- **Banner** - Info/warning/error messages
- **Dialog** - Modal dialogs
- **Empty States** - No data views

### Layout
- **Accordion** - Collapsible sections
- **Carousel** - Horizontal scroll

---

## Design Tokens (Pre-Configured)

### Colors
```
accent: #675DF4 (primary brand)
accent-hover: #746BF5
accent-pressed: #564BE7
surface-text: #1f2533 (default text)
surface-text-weak: #545f70 (secondary text)
negative: #A8242A (destructive/error)
positive: #00875a (success)
```

### Spacing (4px Scale)
```
s1: 4px   s2: 8px   s3: 12px
s4: 16px  s5: 20px  s6: 24px  s8: 32px
```

### Typography
```
text-headline-small: 20px/28px, SemiBold
text-title-medium: 16px/24px, SemiBold
text-title-small: 14px/20px, SemiBold
text-label-medium: 14px/20px, Medium
text-body-small: 14px/20px, Regular
```

### Border Radius
```
rounded-xsmall: 4px
rounded-small: 8px (rounded-sm in template)
rounded-medium: 12px (rounded-md in template)
rounded-full: 9999px
```

---

## Common Patterns

### Tabs
```html
<div class="flex gap-2 border-b border-surface-border-weak">
  <button class="tab-btn px-s4 py-s2 text-label-medium border-b-2 border-accent text-accent" data-tab="tab1">Tab 1</button>
  <button class="tab-btn px-s4 py-s2 text-label-medium border-b-2 border-transparent text-surface-text-weak hover:text-surface-text" data-tab="tab2">Tab 2</button>
</div>
<div id="tab1" class="tab-content py-s4">Content 1</div>
<div id="tab2" class="tab-content py-s4 hidden">Content 2</div>

<script>
document.querySelectorAll('.tab-btn').forEach(btn => {
  btn.addEventListener('click', () => {
    const target = btn.dataset.tab;
    document.querySelectorAll('.tab-content').forEach(t => t.classList.add('hidden'));
    document.getElementById(target).classList.remove('hidden');
    document.querySelectorAll('.tab-btn').forEach(b => {
      b.classList.remove('border-accent', 'text-accent');
      b.classList.add('border-transparent', 'text-surface-text-weak');
    });
    btn.classList.add('border-accent', 'text-accent');
    btn.classList.remove('border-transparent', 'text-surface-text-weak');
  });
});
</script>
```

### Modal
```html
<div id="my-modal" class="fixed inset-0 z-50 hidden bg-black/50">
  <div class="fixed inset-0 flex items-center justify-center p-4">
    <div class="bg-white rounded-md shadow-large p-s6 max-w-lg w-full">
      <h2 class="text-headline-small mb-s4">Modal Title</h2>
      <p class="text-body-small text-surface-text-weak mb-s6">Modal content here.</p>
      <div class="flex justify-end gap-s3">
        <button onclick="closeModal('my-modal')" class="focus-ring px-s4 py-s2 rounded-sm text-label-medium text-surface-text hover:bg-surface-hover">Cancel</button>
        <button class="focus-ring px-s4 py-s2 rounded-sm bg-accent text-white hover:bg-accent-hover text-label-medium">Confirm</button>
      </div>
    </div>
  </div>
</div>

<script>
function openModal(id) { document.getElementById(id).classList.remove('hidden'); }
function closeModal(id) { document.getElementById(id).classList.add('hidden'); }
</script>
```

### Button Variants
```html
<!-- Primary -->
<button class="focus-ring px-s4 py-s2 rounded-sm bg-accent text-white hover:bg-accent-hover text-label-medium">Primary</button>

<!-- Secondary -->
<button class="focus-ring px-s4 py-s2 rounded-sm border border-surface-border text-surface-text hover:bg-surface-hover text-label-medium">Secondary</button>

<!-- Tertiary -->
<button class="focus-ring px-s4 py-s2 rounded-sm text-accent hover:bg-accent-weak text-label-medium">Tertiary</button>

<!-- Destructive -->
<button class="focus-ring px-s4 py-s2 rounded-sm bg-negative text-white hover:bg-negative-hover text-label-medium">Delete</button>
```

### Search Input
```html
<div class="flex items-center gap-s2 h-10 w-80 rounded-sm border border-surface-border bg-white px-s3">
  <svg class="w-4 h-4 text-surface-text-weak" fill="none" viewBox="0 0 24 24" stroke="currentColor">
    <circle cx="11" cy="11" r="8"/><path d="m21 21-4.35-4.35"/>
  </svg>
  <input type="search" placeholder="Search..." class="flex-1 text-body-small outline-none" />
</div>
```

---

## Output Checklist

Before delivering prototype, verify:

- [ ] `<title>` updated to match prototype name
- [ ] Main `<h1>` heading updated
- [ ] All interactive elements have `focus-ring` class
- [ ] Semantic HTML used (`<nav>`, `<main>`, `<header>`)
- [ ] Skip link present at top of body
- [ ] All SVG icons have `aria-hidden="true"`
- [ ] JavaScript is vanilla (no frameworks)
- [ ] File saved with descriptive name (e.g., `user_management_prototype.html`)

---

## Figma Integration

If user provides a Figma URL, use Figma MCP tools:

```
mcp__figma__get_design_context - Extract design details
mcp__figma__get_screenshot - Get visual reference
```

Map Figma designs to available components from DesignSystem.html.

---

## Example Invocations

**Simple:**
```
/rapid-prototype "Create a settings page with tabs for Profile, Security, and Notifications"
```

**Detailed:**
```
/rapid-prototype "Build a task management prototype with:
- Header with breadcrumbs (Home > Projects > My Tasks)
- Filter bar with status dropdown and search
- Task list with checkboxes, priority badges, due dates
- Each task row clickable to open detail modal
- Bulk action bar when tasks selected"
```

**From Figma:**
```
/rapid-prototype from https://www.figma.com/design/abc123/MyDesign?node-id=123-456
```
