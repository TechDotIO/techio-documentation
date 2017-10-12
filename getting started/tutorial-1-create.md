# Introduction

The goal of this tutorial is to demonstrate how to build a basic playground on Tech.io.

## Prerequisites

You only need:
- Git installed on your computer.
- Basic knowledge about Git (clone, push)

The source code of this documentation is on GitHub ([Documentation GitHub repository](https://github.com/TechDotIO/techio-documentation), feel free to come up with proposals to improve it!)

## What's a Playground?

A playground can take many forms:
- General article explaining a concept (ex: [Genetic Algorithms](https://tech.io/playgrounds/334/genetic-algorithms), [Graph Theory Basics](https://tech.io/playgrounds/5470/graph-theory-basics-engesp))
- List of advanced features of a language (ex: [Advanced Python Features](https://tech.io/playgrounds/500/advanced-python-features), [7 Features of C++ 17 that will Simplify your Code](https://tech.io/playgrounds/2205/7-features-of-c17-that-will-simplify-your-code))
- Technology showcase (ex: [Reactive Programming with Reactor 3](https://tech.io/playgrounds/929/reactive-programming-with-reactor-3))
- In-depth Course on a specific topic ([Using C# LINQ - A Practical Overview](https://tech.io/playgrounds/213/using-c-linq---a-practical-overview))
- Quick how-to ([How to iterate (loop) over the elements in a map in Java 8](https://tech.io/playgrounds/5048/how-to-iterate-loop-over-the-elements-in-a-map-in-java-8))
...

Most of the playgrounds contain runnable code samples, but it's not mandatory. At the end of the day, you can craft what you want.

# Creating Your Own Playground

Head to the [Create a playground](/new-playground) page. 

## Templates

There, you can choose a template from a large selection of technologies. There are two types of templates:
- A "simple" template with limited code sample options but which enables you to quickly get started *(recommended for a first playground)*.
- A more advanced template with many options -dependencies, unit tests, visual renderer...- like a real project.

All templates contain a working code example and some hints to help you getting started.

You can also choose to create an empty playground from scratch.

## Repository

A skeleton playground based on the selected template is created in a new git repository.

There are two options for choosing the repository:
- On your own Github repository. For this, we need your authorization *(We will not perform any action without your approval. You can revoke the access from your GitHub settings at any time)*. This will allow a better collaboration with the community as they will be able to fork your playground and propose improvements and translations. *(recommended)*
- On our private Tech.io repository. For this, you need to be authenticated on Tech.io’s Git platform. 

::: Authenticating on Tech.io's Git platform

To do so, you need to add a SSH key to your profile.

If you don’t already have an SSH key, execute `ssh-keygen` in your terminal. This command creates a public and a private key used to access your repository. (Check out [GitHub Help for more information](https://help.github.com/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent)).

By default, the public key is located in `~/.ssh/id_rsa.pub`. Copy your public key to [your settings page](/settings/ssh).

Now that your key has been added, you can clone your repository using the origin URL provided on the playground page:

```bash
  git clone git@ssh.git.tech.io:cg123456/playground-hash.git
```

:::

# Structure of Your Playground
Now that you have created the repository, let's take a look at the folder structure:
- `techio.yml`: This mandatory file describes the structure of your playground. It must be present at the root of the playground’s git repository. It contains: the table of content of the playground, the references to the lesson files, and some other technical details for advanced usage (see [techio.yml reference](/reference/reference-techioyml.md)).
- `cover.png`: This small image (140x76) along your playground in the [explore page](https://tech.io/explore). By default, it's the logo of the technology you chose.
- `markdowns` folder or `statement.md` file: Each markdown file corresponds to a page. A one-page playground will just contain the `statement.md` file at the root. Else, all files will be contained in the `markdowns` folder.
*Markdown is a simple syntax for basic formatting (links, images, quote text, code formatted text snippets, etc). You can find a cheatsheet for markdown [here](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet).*
- `project` folder or nothing: This folder contains the files used in your coding exercies. We'll describe it later in the [Add a coding exercise](/getting%20started/tutorial-3-coding-exercise.md) section of the documentation. In a simple template, this folder is absent, because samples of codes are added directly in the markdown using [Code Snippets](/markdown/markdown-snippet.md).

# Updating Your Playground

## Changing the Title and Writing an Introduction

In the `tech.io.yml`file, update the title:

```yml
title: Put your playground title here
plan:
  - title: Welcome
    statement: markdowns/welcome.md
```
Then, in your markdown (either in `statement.md` or `markdowns/welcome.md`), write an introduction:

```markdown
# Hello world,

Welcome to this playground about this amazing technology. I'll show you ...
```

## Adding a New Page
If you want to add a new lesson, follow these steps:

- Create a markdown file: `markdowns/part2.md`
- Edit this markdown and add some content
- Reference this markdown in `techio.yml`:

```yml
title: Put your playground title here
plan:
  - title: Part 1
    statement: markdowns/welcome.md
  - title: Part 2
    statement: markdowns/part2.md
```

## Deploying the Changes on Tech.io

Committing and pushing a change to `master` will automatically trigger a build of the playground and update it on Tech.io.  Use the following git commands:

```bash
git commit -a -m "Title and introduction"
git push origin master
```

Come back to your playground page on Tech.io. It should have refreshed. Click "Preview" to play with your playground.


# Sharing Your Playground

## Sharing a Preview Link

Even if your playground is not published, you can share its preview link which looks like this:

https://tech.io/playgrounds/super_long_id/title_of_the_playground

Each time you push changes to your playground, the super_long_id is updated.

## Publishing Your Playground

A published playground is visible in the [Latest Playgrounds page](https://tech.io/explore/latest). *To maintain the quality of displayed playgrounds, we recommend you not to publish your test playground.*

Once a playground is published, the super_long_id becomes a short_id which makes the url much more friendly.

## Future Updates

Once a playground is published and available to the community, you can freely update it with improvements and use the preview to see the results impacting readers. Once you're satisfied with it, you can publish the new version, and the users will see the changes.
