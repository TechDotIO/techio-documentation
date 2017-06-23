# General Information

The presence of the `techio.yml` file is mandatory at the root of the git repository of a playground.

This file contains the plan of the playground, the references to the playground files and the technical details to correctly build a playground associated to the repository.

# Main section
The main section of `techio.yml` contains the title and a plan of your playground.
The content and the hierarchical structure of a playground is defined by the plan.
The information required to correctly build and run the technical part of a playground is defined by the projects element.

```yml
# The playground title.
# type: String
title: playground title

# Specify a cover for your playground.
# This is a small image (jpg/png) that will be displayed
# in the playground card. By default, you can also create
# a cover.jpg (or cover.png) at the root of your repository
cover: /path/to/an/image.jpg

# The root of the playground plan. The plan can either be composed of chapters
# or lessons.
# type: Ordered List of Chapter or Lesson
plan: See Chapter or Lesson

# The root element of the projects list.
# type: Ordered Map of Project
projects: See Projects section
```


# Lesson
A Lesson is displayed as a single page on Tech.io.

```yml
# The root element of a Lesson.
# type: Ordered List
plan:
      # The lesson title.
      # type: String
    - title: The lesson title
      # The statement content file. The path is relative to the git root
      # directory.
      # type: String
      statement: /path/to/lesson1.md
```



# Chapter
In our terminology, a chapter is an ordered list of Lessons. Thus, it is the hierarchical level above the concept of lessons. This hierarchical level is optional since playgrounds can only be made of lessons.

A chapter has a title, a description and contains a list of lesson (plan).
The description is composed by few lines of text which describe the purpose of the chapter and which is displayed in the table of content.

```yml
# The root element of a Chapter.
# type: Ordered List
plan:
      # The chapter title.
      # type: String - default value: Unnamed
    - title: The chapter title
      # Few lines of text which describe the purpose of the chapter.
      # type: String
      description: This fields contains the description of the chapter.
      # The root of the lessons plan of this chapter.
      # type: Ordered Map of Lesson
      plan: See Lesson
```


# Projects
The projects element contains a list of project. A project contains the technical elements necessary to build and run interactive code section of a lesson.

```yml
# The root element of the projects list.
# type: Unordered Map
projects:
    # The project id. The project id will be referenced by tests.
    # type: Unordered Map
    my-playground:
        # The root directory of the project. This root path is relative to the
        # git root directory. The content of this directory will be copied
        # into the builder source path (see Builder section for more details).
        # type: String
        # default value: /
        root: /path/to/root/sources

        # The build command can reference a script from your git project, or
        # a set of commands (e.g: cd /project/target && npm install) that will
        # be executed in the runner image, at build time.
        # It allows you to use standard docker images and perform “install”
        # or “setup” actions in the new images, for instance
        # fetching dependencies.
        # It *replaces* the build script that may already exists in your
        # personalized docker image. Note: you can still call the standard
        # /project/build script of the image from your own script.
        # (see Runer reference documentation for more details on build scripts).
        # type: String
        buildCommand: cd /project/target && ./my-install-script.sh

        # The runner image reference. See runner element details for more
        # information.
        # type: Ordered Map representing a Runner
        runner: See Runner
```

# Runner
The runner enters in action when a user click on the RUN button inside an interactive programming section in a lesson.

All the technical specification about the creation and the use of a Runner can be found in the [Runner Reference Documentation](/playgrounds/408/tech-io-documentation/content/runner-reference).



```yml
# The runner root element.
# type: String
runner: junit-runner:1.0.0
```

This additional syntax is also valid:

```yml
# The runner root element.
# type: Unordered Map
runner:
    # The runner docker image name. It will be downloaded from the docker hub.
    # type: String
    name: junit-runner
    # The docker tag to use for the image
    # type: String
    version: 1.0.0
```


# Example

```yml
title: My playground title
cover: /playgrounds/cover.png
plan:
- title: My first chapter title
  description: This is a quick description of my first chapter.
  plan:
  - title: Lesson 1 of Chapter 1
    statement: /playgrounds/chapter1/lesson1.md
  - title: Lesson 2 of Chapter 1
    statement: /playgrounds/chapter1/lesson2.md
- title: My Second chapter title
  description: This is a quick description of my second chapter.
  plan:
  - title: Lesson 1 of Chapter 2
    statement: /playgrounds/chapter2/lesson1.md

projects:
    my-java-playground-project:
        root: /project
        buildCommand: ./install.sh
        runner: junit-runner: 1.0.0
```
