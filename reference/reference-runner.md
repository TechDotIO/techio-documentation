# Overview
When a user click on the RUN button, a new docker container is spawned in the Tech.io  infrastructure. You might already be familiar with docker containers, but if not, as a short description, a docker container contains all the resources and programs to execute your desired tasks in an isolated environment.

Our system will execute the code associated to the RUN section inside the container, using all the tools available in the container image. We call this docker container: Runner.

The result of its execution is sent back and displayed into the Tech.io web application.

Runner images are reusable among different playgrounds. You can use images from the official docker hub or you can create and push your own.


# Runner Lifetime
## Content
The content of a runner is based on a docker image, thus you will find in a runner all the files that make up this container.

In addition of the original files of the docker images, the content of your project root directory (defined in the `techio.yml` file - next to the declaration of the runner image) is copied into the directory `/project/target`.

This additional files makes your runner specific and tight to your playground.



## Build phase
Once that the image and all files are ready in your image, you might want to execute a build phase (or we can also call it a setup or init phase), where you can perform initial operations on your /project/target files.

For instance, you might want to:
- Download dependencies of your project from internet, according to the list of libraries that are defined in one of your project files
- Pre-compile all the source files of the /project/target directory to not have to compile it at every run of your Runner image.
- Copy some files from /project/target into more suitable directories of your container.

## Build file definition in the container image
If the runner image contains a file with the path /project/build, the content of this file will be executed during the build phase. This file can be a compiled file with the executable flag or a script file.

## Build file definition in the project root directory (buildCommand)
If you want to execute initialisation command in your runner, you can also provide it directly from your git repository. The path of the build file can be set in the project configuration file (`techio.yml`).
[See projects/buildCommand section of the techio.yml reference documentation](/playgrounds/408/tech-io-documentation/content/techio-yml)
If the file is an interpretable script, then all the tools required to execute it need to be available in the runner.

In case where both Runner image and project configuration defines a build file:
- The runner image build file is executed first (`/project.build`)
- The project configuration build file is executed in second (`buildCommand` in a project defined in `techio.yml`)


## Runner Input
Once you click on RUN button, the content of the code written in the web client is transferred into the runner container.
The content of all the files will be stored in the `/project/target` directory of your image.
The path where the file will be stored is defined in your markdown file associated with the test run extension.

Exemple: if your markdown is defined as

```
@[My Playground Test]({"stubs": ["src/HelloWorld.java", "src/front/style.css"], "command": "python /project/target/exec.py"})
```

You have 2 files opened in the web application (HelloWorld.java and style.css).

Once the Run button has been clicked, the content of those files will be copied respectively into /project/target/src/HelloWorld.java and /project/target/src/front/style.css


# Runner Execution
## Entrypoint or command
When a runner image is spawned and runned, like any docker image, its ENTRYPOINT is executed (entrypoint defined in the Dockerfile of the container).

This Entrypoint command can receive extra arguments. The arguments are defined in the "command" parameter.

For instance, if the Dockerfile is defined as

```
FROM ubuntu
ENTRYPOINT /bin/date
```

The creator of a playground can decide to use a specific date format for the execution of the Run section.

```
@[Date example]({"command": "--utc -R"})
```

The produced and executed command line of the container will be `/bin/date --utc -R`.

If the Runner does not contain an Entrypoint, then the command parameter of the Run section will be used as a full command.

For instance, using a standard ubuntu Runner image, the following Run section list the files of the container:

```
@[List file example]({"command": "/bin/ls -la /"})
```

## Timeout
The maximum lifetime duration of a runner image is 30 seconds. The runner instance is stopped if the execution exceed this duration. The instance lifetime duration can be shorter if the execution is finished before.

If a [viewer](/playgrounds/408/tech-io-documentation/content/open) is opened on a port, the maximum lifetime duration is extended of 120 seconds. This will allow the user to interact with the docker container through this port for a longer amount of time. Any time that a request is made on the port, a new extension of 120 seconds lifetime is set on the runner.

## Max ressources
The number of resources that a runner can use is limited:
- Only one runner can be executed by a user at a time. (The previous runner is killed if the user click on a new RUN button)
- 30 seconds of CPU execution max (can be extended if a viewer is opened, but the Runner cpu priority is then reduced)
- 720 Mo or RAM
- 10 Go of disk usage
- 100 processes limit
- Limited speed rate access to the network.


# Runner Outputs
## Standard output and commands
A list of text output can be written to the standard output of the runner, during its execution phase. The text is interpreted as commands and some action result can be displayed on the client (success/fail status, debug message, code annotation, …)

The full command list and their documentation is available in the [Runner command reference Documentation](/408/tech-io-documentation/content/runner-commands).

## Viewer
One of the command available in the runner is `open`. This command is a bit special because it can open a new interactive communication channel between the web application and the runner container.

This communication channel allow you to add a new layer of interactivity to your playground. Some examples are:
- Display interactive canvas content
- Create client/server interaction for a web application example


# Provide a custom Runner
You might already be familiar with docker tools, so this documentation section might be unnecessary for you.

We will give you the minimal commands necessary to build your custom docker image and push it in the docker hub to make it available to the system and other users.

- Create and build a custom docker image
- Create a docker image based on ubuntu that will execute a shell script:

Docker file content:

```
FROM ubuntu
COPY entrypoint.sh /entrypoint.sh
ENTRYPOINT /entrypoint.sh
```

Build the docker image (and tag it):

```bash
docker build -t "my-ubuntu:1.0" .
```

You can test your docker image with the command:

```bash
docker run -v /home/user/project/target:/project/target "my-ubuntu:1.0" [COMMAND]
```

Remember to mount a `/project/target` directory in your image to reproduce the behavior of the image used by the system.

- Tag and push a docker image
- Creates an account on docker hub if you not already have one: https://hub.docker.com
- Sign in with your username and password: `docker login`
- Push your image: `docker push "my-ubuntu:1.0"`

Your image can now be declared in the runner section of your techio.yml file

```yml
runner: user/my-ubuntu:1.0
```
