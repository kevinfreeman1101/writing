# Bootstrap 5 Profile Page

## Query

I want a nice looking Profile web page that uses Bootstrap 5 and complies with the current WCAG accessibility standard. The main page should feature a profile image centered in the page; there should be a navigation bar with links to a Projects page (a Bootstrap grid of demo projects), a Publications page showing 2 published books, a Reading Corner for recommended reading and free book downloads, and a Code page for users to check out a selection of functional Jupyter Notebooks demonstrating Python data visualization; and all pages should have a footer with contact links, social media icons, and a toggle button for changing the color scheme from dark-high-contrast mode (the page's default scheme) to a light-high-contrast solar color scheme.

## wizardcoder Response

To create a Bootstrap 5 Profile web page that meets WCAG accessibility standards, follow these steps:

1. Choose an appropriate domain name for your website and purchase it or use a free subdomain.
2. Create a new folder on your local machine for your project files and navigate to it in the terminal.
3. Initialize a new Bootstrap 5 project by running `npm init` and selecting "Yes" when prompted if you want to create a package.json file.

interface.
5. Run `npm install bootstrap` to download Bootstrap's CSS and JavaScript files.
6. Create a new file called `index.html` and copy the following HTML code into it:

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <link
      href="https://cdn.jsdelivr.net/npm/bootstrap@5.0.2/dist/css/bootstrap.min.css"
      rel="stylesheet"
      integrity="sha384-EVSTQN3Pb1fMpWSRw6s7YZC1akiI2RFcxYChAznTl8EThVgTfwL3MIKZVPCTLfnqnGQUaO3+rJdm4jj0QJmF"
      crossorigin="anonymous"
    />
    <link rel="stylesheet" href="styles.css" />
  </head>
  <body class="d-flex flex-column h-100">
    <!-- Navbar -->
    <nav class="navbar navbar-expand-lg navbar-light bg-light">
      <div class="container-fluid">
        <a class="navbar-brand" href="#">Your Profile</a>
        <button
          class="navbar-toggler"
          type="button"
          data-bs-toggle="collapse"
          data-bs-target="#navbarNav"
          aria-controls="navbarNav"
          aria-expanded="false"
          aria-label="Toggle navigation"
        >
          <span class="navbar-toggler-icon"></span>
        </button>
        <div class="collapse navbar-collapse" id="navbarNav">
          <ul class="navbar-nav">
            <li class="nav-item">
              <a class="nav-link active" aria-current="page" href="#">Projects</a>
            </li>
            <li class="nav-item">
              <a class="nav-link" href="#">Publications</a>
            </li>
            <li class="nav-item">
              <a class="nav-link" href="#">Reading Corner</a>
            </li>
            <li class="nav-item">
              <a class="nav-link" href="#">Code</a>
            </li>
          </ul>
        </div>
      </div>
    </nav>

    <!-- Jumbotron -->
    <div class="jumbotron jumbotron-fluid">
      <div class="container">
        <h1>Your Name</h1>
        <p class="lead">Welcome to my profile!</p>
        <!-- Profile image centered in the page -->
        <img
          src="profile.jpg"
          alt="Profile picture"
          width="200"
          height="200"
          class="rounded-circle d-block mx-auto mb-4"
        />
      </div>
    </div>

    <!-- Projects page -->
    <section id="projects" class="container">
      <h2 class="text-center">Projects</h2>
      <div class="row">
        <div class="col-md-4 mb-3">
          <a href="#" class="text-decoration-none text-reset">
            <div class="card h-100 border-primary">
              <img
                src="project1.png"
                alt="Project 1"
                class="card-img-top"
                style="width: 100%; height: auto;"
              />
              <div class="card-body d-flex flex-column">
                <h5 class="card-title">Project Name</h5>
                <p class="card-text mt-auto">Description of the project...</p>
              </div>
            </div>
          </a>
        </div>

        <!-- Add more projects here -->
      </div>
    </section>

    <hr class="my-4" />

    <!-- Publications page -->
    <section id="publications" class="container">
      <h2 class="text-center">Publications</h2>
      <ul class="list-group">
        <li class="list-group-item list-group-item-action bg-light text-dark">
          Book Title
          <p>Authors, Publication Year</p>
        </li>
        <!-- Add more publications here -->
      </ul>
    </section>

    <hr class="my-4" />

    <!-- Reading Corner page -->
    <section id="reading-corner" class="container">
      <h2 class="text-center">Reading Corner</h2>
      <div class="row mb-3">
        <div class="col-md-4 mb-3">
          <a href="#" class="text-decoration-none text-reset">
            <div class="card h-100 border-primary">
              <img
                src="book.jpg"
                alt="Recommended Reading"
                class="card-img-top"
                style="width: 100%; height: auto;"
              />
              <div class="card-body d-flex flex-column">
                <h5 class="card-title">Book Title</h5>
                <p class="card-text mt-auto">Author, Publication Year</p>
              </div>
            </div>
          </a>
        </div>

        <!-- Add more recommended reading here -->
      </div>
    </section>

    <hr class="my-4" />

    <!-- Code page -->
    <section id="code" class="container">
      <h2 class="text-center">Code</h2>
      <div class="row mb-3">
        <div class="col-md-4 mb-3">
          <a href="#" class="text-decoration-none text-reset">
            <div class="card h-100 border-primary">
              <img
                src="python.png"
                alt="Python Notebook"
                class="card-img-top"
                style="width: 100%; height: auto;"
              />
              <div class="card-body d-flex flex-column">
                <h5 class="card-title">Data Visualization with Python</h5>
                <p class="card-text mt-auto">Open the notebook in Jupyter Lab.</p>
              </div>
            </div>
          </a>
        </div>

        <!-- Add more functional Jupyter Notebooks here -->
      </div>
    </section>

    <footer class="bg-light text-center pb-4">
      <ul class="list-inline mx-auto">
        <li class="list-inline-item me-3"><a href="#" class="text-reset">LinkedIn</a></li>
        <li class="list-inline-item me-3"><a href="#" class="text-reset">Twitter</a></li>
        <li class="list-inline-item me-3"><a href="#" class="text-reset">GitHub</a></li>
        <button
          type="button"
          class="btn btn-sm btn-outline-dark mx-auto toggle-color-mode"
          id="toggleModeButton"
          onclick="toggleColor()"
        >
          🌞 Light Mode
        </button>
      </ul>
    </footer>
  </body>

  <script src="/node_modules/bootstrap/dist/js/bootstrap.bundle.min.js"></script>
  <script>
    function toggleColor() {
      const body = document.querySelector("body");
      if (body.classList.contains("dark-mode")) {
        body.classList.remove("dark-mode");
        body.classList.add("light-mode");
        document
          .getElementById("toggleModeButton")
          .textContent = "🌚 Dark Mode";
      } else {
        body.classList.remove("light-mode");
        body.classList.add("dark-mode");
        document
          .getElementById("toggleModeButton")
          .textContent = "🌞 Light Mode";
      }
    }
  </script>
</html>
```

7. Create a `styles.scss` file and add the following Sass code:

```scss
// Import Bootstrap's SASS file
@import "~bootstrap/scss/bootstrap";

// Customize colors
$primary: #0a4c6e; // solar color scheme
$secondary: #f8f8f2;

// Set font-family
body {
  font-family: "Segoe UI", Arial, sans-serif;
}
```

8. Compile the SASS file into CSS using `sass --watch styles.scss:styles.css` in a separate terminal window.
9. Add images and icons to your project folder for use on the homepage and other pages.
10.  Create an optional `js` folder and add a custom JavaScript file called `dark-mode.js`. This script will handle toggling between light-high-contrast mode and dark-high-contrast mode when the toggle button is clicked:

```javascript
function toggleColor() {
  const body = document.querySelector("body");
  if (body.classList.contains("dark-mode")) {
    body.classList.remove("dark-mode");
    body.classList.add("light-mode");
  } else {
    body.classList.remove("light-mode");
    body.classList.add("dark-mode");
  }
}
```

11. Test your web page by running `npx http-server` in the project folder and opening it in a browser.

You can customize the colors, font, and content to suit your needs, but this is a basic structure that should be accessible to users with visual impairments or color blindness. Note that you'll need to add more content to each page (e.g., project descriptions, book titles, links) and adjust the styling as needed to fit your specific purposes.
