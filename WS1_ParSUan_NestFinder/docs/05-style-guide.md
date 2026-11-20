
# Task 5 – Style Guide
## ParSUan NestFinder

### 1. Color Palette

The website will use a clean and professional color palette to make the interface simple, readable, and comfortable for users.

| Color Purpose | Hex Code | Usage |
|---|---|---|
| Primary | #17324D | Buttons, links, and headings |
| Background | #F7F9FC | Main page background |
| Text | #17212B | Paragraphs, labels, and content |
| Success | #236B45 | Success messages and confirmations |
| Error | #B42318 | Error messages and validation |

### 2. WCAG AA Contrast Check

The main text color (#17212B) against the background color (#F7F9FC) has a contrast ratio of **15.45:1**.

This passes the WCAG AA requirement of at least 4.5:1 for normal-sized text.

Additional contrast checks:

- White text on primary color: 13.13:1 – Pass
- Error color on background: 6.23:1 – Pass
- Success color on background: 6.11:1 – Pass

### 3. Typography

- Heading Font: Poppins
- Body Font: Inter
- Base Font Size: 16px

Poppins will be used for headings because of its clean and modern appearance. Inter will be used for body text, labels, and buttons because it is easy to read.

### 4. UI Components

**Primary Button**
- Navy blue background (#17324D)
- White text
- Rounded corners
- Used for important actions such as searching and saving.

**Secondary Button**
- White or transparent background
- Navy blue border and text
- Rounded corners
- Used for actions such as canceling or going back.

**Text Input**
- Light background
- Visible border
- Rounded corners
- Includes a clear label and placeholder.

**Error Message**
- Red text (#B42318)
- Red border when needed
- Used to display validation errors and missing information.

### 5. CSS Custom Properties

These variables will be placed at the beginning of the shared css/style.css file.

```css
:root {
    /* Color palette */
    --color-primary: #17324D;
    --color-bg: #F7F9FC;
    --color-text: #17212B;
    --color-success: #236B45;
    --color-error: #B42318;

    /* Typography */
    --font-heading: "Poppins", Arial, sans-serif;
    --font-body: "Inter", Arial, sans-serif;

    /* Base font size */
    --font-size-base: 16px;

    /* UI styling */
    --radius: 8px;
    --spacing: 16px;
}
```

### 6. Design Consistency

The same colors, fonts, and component styles will be used throughout the student, owner, and admin pages. This will help maintain a consistent appearance and make the website easier to use.
