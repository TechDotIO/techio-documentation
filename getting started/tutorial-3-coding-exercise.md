# Get an example
To understand how the coding exercises work, we recommend starting off with a template. For this tutorial, we'll use the **Python template**, but feel free to choose the template for the language which you are most comfortable with.

Once you've selected your template, create it locally by cloning it using git.

# Structure of a coding exercise
In our example, the coding exercise is stored in the `*-project` folder. It consists of two files:
- `universe.py`: This is a simple code snippet that will be displayed to the user, who will need to fix it.
- `test_universe.py`: This is a file which will be used to test the presented code snippet when the user presses the "run" button.

# Configuration of the exercise in techio.yml
In `techio.yml`, the project is defined as such:

```yml
projects:
  python:
    root: /python-project
    runner: python:3  
```

Here are the details:
- `projects:`: This is where you define all the projects you need for your playground.
- `  python:`: This is the name of this project.
- `    root: /python-project`: This is where the project is stored.
- `    runner: python:3`: This is a Docker image used to run your project

# Add the exercise to a markdown
In the `welcome.md` markdown, you can see a special tag that creates the exercise at the position you want:

```markdown
@[Luke, how many stars are there in these galaxies?]({"stubs": ["universe.py"], "command": "python3 test_universe.py"})
```

Let's explain this command:

- `@ [Luke, how many stars are there in these galaxies?]`: Displays the text in a label at the top of the exercise.
- `stubs: ["universe.py"]`: Define what files to show to the user.
- `command: "python3 test_universe.py"`: Test command given to the docker image (defined in `techio.yml`) for this project when the user presses the run button.

# Understanding the workflow
- When a coding exercise is displayed to a user, it shows a label and the stubs declared in the stubs property.
- When the user changes the snippet and clicks the "run" button, the docker image specified in `techio.yml` for the project is instancied and launched
- The root folder of the project is mounted in the image (located in the `/project/target` folder).
- The snippets that have been modified by the user are copied into the root folder and the initial ones are erased.
- The specified command is ran on the Docker instance.
- Techio commands (e.g. `TECHIO> success`) can be called during this process to interact with the user.


# Runner
The runner is the execution engine for your code. It packages your project and then runs your code exercises.

Technically speaking, it's a Docker image. You may use official images available on the [Docker Hub](https://hub.docker.com/u/techio/) or those made specifically for the Tech.io platform (which include extra tools and features). A complete documentation about the Runners can be find [here](/reference/reference-runner.md).

# Test the playground
It's time to test the playground:
1. Push your code and navigate back to the main page of your playground.
2. Once the new version is detected and sucessfully built, click the preview button.
3. Check that your coding exercise are displayed as the stub content.  You should see an interactive code editor.
4. Click the "Run" button.

This will run the Docker image with the parameters that you set in the “command” property of your test exercise.

# Next Step
Here are interesting links to dive into the awesome world of Runners:
- [Crafted Runners](/misc/runner-list.md)
- [Runner Reference Documentation](/reference/reference-runner.md)
- [Runner Commands Reference Documentation](/reference/reference-command.md)
