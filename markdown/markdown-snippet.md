# Simple piece of code
To display a piece of code, use the following syntax:

````
```javascript
var a = 2;
var b = 4;
console.log(a+b);
```
````

`javascript` specifies the language so that the syntax is correctly highlighted.


# Auto fold
You can auto fold some sections of your code by using this syntax:

````
// { autofold
  code which is collapsed
// }

visible code

````

# Runnable snippet
## Syntax
For basic usage, you can make a simple piece of code runnable. To do that you need to create a piece of code by using the standard markdown syntax and then add the `runnable` keyword:

````
```javascript runnable
var a = 2;
var b = 4;
console.log(a+b);
```
````

renders as

```javascript runnable
var a = 2;
var b = 4;
console.log(a+b);
```


## Compatible languages
This simple syntax is a shortcut for a given language that automatically selects a runner and a command.

Here you can find a table that summarizes the supported languages and the associated docker image, command and filename.

| Language   | Docker image          | command                                             | filename     |
| ---------- | --------------------- | --------------------------------------------------- | ------------ |
| java       | java:latest           | bash -c "javac Main.java" && java Main"             | Main.java    |
| javascript | node:latest           | node index.js                                       | index.js     |
| python     | python:latest         | python main.py                                      | main.py      |
| bash       | bash:latest           | bash main.sh                                        | main.sh      |
| C          | gcc:latest            | bash -c "gcc main.c -o exe && ./exe"                | main.c       |
| C#         | mono:5                | bash -c "mcs main.cs && mono main.exe"              | main.cs      |
| C++        | gcc:latest            | bash -c "g++ main.cc -o exe && ./exe"               | main.cc      |
| dart       | google/dart:latest    | dart main.dart                                      | main.dart    |
| elixir     | elixir:latest         | elixir main.exs                                     | main.exs     |
| F#         | mono5:latest          | bash -c "fsharpc --nologo main.fs && mono main.exe" | main.fs      |
| go         | golang:latest         | go run main.go                                      | main.go      |
| groovy     | groovy:latest         | groovy main.groovy                                  | main.groovy  |
| haskell    | haskell:latest        | bash -c "ghc main.hs -o exe && ./exe"               | main.hs      |
| html       | ubuntu:latest         | echo "TECHIO> open -s /project/target index.html"   | index.html   |
| kotlin     | techio/kotlin-snippet-runner:latest|kotlin-compiler-runner.sh main.kt       | main.kt      |
| perl       | perl:latest           | perl main.pl                                        | main.pl      |
| php        | php:latest            | php main.php                                        | main.php     |
| ruby       | ruby:latest           | ruby main.rb                                        | main.rb      |
| rust       | rust:latest           | bash -c "rustc main.rs && ./main"                   | main.rs      |
| scala      | techio/scala-sbt:2.12 | bash -c "scalac Main.scala && scala Main"           | Main.scala   |
| swift      | swift:latest          | swift main.swift                                    | main.swift   |
| vb.net     | mono:5                | bash -c "vbnc /nologo main.vb && mono main.exe"     | main.vb      |

For any language in the `language` column you can create a snippet by specifying the language and the keyword `runnable` as seen before.

When the user presses the Run button, it automatically saves this piece of code in a file (`filename` column) stored in the specific docker image and then executes the command.

If you want us to add new language extension, feel free to contact us by giving us all required data (docker image, command, filename): [community@tech.io](mailto:community@tech.io)
