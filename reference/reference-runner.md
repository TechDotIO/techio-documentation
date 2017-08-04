# Overview
When a user clicks on the RUN button, a new Docker container is spawned in the Tech.io infrastructure. A Docker container packages all the resources and programs to execute your desired tasks in an isolated environment.

Our system will execute the code snippet inside the container using all the tools available in the container image. We call this Docker container the *Runner*.

The result of its execution is sent back and displayed into the Tech.io web application.

Runner images are reusable among different playgrounds. You can use images from the official Docker hub or you can create and push your own.


# Runner Lifetime

## Content
The runner is based on a Docker image, therefore all the files that make up this container will be in the runner.

In addition to the original files of the Docker images, the content of your project root directory (defined in the `techio.yml` file, next to the declaration of the runner image) is copied into the directory: `/project/target`.

These additional files make your runner specific and tied to your playground.

## Build phase
Once the files are ready in your image, you may want to execute a build phase (setup or init phase), where you can perform initial operations on your `/project/target` files.

You may choose to:
- Download dependencies of your project from internet, based on the list of libraries that are defined in one of your project files.
- Pre-compile all the source files of the `/project/target` directory so you don't have to compile it at every run of your Runner image.
- Copy files from `/project/target` into more suitable directories of your container.

## Build file definition in the container image
If the runner image contains a file with the path `/project/build`, the content of this file will be executed during the build phase. This file can be a compiled file with the executable flag or a script file.

## Build file definition in the project root directory (buildCommand)
If you want to execute initialization commands in your runner, you can provide it directly from your git repository. The path of the build file can be set in the project configuration file (`techio.yml`).
[See projects/buildCommand section of the techio.yml reference](/reference/reference-techioyml.md)
If the file is an interpretable script, all the tools required to execute it must be available in the runner.

In case where the Runner image and project configuration both define a build file:
- The runner image build file is executed first (`/project.build`)
- Then the project configuration build file is executed (`buildCommand` in a project defined in `techio.yml`)


## Runner Input
Once the user clicks on the RUN button, the code snippet written in the web client is transferred into the runner container.
The content of all the files will be stored in the `/project/target` directory of your image.
The path where the file will be stored is defined in your markdown file associated with the test run extension.

Exemple: If your markdown is defined as:
```
@[My Playground Test]({"stubs": ["src/HelloWorld.java", "src/front/style.css"], "command": "python /project/target/exec.py"})
```

You have 2 files opened in the web application (HelloWorld.java and style.css).

Once the Run button has been clicked, the content of these files will be copied respectively into /project/target/src/HelloWorld.java and /project/target/src/front/style.css


# Runner Execution
## Entrypoint or command
Like any docker image, when the runner image is spawned and ran, its ENTRYPOINT is executed. The ENTRYPOINT is defined in the Dockerfile of the container.

This ENTRYPOINT command can receive extra arguments. The arguments are defined in the "command" parameter.

For instance, if the Dockerfile is defined as:
```
FROM ubuntu
ENTRYPOINT /bin/date
```

The creator of a playground can decide to use a specific date format for the execution of the Run section.
```
@[Date example]({"command": "--utc -R"})
```

The produced and executed command line of the container will be `/bin/date --utc -R`.

If the Runner does not contain an ENTRYPOINT, then the command parameter of the Run section will be used as a full command.

For instance, when using a standard ubuntu Runner image, the following Run section lists the files of the container:

```
@[List file example]({"command": "/bin/ls -la /"})
```

## Timeout
The maximum lifetime duration of a runner image is 30 seconds. The runner instance is stopped if the execution exceeds this duration. The instance lifetime duration can be shorter if the execution is finished before.

If a [viewer](/commands/command-open.md) is opened on a port, the maximum lifetime duration is extended to 120 seconds. This will allow the user to interact with the Docker container through this port for a longer amount of time. Any time that a request is made on the port, a new lifetime extension of 120 seconds is set on the runner.

## Max ressources
The number of resources that a runner can use is limited:
- Only one runner can be executed by a user at a time. The previous runner is killed if the user click on a new RUN button.
- 30 seconds of CPU execution max (can be extended if a viewer is opened, but the Runner CPU priority is then reduced)
- 720 Mo or RAM
- 10 Go of disk usage
- 100 processes limit
- Limited speed rate access to the network.


# Runner Outputs
## Standard output and commands
A list of text output can be written to the standard output of the runner during its execution phase. The text is interpreted as commands and some action result can be displayed on the client (success/fail status, debug message, code annotation, etc).

The full command list and the documentation can be found here: [Runner command reference Documentation](/reference/reference-command.md).

## Viewer
One of the command available in the runner is `open`. This command is a bit special because it can open a new interactive communication channel between the web application and the runner container.

This communication channel allows you to add a new layer of interactivity to your playground. Some examples are:
- Display interactive canvas content
- Create client/server interaction for a web application example


# Provide a custom Runner
We will give you the minimal commands necessary to build your custom Docker image and push it in the Docker hub to make it available to the system and other community members.

- Create and build a custom Docker image
- Create a Docker image based on Ubuntu that will execute a shell script:

Docker file content:

```
FROM ubuntu
COPY entrypoint.sh /entrypoint.sh
ENTRYPOINT /entrypoint.sh
```

Build the Docker image and tag it:

```bash
docker build -t "my-ubuntu:1.0" .
```

You can test your Docker image with the command:

```bash
docker run -v /home/user/project/target:/project/target "my-ubuntu:1.0" [COMMAND]
```

Remember to mount a `/project/target` directory in your image to reproduce the behavior of the image used by the system.

- Tag and push a Docker image
- Creates an account on Docker hub if you not already have one: https://hub.docker.com
- Sign in with your username and password: `docker login`
- Push your image: `docker push "my-ubuntu:1.0"`

Your image can now be declared in the runner section of your techio.yml file:

```yml
runner: user/my-ubuntu:1.0
```
