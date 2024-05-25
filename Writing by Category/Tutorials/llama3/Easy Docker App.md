# Easy Docker App

## Query

What's the easiest way to write an app that runs on desktop and mobile which uses docker to run a bash command?

## llama3 Response

What a fascinating question!

To create an app that runs on both desktop and mobile, using Docker to run a Bash command, you'll need to choose a suitable framework or technology. Here are a few options:

1. **Electron**: A popular framework for building cross-platform desktop apps using web technologies (HTML, CSS, JavaScript). You can use Electron's `child_process` module to run a Bash command in a Docker container.
2. **Flutter**: An open-source mobile app development framework created by Google. You can use Flutter's `path_provider` package to run a Bash command in a Docker container on Android and iOS devices.
3. **React Native**: A framework for building cross-platform mobile apps using JavaScript and React. You can use React Native's `react-native-ssh` library to run a Bash command in a Docker container.

Here's a high-level example of how you could use Electron with Docker:

**Step 1: Create a Docker image**

Create a new directory for your project and create a `Dockerfile`:
```dockerfile
FROM ubuntu:latest

WORKDIR /app

COPY . /app

RUN chmod +x my_bash_script.sh

CMD ["my_bash_script.sh"]
```

This Dockerfile creates an Ubuntu-based image, copies your Bash script into the container, sets the executable bit on the script, and sets the default command to run the script.

**Step 2: Create a React app with Electron**

Create a new directory for your project and create a `main.js` file:

```javascript
const { app, BrowserWindow } = require('electron');

let win;

function createWindow() {
  // Create the browser window.
  win = new BrowserWindow({
    width: 800,
    height: 600,
    webPreferences: {
      nodeIntegration: true,
    },
  });

  // Run your Bash command in a Docker container
  const dockerContainer = require('docker-container');
  const container = dockerContainer.create('my_bash_script');

  // Run the Bash command and get the output
  container.run(['bash', '-c', 'my_bash_script.sh']).then((output) => {
    console.log(output);
  });

  win.loadURL(`file://${__dirname}/index.html`);

  // Emitted when the window is closed.
  win.on('closed', () => {
    win = null;
  });
}

app.on('ready', createWindow);

// Quit when all windows are closed.
app.on('window-all-closed', () => {
  app.quit();
});

app.on('activate', () => {
  if (win === null) {
    createWindow();
  }
});
```

This code creates an Electron app, runs your Bash command in a Docker container using the `docker-container` module, and gets the output.

**Step 3: Package and run your app**

Use the `electron-builder` package to package your app for desktop distribution:

```bash
npm install electron-builder --save-dev
```
Then, create a `build` script in your `package.json` file:
```json
"scripts": {
  "build": "electron-builder build"
}
```

Run the build script: `npm run build`

You can then distribute your app as an executable for desktop platforms.

For mobile development, you'll need to use one of the other frameworks mentioned earlier (Flutter or React Native) and modify the code to run your Bash command in a Docker container using their respective modules or libraries.
