# Goal & Prerequisites

The goal of this tutorial is to demonstrate how to build a basic playground on the platform.

You only need:
- Git installed on your computer.
- Basic knowledge about Git (clone, push)

The source code of this documentation is on GitHub ([Documentation GitHub repository](https://github.com/jeromecance/techio-documentation)), please feel free to come up with proposals to improve it.

# Create a playground
Go to the [My playgrounds](/my-playgrounds) section, click on the "**Create new playground**" tile.

Then, select a template. A skeleton playgorund based on the template you choose is created in a new git repository.

# Get your playground
To modify this playground, you need to be authenticated on Tech.io’s Git Platform. To do so, you need to add a SSH key to your profile.

If you don’t already have an SSH key, execute `ssh-keygen` in your terminal. This command creates a public and a private key used to access your repository. (Check out [GitHub Help for more information](https://help.github.com/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent)).

By default, the public key is located in `~/.ssh/id_rsa.pub`. Copy your public key to [your settings page](/settings/ssh). 

Now that your key has been added, you can clone your repository using the origin URL provided on the playground page:

```bash
  git clone git@ssh.git.tech.io:cg123456/playground-hash.git
```

# Structure of a playground
Now that you have cloned the project, let's take a look at the folder structure:
- `techio.yml`: This mandatory file must be present at the root of a playground’s git repository and contains: table of content of the playground, the references to the lesson files, and some other technical details for advanced usage (discuessed later in the documentation).
- `cover.png`: This small image is displayed when your playground is displayed on the platform. Feel free to change it.
- `markdowns` folder: This folder contains lesson statements.
- `project` folder: We'll describe this later in the [Add a coding exercise](playgrounds/408/tech-io-documentation/content/add-a-coding-exercise) section of the documentation.

## techio.yml
The `techio.yml` contains the following details:
- title : The title of your playground which appears on the playground page.
- plan: The plan of your playground is described as list of the lessons. Each lesson is composed of a title (which appears in the table of contents) and a statement as a link to a markdown file, relative to your root folder.

> /!\ Do not use tab characters in this file, only spaces are allowed.

Have a look at the reference for all available options: [techio.yml reference](playgrounds/408/tech-io-documentation/content/techio-yml).

## Statement & Markdown
Lesson statements are markdown files. Markdown is a simple syntax for basic formatting (links, images, quote text, code formatted text snippets, etc).

You can find a cheatsheet for markdown [here](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet).

The repository skeleton contains a folder with one lesson, under the `markdowns` folder.

# Update your playground
First, change the content of `markdowns/welcome.md`:

```markdown
# Hello world,

welcome to my course. This is the first lesson.
```

Then, change the `techio.yml`to update the title of your playground:

```yml
title: Put your playground title here
plan:
  - title: Welcome
    statement: markdowns/welcome.md
```

# Deploy on tech.io
Now that you've changed your playground, you need to deploy it on Tech.io. Commit your changes and push them to Tech.io using the following git commands:

```bash
git commit -a -m "My first changes"
git push origin master
```

# Play with your playground
Come back to your playground page on Tech.io. It should have refreshed. Click "Preview" to play with your playground.

# Add a new lesson
If you want to add a new lesson, follow these steps:

- Create a markdown file: `markdowns/part2.md`
- Edit this markdown and add content
- Reference this markdown in `techio.yml`:

```yml
title: Put your playground title here
plan:
  - title: Part 1
    statement: markdowns/welcome.md
  - title: Part 2
    statement: markdowns/part2.md
```

- Push your changes

```bash
git commit -a -m "Add Part 2"
git push origin master
```

- Navigate back to your playground on Tech.io. Once it has refreshed and finished building, you can preview your modified playground.

# Share your playground
Once you're satisfied with your playground, it's time to share it with the world. You can make your plaground go 'live' by clicking the "Publish" button. It will shorten the url and publish it on your Tech.io profile. You can also share the link to your friends.

# Future updates to your plaground
When a playground is published and consumed by learners, you can freely update it with improvements and use the preview to see the results impacting users. Once you're satisfied, publish it again and the users will see the changes.
