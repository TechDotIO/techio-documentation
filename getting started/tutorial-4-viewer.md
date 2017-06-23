# Concept of Viewer
A viewer is a HTTP service that serves contents from the runner to an iframe inside the playground page. You can create your own http server from your code or use a simplified server given by tech.io.

It is possible to launch a viewer at anytime during the execution of a test by using the [`Open` command](/playgrounds/408/tech-io-documentation/content/open).

# Use a Viewer
First, create a playground. In this example, we're using the node.js template.
Then, create a `www` folder at the root of your project (so `/nodejs-project/www`). Add into it a simple html file named `HelloWorld.html` whose content is:

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
Open the file `nodejs-project/universe.spec.js` and add a command after the line `it('should sum stars', function () {`:

```javascript

it('should sum stars', function () {
  console.log('TECHIO> open -s /project/target/www HelloWorld.html');

```

Here we use a new syntax: the `TECHIO>` prompt.  Each time there is a `TECHIO>` prompt on the standard output, the platform will consider it as a command.

Let's analyse the command:

```
TECHIO> open -s /project/target/www HelloWorld.html
```

- `TECHIO>`	execute a techio.io command
- `open` open a viewer on a http flux
- `-s` specify to use a simple server by defining a folder
- `/project/target/www` is the folder you want to use as a root folder for the server. See below for more details.
- `HelloWorld.html` is the file you want to load in the iframe of the viewer

# Why /project/target/www?
If you've read the documentation about [adding a coding exercise](/playgrounds/408/tech-io-documentation/content/add-a-coding-exercise), you remember that when your project is built, a docker image is created and your project is copied into this image in the `/project/target` directory. So if you want to expose a folder inside this project (like our `www` folder), you need to prefix the path with `/project/target`.
It means that you can also reference any folder in your docker image. For example, if a coding exercise generates some html files based on the code of the user and these files are stored in the filesystem in /var/www/html, you can use this folder.

# Test your playground
Commit your changes and push your code. Then run the coding exercise. You should see a viewer displaying your html file.

# Furthermore

If you want to create a more complex server and not serve only a folder of static files, do not use the `-s` option. Check the full documentation of the [open command](/playgrounds/408/tech-io-documentation/content/open).

Here are some classical use cases for the use of a viewer:
- Playgrounds around a http stack (node.js, Play!Framework, Spring Boot, etc.)
- Playgrounds around front-end technologies (Angular.Js, React, etc.)
- Playgrounds with plots (such as DataScience courses, R plotting, etc.)
- Playgrounds with interactive contents (games, Web application development, etc.)
- Playgrounds with visual interface over databases (neo4j browser, etc.)
