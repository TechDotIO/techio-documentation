# Get an example
To understand how coding exercises works, we recommend you to start with a template. For this tutorial, we'll use the Python template but feel free to choose the template which is the more appealing for you.

Once you've selected your template, get it by cloning it using git.

# Structure of a coding exercise
In our example, the coding exercise is stored in the `*-project` folder. It is composed of two files:
- `universe.py`: this is a simple piece of code that will be displayed to the user and that he will need to fix it.
- `test_universe.py`: this is a file which will be used when the user will press the "run" button.

# Configuration of the exercise in techio.yml
In `techio.yml`, the project is defined as it:

```yml
projects:
  python:
    root: /python-project
    runner: python:3  
```

Here is the detail:
- `projects:`: this is where you define all the projects you need for your playground
- `  python:`: this is the name of this project
- `    root: /python-project`: this is where the project is stored
- `    runner: python:3`: this is a docker image name to use to run your project (see Understanding the workflow below)

# Add the exercise to a markdown
In the `welcome.md` markdown you can see a special tag that creates the exercise at the position you want:

```markdown
@[Luke, how many stars are there in these galaxies?]({"stubs": ["universe.py"], "command": "python3 test_universe.py"})
```

Let's explain this command:

- `@ [Luke, how many stars are there in these galaxies?]`: display a label at the top of your exercise.
- `stubs: ["universe.py"]`: define what files to show to the user.
- `command: "python3 test_universe.py"`: this is the command which is given to the docker image defined in `techio.yml` for this project when the user presses the run button.

# Understanding the workflow
- When a coding exercise is displayed to a user, it shows a label and the stubs declared in the stubs property.
- When the user changes the stubs and press the "run" button, the docker image specified in `techio.yml` for the project is instancied and launched
- The root folder of the project is mounted in the image in the folder `/project/target`
- The files (stubs) that have been modified by the user are copied in the root folder and erased the initial ones.
- The specified command is run on the docker instance.
- Techio commands (e.g. `TECHIO> success`)can be called during this process to interact with the user.


# Runner
The runner is the execution engine for your code. It puts everything together: it packages your project, then runs your code exercices.

Technically speaking, it's a Docker image. You can use official images available on the Docker Hub or you may use those made specifically for the platform (to include extra tools and features). A complete documentation about the Runners can be find [here](/playgrounds/408/tech-io-documentation/content/runner-reference).

As said earlier, Runners are Docker images. Tech.io has created some images that work well with the platform, these images are available on https://hub.docker.com/u/techio/.


# Test the playground
It's time to test the playground:
1. Push your code and go back to your contribution main page.
2. Click the preview button once the new version is detected (and there is no reported error).
3. Check that your coding exercise displays the stub content.  You should see an interactive code editor.
4. Click the "Run" button.

This will run the docker image with the parameters that you set in the “command” property of your test exercise.

# Next Step
Here are interesting links to dive into the awesome world of Runners:
- [Crafted Runners](/playgrounds/408/tech-io-documentation/content/runner-list)
- [Runner Reference Documentation](/playgrounds/408/tech-io-documentation/content/runner-reference)
- [Runner Commands Reference Documentation](/playgrounds/408/tech-io-documentation/content/runner-commands)
