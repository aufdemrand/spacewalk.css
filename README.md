# Spacewalk CSS: The Official Handbook

Welcome to the official handbook for **Spacewalk CSS**, a simple, modern CSS framework designed for building responsive and highly customizable web applications and user interfaces.

### Table of Contents

1.  [Philosophy & Core Concepts](#philosophy--core-concepts)
2.  [Getting Started](#getting-started)
3.  [Customization & Theming](#customization--theming)
4.  [The Spacewalk Approach to Spacing](#the-spacewalk-approach-to-spacing)
5.  [Layout Elements](#layout-elements)
6.  [Container Components](#container-components)
7.  [When to Use `<div>` and `<span>`](#when-to-use-div-and-span)
8.  [Content & Text Elements](#content--text-elements)
9.  [Utility Classes](#utility-classes)
10. [Special Features](#special-features)
11. [Example Page](#example-page)

-----

### Philosophy & Core Concepts

Spacewalk is built on modern CSS features to provide a developer-friendly experience.

  * **A Foundation, Not a Cage:** Spacewalk is designed to be a **baseline** for your application. It provides sensible defaults and layout tools but intentionally stays out of your way. You are encouraged to write your own CSS to build on top of it. This makes it especially powerful for data-driven applications and interfaces heavy on user input, where custom components are the norm.
  * **Cascade Layers (`@layer`):** The framework's styles are organized into predictable layers (`reset`, `layout`, `containers`, `elements`, `properties`, `slots`, `edge`). This means any custom CSS you write *outside* of a layer will automatically override the framework's styles without needing `!important` or complex selectors.
  * **Deep Customization via Custom Properties:** Nearly every value—colors, fonts, sizes, spacing—is defined as a CSS Custom Property (variable) in the `:root`. Theming is as simple as overriding these variables.
  * **Automatic Dark Mode:** Spacewalk uses the `light-dark()` color function, allowing it to automatically adapt to a user's system preference for light or dark mode. To disable this, simply comment out or remove `color-scheme: light dark;` from the `:root` block in the framework file.
  * **Fluid & Responsive Design:** The framework uses modern functions like `clamp()` for font sizes and page gutters. This allows your UI to scale smoothly with the viewport size, minimizing the need for manual media queries.
  * **Semantic Custom Elements:** Spacewalk provides styles for non-standard but highly semantic tags like `<panel>`, `<flex>`, and `<grid>`, enabling cleaner and more readable HTML structure.

-----

### Getting Started

To use Spacewalk, include the CSS file in your project.

**1. Link in HTML:**

```html
<link rel="stylesheet" href="path/to/spacewalk.css">
```

**2. Import in CSS:**
Place this at the top of your main stylesheet.

```css
@import url('path/to/spacewalk.css');

/* Your custom styles go here */
```

**3. Use a CDN:**
View the latest release at: [https://www.jsdelivr.com/package/gh/aufdemrand/spacewalk.css]

```html
<link rel='stylesheet' href='https://cdn.jsdelivr.net/gh/aufdemrand/spacewalk.css@latest/spacewalk.css'>
```

-----

### Customization & Theming

To customize the theme, override the CSS variables defined in the `:root` block within your own stylesheet.

```css
/* in your-styles.css */
:root {
  /* Change the primary accent color */
  --accent: light-dark(purple, lightpink);

  /* Change the default font family */
  --default-font: 'Inter', sans-serif;

  /* Adjust the default border radius for a softer look */
  --radius: 0.5em;
}
```

#### Key Variable Groups:

  * **Fonts:**
      * `--default-font`: The primary font for the application.
      * `--monospace-font`: Used for `<code>` and `<pre>` elements.
  * **Colors:**
      * **Primary:** `--text`, `--background`, `--accent`, `--inverted`.
      * **UI Elements:** `--header`, `--footer`, `--button`, `--link`.
      * **Indicators:** `--error`, `--danger`, `--success`, `--warning`, `--info`.
      * **Tones:** (`--lite-tone`, `--medium-tone`, etc.) Automatically generated transparent versions of your `--text` color.
      * **Shades:** (`--lite-shade`, `--warning-shade`, etc.) Automatically generated lighter or darker versions of your base colors using the `hsl(from ...)` function.
  * **Sizing & Spacing:**
      * `--base-size`: The root font size (default `16px`). Changing this acts as a global "zoom" for the UI.
      * `--text-size`: The fluid font size for body text.
      * `--page-gutter`: The responsive margin on the left and right of the `<main>` content area.
      * `--padding`, `--margin`, `--gap`, `--radius`: The base values used for spacing and rounding throughout the framework.

-----

### The Spacewalk Approach to Spacing

A core philosophy of Spacewalk is that **spacing should be intentional**. This is achieved by thinking about spacing on two levels: the "macro" layout of the page and the "micro" arrangement of elements within components.

#### Macro Spacing: Structuring the Page 🏗️

This is about creating the major vertical blocks of your application.

  * **`<section>` for Flow:** The `<section>` element is your primary tool for grouping content. By default, it creates a large, responsive vertical margin based on `--page-gutter`.
  * **Controlling Vertical Rhythm:** You have two types of tools for this:
      * **Section Modifiers:** For large-scale changes, use the dedicated `<section>` modifier classes: `.small-margin` and `.big-margin`. These responsive classes are tied to `--page-gutter`.
      * **General Utilities:** For more granular control on any element, use the `.block-margin` family of utilities (`.less-block-margin`, `.block-margin`, `.more-block-margin`, `.way-more-block-margin`). These are based on the standard `--margin` variable.
  * **Managing Content Width:** Inside a full-width `<section>`, use `.constrained` and `.centered` on a child container to keep your content readable on wide screens.

<!-- end list -->

```html
<!-- A section with a very large, responsive top/bottom margin -->
<section class="big-margin text-center">
    <h1 class="xlarge-text constrained centered">App Title</h1>
    <p class="large-text constrained-more centered">A catchy tagline for your amazing app.</p>
</section>

<!-- A standard section that follows -->
<section>
    <!-- A panel with a smaller, fixed margin -->
    <panel class="bordered padded block-margin">...</panel>
</section>
```

#### Micro Spacing: Arranging Components ↔️

This is about arranging items *inside* a component, like a title and buttons on the same line.

  * **Container-Managed Gaps:** The primary way to create space is with container components. `<flex>`, `<grid>`, and `<panel>` all use the `gap` property to apply consistent, predictable spacing *between their children*. This is the recommended approach, as it avoids unpredictable margin-collapsing issues.
  * **Alignment with Justification:** Beyond a simple gap, you often need to align items within the available space. The `.spread` class (`justify-content: space-between`) is your most powerful tool here, pushing the first and last children to the edges of the container. This is perfect for headers and footers.
  * **Unopinionated Elements:** Most base elements like `<button>` and `<input>` have no built-in margins. This gives you complete control, preventing you from ever having to fight the framework's styles. You decide where the space goes, either via a container's `gap` or with precision margin utilities.

<!-- end list -->

```html
<!-- Inside a <panel> component -->
<flex class="spread">
  <h3>User Profile</h3>
  <button>...</button> <!-- "More options" icon button -->
</flex>
```

-----

### Layout Elements

Spacewalk provides styles for standard HTML5 semantic elements to structure your page.

  * **`<header>`:** A flex container pinned to the top. The first child element is automatically pushed to the left, and all subsequent children are pushed to the right.
      * **Modifiers:** `.no-border`, `.thick-border`, `.wide-border`.
  * **`<main>`:** The primary content area for your page, with built-in responsive side margins.
  * **`<footer>`:** A flex container that remains sticky to the bottom of the viewport when content is short.
  * **`<section>`:** A container for grouping related content.
      * **Modifiers:** `.no-margin`, `.small-margin`, `.big-margin` to control vertical spacing between sections.
  * **`<aside>`:** A floated sidebar element. It is designed to be placed inside `<main>` and will float to the right of the content.
  * **`<dialog>`:** A pre-styled modal dialog. It is responsive and collapses to a full-screen element on smaller devices.
  * **`<tray>`:** A custom element for a fixed container at the bottom-right of the screen, perfect for notifications or floating action buttons.

-----

### Container Components

These custom elements are the primary building blocks for your UI content.

#### `<panel>`

A versatile container that uses CSS Grid to stack its children vertically. By default, it applies a standard `gap` between each child, making it perfect for forms and content blocks.

  * **Classes:** `.no-gap`, `.small-gap`, `.big-gap`, `.center` (centers items within the panel).

<!-- end list -->

```html
<panel class="bordered padded">
  <h3>Panel Title</h3>
  <p>This is the content of the panel.</p>
</panel>
```

#### `<flex>`

A powerful and configurable flexbox wrapper. By default, it aligns items vertically to the center and applies a small `gap` between them, making it ideal for arranging items horizontally, like buttons or icons next to text.

  * **Display:** `.inline` to create an `inline-flex` container.
  * **Alignment (Horizontal):** `.spread`, `.left`, `.center`, `.right`.
  * **Alignment (Vertical):** `.top`, `.bottom`, `.fill`.
  * **Sizing:** `.grow`, `.grow-more`, `.shrink`, `.shrink-more`.
  * **Wrapping:** `.wrap`.
  * **Spacing:** `.no-gap`, `.small-gap`, `.big-gap`.

<!-- end list -->

```html
<flex class="spread">
  <h2>Section Title</h2>
  <flex class="small-gap">
    <button>Save</button>
    <button>Cancel</button>
  </flex>
</flex>
```

#### `<grid>`

A responsive CSS Grid wrapper that automatically fits columns based on available space. By default, it uses a standard `gap` for rows and a much larger `gap` for columns, creating clear visual separation in a multi-column layout.

  * **Display:** `.inline` to create an `inline-grid` container.
  * **Column Sizing:** `.wide` (min 30rem), `.narrow` (min 15rem).
  * **Fixed Columns:** `.two-column`, `.three-column`, `.four-column`.
  * **Spacing:** `.no-gap`, `.small-gap`, `.big-gap`.

<!-- end list -->

```html
<grid class="three-column big-gap">
  <panel class="bordered padded">Item 1</panel>
  <panel class="bordered padded">Item 2</panel>
  <panel class="bordered padded">Item 3</panel>
</grid>
```

-----

### When to Use `<div>` and `<span>`

While Spacewalk provides powerful custom elements like `<panel>` and `<flex>`, standard `<div>` and `<span>` tags remain essential tools. In Spacewalk, they are intentionally left as "plain" elements with no default styling, margins, or padding.

  * **Use `<div>` for grouping.** When you need a block-level wrapper purely for organizational purposes—without the flexbox, grid, or gap behavior of a framework component—a `<div>` is the perfect choice. It's the ideal hook for applying a single margin utility or a class like `.constrained` to a group of elements.
  * **Use `<span>` for inline styling.** When you need to target a piece of text *within* a larger block (like a paragraph or heading), `<span>` is the correct tool. It allows you to apply a color, font weight, or utility class to a word or phrase without breaking the flow of the text.

In short: if you need structure and layout, use a Spacewalk component. If you just need a hook for styling, use a `<div>` or `<span>`.

-----

### Content & Text Elements

These elements are used for displaying text and data.

  * **`<p>`:** The standard paragraph element.
      * **Text Wrapping:** Use `.balanced` (or `.balance`), `.stable`, or `.normal` to control how paragraph text wraps for optimal readability.
  * **`<b>` (Badge):** The `<b>` tag is styled as a small, inline badge, perfect for status indicators, counts, or tags.
  * **`<table>`:** A standard data table.
      * **Modifiers:** Use the `.collapsable` class to force the table to its minimum required width.

-----

### Utility Classes

Spacewalk includes a comprehensive set of utility classes for making targeted, one-off adjustments.

| Category | Available Classes |
| :--- | :--- |
| **Borders** | `.bordered`, `.left-border`, `.right-border`, `.top-border`, `.bottom-border`, `.no-border` |
| **Appearance** | `.floating` (shadow), `.info`, `.informational`, `.warning`, `.error`, `.danger`, `.important` (accent bg), `.gray`, `.grey`, `.white`, `.light`, `.transparent` |
| **State** | `.on` (accent outline), `.off` (subtle outline) |
| **Positioning**| `.centered`, `.cleared`, `.clear-left`, `.clear-right` |
| **Sizing** | `.constrained`, `.constrained-less`, `.constrained-more`, `.narrow-width`, `.very-narrow-width` |
| **Text Align** | `.text-left`, `.text-center`, `.text-centered`, `.text-right`, `.text-justify` |
| **Text Style** | `.text-white`, `.text-dark`, `.inverted-text`, `.text-spaced`, `.pretty-text` |
| **Text Size** | `.normal-text`, `.large-text`, `.xlarge-text`, `.xxlarge-text` |
| **Padding** | `.padded`, `.padded-more`, `.padded-less`, `.cozy`, `.cozy-h`, `.cozy-v` |
| **Margins** | `.comfy`, `.comfy-h`, `.comfy-v`, and a full suite of directional margin helpers like `.top-margin`, `.more-top-margin`, etc., for all four directions. |
| **Display** | `.show`, `.hidden`, `.visible`, `.invisible`, `.block`, `.inline`, `.inline-block` |
| **Overflow** | `.inline-overflow` (overflow-x), `.block-overflow` (overflow-y) |
| **Interaction**| `.pointer`, `.interactive` (cursor), `.no-select` |

-----

### Special Features

#### Slots

Slots are a powerful feature for creating complex layouts where a child element needs to "break out" of its parent's padding. This is common for full-bleed images or footers in cards.

  * `.image-slot`: For full-bleed images. Breaks out of all padding and adjusts its own margins.
  * `.top-slot`: Breaks out of the top and side padding of its container.
  * `.bottom-slot`: Breaks out of the bottom and side padding of its container.

<!-- end list -->

```html
<panel class="bordered padded">
  <img class="image-slot" src="https://placehold.co/800x300/purple/white?text=Image+Slot" alt="Header">
  <p class="top-margin">The image above breaks out of the panel's padding.</p>
  <flex class="bottom-slot spread">
      <small>Footer Info</small>
      <a href="#">Details</a>
  </flex>
</panel>
```

#### Loading States

Spacewalk has a built-in, animated loading state that can be applied to almost any element by adding the `loading="true"` attribute. This is incredibly useful for dynamic applications where you need to provide visual feedback during asynchronous operations. Since you're a JavaScript developer, you can easily toggle this attribute.

  * **For block elements (`div`, `panel`, `button`):** Adds a shimmering gradient overlay and disables pointer events.
  * **For `<i>` elements:** Adds a subtle pulsing animation.

<!-- end list -->

````html
<!-- This button will have a shimmer effect -->
<button id="action-btn" loading="true">Processing...</button>

<!-- This entire panel will be disabled with a shimmer -->
<panel id="data-panel" loading="true">
  <h3>Loading Data...</h3>
  <p>Content will appear here shortly.</p>
</panel>
```javascript
// Example of toggling the loading state
const myButton = document.getElementById('action-btn');
myButton.setAttribute('loading', 'true'); // Show loading

// After your async operation completes...
myButton.removeAttribute('loading'); // Hide loading
````

-----

### Example Page

Here is a complete HTML document that demonstrates many of the features of Spacewalk CSS in a practical layout.

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Spacewalk CSS Demo</title>
  
  <!-- Import the default Rubik font -->
  <link rel="preconnect" href="[https://fonts.googleapis.com](https://fonts.googleapis.com)">
  <link rel="preconnect" href="[https://fonts.gstatic.com](https://fonts.gstatic.com)" crossorigin>
  <link href="[https://fonts.googleapis.com/css2?family=Rubik:ital,wght@0,300..900;1,300..900&display=swap](https://fonts.googleapis.com/css2?family=Rubik:ital,wght@0,300..900;1,300..900&display=swap)" rel="stylesheet">
  
  <!-- Link to the Spacewalk CSS file -->
  <link rel="stylesheet" href="spacewalk.css">

  <style>
    /* Example of a simple theme override */
    :root {
        --accent: light-dark(#673AB7, #D1C4E9); /* A nice deep purple */
    }
  </style>
</head>
<body>

  <header>
    <!-- The first child is pushed to the left -->
    <h3>My Application</h3>
    <!-- Subsequent children are pushed to the right -->
    <a href="#">Dashboard</a>
    <a href="#">Profile</a>
    <button>Log Out</button>
  </header>

  <main>
    <section class="text-center">
      <h1 class="xlarge-text no-bottom-margin">Welcome Back</h1>
      <p class="constrained centered balanced">
        This page demonstrates the layout capabilities of the Spacewalk CSS framework.
      </p>
    </section>

    <section class="big-margin">
        <grid class="two-column big-gap">
            
            <panel class="bordered padded">
                <img class="image-slot" src="[https://placehold.co/800x300/673AB7/FFFFFF?text=Spacewalk](https://placehold.co/800x300/673AB7/FFFFFF?text=Spacewalk)" alt="Purple placeholder">
                
                <h3 class="top-margin">User Settings</h3>
                <p>Use the form below to update your information.</p>
                
                <form>
                    <panel class="small-gap">
                        <label for="name">Full Name</label>
                        <input type="text" id="name" placeholder="John Doe">

                        <label for="email">Email Address</label>
                        <input type="email" id="email" placeholder="john.doe@example.com">

                        <flex class="top-margin">
                            <input type="checkbox" id="subscribe">
                            <label for="subscribe">Subscribe to newsletter</label>
                        </flex>
                    </panel>
                </form>
                
                <flex class="bottom-slot spread">
                    <a href="#" class="danger">Delete Account</a>
                    <button class="important">Save Changes</button>
                </flex>
            </panel>

            <panel class="small-gap">
                <panel class="bordered padded">
                    <h3>System Status</h3>
                    <p>All systems are currently operational.</p>
                    <flex class="spread">
                        <b class="success">ONLINE</b>
                        <small>Last checked: 1 minute ago</small>
                    </flex>
                </panel>
                <panel class="bordered padded warning">
                    <h3>Warning</h3>
                    <p>Your subscription is expiring in 7 days.</p>
                </panel>
                <panel id="loading-panel" class="bordered padded" loading="true">
                    <h3>Loading Data...</h3>
                    <p>This panel demonstrates the loading state.</p>
                </panel>
            </panel>

        </grid>
    </section>
  </main>

  <footer class="spread">
    <small>&copy; 2025 Your Company Inc.</small>
    <flex class="small-gap">
        <a href="#">Terms of Service</a>
        <a href="#">Privacy Policy</a>
    </flex>
  </footer>

</body>
</html>
```
