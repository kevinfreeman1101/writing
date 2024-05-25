# Bootstrap 5 Profile Page

## Query

I want a nice looking Profile web page that uses Bootstrap 5 and complies with the current WCAG accessibility standard. The main page should feature a profile image centered in the page; there should be a navigation bar with links to a Projects page (a Bootstrap grid of demo projects), a Publications page showing 2 published books, a Reading Corner for recommended reading and free book downloads, and a Code page for users to check out a selection of functional Jupyter Notebooks demonstrating Python data visualization; and all pages should have a footer with contact links, social media icons, and a toggle button for changing the color scheme from dark-high-contrast mode (the page's default scheme) to a light-high-contrast solar color scheme. Format your response as a tutorial in Markdown format and be sure to give instructions for installation of npm, node, and sass so readers can follow along.

## Codegemma Response

### Bootstrap 5 Profile Page with Accessibility and Color Scheme

This tutorial will guide you through the process of building a Bootstrap 5 profile page that is WCAG compliant and features a toggle color scheme.

**Step 1: Install Dependencies**

```
npm install bootstrap@5 sass
npm install --save-dev sass-loader node-sass
```

**Step 2: Create Files**

Create the following files:

- `index.html`
- `style.scss`
- `projects.html`
- `publications.html`
- `reading_corner.html`
- `code.html`

**Step 3: Design and Code**

**index.html:**

```html
<!-- Header -->
<header>
  <nav class="navbar navbar-expand-lg navbar-dark bg-dark">
    <!-- Navigation links -->
  </nav>
</header>

<!-- Profile image -->
<div class="container mt-4">
  <img src="profile.jpg" alt="Profile Image" class="img-fluid mx-auto d-block">
</div>

<!-- Content -->
<div class="container mt-4">
  <!-- Links to other pages -->
</div>

<!-- Footer -->
<footer class="bg-dark text-white text-center p-3">
  <!-- Contact links, social media icons, color scheme toggle -->
</footer>
```

**style.scss:**

```scss
// Custom styles for the page
```

**Step 4: Configure Color Scheme Toggle**

- Create a JavaScript function to toggle between light and dark color schemes.
- Use Bootstrap classes to apply the appropriate theme to the header, footer, and body.

**Step 5: Accessibility Compliance**

- Ensure all text has appropriate font size, line height, and contrast ratio.
- Use alt text for images.
- Implement keyboard navigation and focus states.

**Step 6: Build and Run**

- Run `npm run sass` to compile sass files.
- Open `index.html` in a browser to view the profile page.

**Tips:**

- Use Bootstrap classes for consistent and responsive design.
- Use a code editor with syntax highlighting for easier coding.
- Test your page with different screen readers and browsers.

**Note:** This is a basic framework, and you can customize the design and content further to create your desired profile page.
