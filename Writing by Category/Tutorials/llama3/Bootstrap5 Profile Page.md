# Bootstrap 5 Profile Page

## Query

I want a nice looking Profile web page that uses Bootstrap 5 and complies with the current WCAG accessibility standard. The main page should feature a profile image centered in the page; there should be a navigation bar with links to a Projects page (a Bootstrap grid of demo projects), a Publications page showing 2 published books, a Reading Corner for recommended reading and free book downloads, and a Code page for users to check out a selection of functional Jupyter Notebooks demonstrating Python data visualization; and all pages should have a footer with contact links, social media icons, and a toggle button for changing the color scheme from dark-high-contrast mode (the page's default scheme) to a light-high-contrast solar color scheme. Format your response as a tutorial in Markdown format and be sure to give instructions for installation of npm, node, and sass so readers can follow along.

## llama3 Response

### Tutorial: Creating an Accessible Profile Web Page with Bootstrap 5 and WCAG Compliance

#### Prerequisites

* Install Node.js (if you don't have it installed) by downloading the installer from [nodejs.org](http://nodejs.org).
* Install npm (Node Package Manager) by running `npm install -g` in your terminal.
* Install Sass (Syntactically Awesome StyleSheets) by running `npm install -g sass` in your terminal.

#### Step 1: Create a New Project

Create a new project folder for your web page and navigate to it in the terminal:
```bash
mkdir my-profile-page
cd my-profile-page
```
#### Step 2: Install Bootstrap 5 and other dependencies

Install Bootstrap 5, Popper.js (for tooltips and popovers), and jQuery (for JavaScript functionality) using npm:
```bash
npm install bootstrap@5.1.3 popper.js@1.16.0 jquery@3.6.0
```
#### Step 3: Create the HTML Structure

Create a new file called `index.html` in your project folder:
```html
<!-- index.html -->
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>My Profile Page</title>
    <link rel="stylesheet" href="styles.css"> <!-- will be created in Step 4 -->
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.1.3/dist/js/bootstrap.min.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/jquery@3.6.0/dist/jquery.min.js"></script>
</head>
<body>
    <!-- will be filled in later -->
</body>
</html>
```
#### Step 4: Create the CSS File

Create a new file called `styles.css` in your project folder:
```css
/* styles.css */
@import "node_modules/bootstrap/scss/bootstrap.scss"; /* include Bootstrap's CSS */

body {
    font-family: Arial, sans-serif;
}

.centered-image {
    text-align: center;
}

.navbar {
    padding-bottom: 20px;
}

.projects-grid {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 10px;
}
```
#### Step 5: Add the Profile Image and Navigation Bar

Update the `index.html` file:
```html
<!-- index.html -->
<!DOCTYPE html>
<html lang="en">
<head>
    <!-- ... -->
</head>
<body>
    <nav class="navbar navbar-expand-lg navbar-dark bg-dark">
        <div class="container">
            <a class="navbar-brand" href="#">My Profile Page</a>
            <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarSupportedContent" 
aria-controls="navbarSupportedContent" aria-expanded="false" aria-label="Toggle navigation">
                <span class="navbar-toggler-icon"></span>
            </button>
            <div class="collapse navbar-collapse" id="navbarSupportedContent">
                <ul class="navbar-nav ms-auto">
                    <li class="nav-item">
                        <a class="nav-link active" href="#projects">Projects</a>
                    </li>
                    <li class="nav-item">
                        <a class="nav-link" href="#publications">Publications</a>
                    </li>
                    <li class="nav-item">
                        <a class="nav-link" href="#reading-corner">Reading Corner</a>
                    </li>
                    <li class="nav-item">
                        <a class="nav-link" href="#code">Code</a>
                    </li>
                </ul>
            </div>
        </div>
    </nav>

    <main>
        <img src="profile-image.jpg" alt="Profile Image" class="centered-image">
    </main>
</body>
</html>
```
#### Step 6: Add the Pages and Footer

Create new files for each page (e.g., `projects.html`, `publications.html`, etc.) and add the necessary content:
```html
<!-- projects.html -->
<h1>Projects</h1>

<div class="projects-grid">
    <!-- demo projects grid items -->
    <div class="col-4">
        <h2>Project 1: Data Visualization</h2>
        <p>This is a description of Project 1.</p>
    </div>
    <!-- ... -->
</div>
```
Create a `footer.html` file:
```html
<!-- footer.html -->
<footer>
    <div class="container">
        <ul>
            <li><a href="#" target="_blank">Contact</a></li>
            <li><a href="#" target="_blank">Social Media</a></li>
            <li><button id="toggle-color-scheme" type="button" data-bs-toggle="collapse" data-bs-target="#color-scheme-options" 
aria-controls="color-scheme-options" aria-expanded="false" aria-label="Toggle color scheme options">
                    Toggle Color Scheme
                </button>
                <div id="color-scheme-options" class="collapse" style="max-width: 300px;">
                    <ul>
                        <li><a href="#" target="_blank">Dark High-Contrast Mode</a></li>
                        <li><a href="#" target="_blank">Solar Color Scheme</a></li>
                    </ul>
                </div>
            </li>
        </ul>
    </div>
</footer>
```
#### Step 7: Add the JavaScript Code for Toggle Button

Create a new file called `script.js` and add the following code:
```javascript
// script.js
const toggleButton = document.getElementById('toggle-color-scheme');
const colorSchemeOptions = document.getElementById('color-scheme-options');

toggleButton.addEventListener('click', () => {
    colorSchemeOptions.classList.toggle('show');
});
```
#### Step 8: Link the JavaScript File to the HTML

Update the `index.html` file:
```html
<!-- index.html -->
<!DOCTYPE html>
<html lang="en">
<head>
    <!-- ... -->
</head>
<body>
    <!-- ... -->
    <script src="script.js"></script>
</body>
</html>
```
#### Step 9: Test and Debug

Open the `index.html` file in your browser to test the page. Check for any accessibility issues using a tool like Lighthouse or WAVE Web Accessibility 
Evaluation Tool.

### Conclusion

You now have a basic profile web page with Bootstrap 5, WCAG compliance, and a toggle button for changing the color scheme. You can customize the pages 
further by adding more content, images, and interactivity using JavaScript and CSS.
