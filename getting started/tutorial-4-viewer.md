# Concept of Viewer
A viewer is a HTTP service that renders content from the runner to an <iframe> inside the playground page. You can create your own HTTP server from your code or use a simplified server given by Tech.io.

It is possible to launch a viewer at anytime during the execution of a test by using the [`Open` command](/playgrounds/408/tech-io-documentation/content/open).

# Use a Viewer
First, create a playground using a template of your choice. In this example, we are using the **NodeJS template**.
Then, create a `www` folder at the root of your project (`/nodejs-project/www`). Add a simple HTML file named `HelloWorld.html` with the following code:

```html
<html>
    <head>
        <title>Hello World!</title>
    </head>
    <body>
        <h1>Hello World!</h1>
        <p>This page is served by the static viewer</p>
    </body>
</html>
```

# Open the server from a command
Open the `nodejs-project/universe.spec.js` file and add a command after the line `it('should sum stars', function () {`:

```javascript
it('should sum stars', function () {
  console.log('TECHIO> open -s /project/target/www HelloWorld.html');
```

Here we use some new syntax... the `TECHIO>` prompt.  Each time there is a `TECHIO>` prompt on the standard output, the platform will consider it as a command.

Let's analyze the command:
```
TECHIO> open -s /project/target/www HelloWorld.html
```

- `TECHIO>`: Execute a Tech.io command
- `open`: Open a viewer on a HTTP flux
- `-s`: Specify to use a simple server by defining a folder
- `/project/target/www`: The folder you want to use as a root folder for the server. More details below.
- `HelloWorld.html`: The file you want to load in the <iframe> of the viewer

# Why /project/target/www?
As discussed in the [adding a coding exercise](/playgrounds/408/tech-io-documentation/content/add-a-coding-exercise) section, when your project is built a Docker image is created and your project is copied into this image in the `/project/target` directory. So if you want to expose a folder inside this project (like the `www` folder), you need to prefix the path with `/project/target`.
This means that you can also reference any folder in your Docker image. For example, if a coding exercise generates some HTML files based on the code of the user and are stored in the filesystem in /var/www/html, you can use this folder.

# Test your playground
Commit your changes and push your code. Then, run the coding exercise. You should see a viewer displaying your html file.

# Furthermore

If you want to create a more complex server and not serve only a folder of static files, do not use the `-s` option. Check the full documentation of the [open command](/playgrounds/408/tech-io-documentation/content/open).

Here are some classical use cases for the use of a viewer:
- Playgrounds around a HTTP stack (NodeJS, Play!Framework, Spring Boot, etc.)
- Playgrounds around Front-End technologies (AngularJS, React, etc.)
- Playgrounds with Plots (such as Data Science courses, R plotting, etc.)
- Playgrounds with Interactive Contents (Games, Web application development, etc.)
- Playgrounds with Visual Interface over Databases (Neo4j Browser, etc.)
