All docker images work with Tech.io. So have a look at https://hub.docker.com to pick one.

Here are the available runners that we've crafted to simplify your life on the platform:

| Name | Short description | Git Docker | Environment (Language, requirements, etc.) |
|------|-------------------|------------|--------------------------------------------|
|java-maven3-junit4-runner|A `JUnit` test runner using `Maven` for building the course and `javac` for compiling the user's answer.|[GitHub](https://github.com/TechDotIO/java-maven3-junit4-runner) [DockerHub](https://hub.docker.com/r/techio/java-maven3-junit4-runner/)|Java 8, Maven 3, JUnit 4|
|maven3-runner|A full maven3 runner using `Maven` for building and running the course according to the user answer.|[GitHub](https://github.com/TechDotIO/maven3-runner) [DockerHub](https://hub.docker.com/r/techio/maven3-runner/)|Java 8, Maven 3|
|sbt-scalatest-runner|A `Scala` test runner that fetches dependencies using `sbt` and executes tests using `scalatest`.|[GitHub](https://github.com/TechDotIO/sbt-scalatest-runner) [DockerHub](https://hub.docker.com/r/techio/sbt-scalatest-runner/)|Scala 2.12|
|golang-godep-runner|A `Golang` test runner using `godep` for fetching dependencies.|[GitHub](https://github.com/TechDotIO/golang-godep-runner) [DockerHub](https://hub.docker.com/r/techio/golang-godep-runner/)|Go 1.8, works with the "testing" package|
|node-npm-runner|A `JavaScript` runner using `npm` for fetching dependencies and running user code with the provided command. |[GitHub](https://github.com/TechDotIO/node-npm-runner) [DockerHub](https://hub.docker.com/r/techio/node-npm-runner/)|Node.js 7.4|
|mono-nuget-nunit-runner|A `NUnit` test runner using `NuGet` for building the course and running user code with `Mono` (`C#`, `F#`)|[GitHub](https://github.com/TechDotIO/mono-nuget-nunit-runner) [DockerHub](https://hub.docker.com/r/techio/mono-nuget-nunit-runner/)|Mono 4.8|
|cmake-gcc-runner|A simple `C/C++` runner building using `CMake` and `GCC` and running user code using the command provided in the course.|[GitHub](https://github.com/TechDotIO/cmake-gcc-runner) [DockerHub](https://hub.docker.com/r/techio/cmake-gcc-runner/)|GCC 6.3|
|c-check-runner|A `Check` test runner for `C` courses using `autoconf/make` and `GCC` for building.|[GitHub](https://github.com/TechDotIO/c-check-runner) [DockerHub](https://hub.docker.com/r/techio/c-check-runner/)|GCC 6.3|
|python3-unittest-runner|A `Python` runner using `unittest` for testing user code.|[GitHub](https://github.com/TechDotIO/python3-unittest-runner) [DockerHub](https://hub.docker.com/r/techio/python3-unittest-runner/)|Python 3.6|
|dotnet-runner|A `.Net Core` runner for `C#/F#` using `MSTest`/`xUnit` for testing user code.|[GitHub](https://github.com/TechDotIO/dotnet-runner) [DockerHub](https://hub.docker.com/r/techio/dotnet-runner/)|.Net Core 1.1|
|rust-cargo-runner|A `Rust` test runner using `cargo` for building the course as well as running user code.|[GitHub](https://github.com/TechDotIO/rust-cargo-runner) [DockerHub](https://hub.docker.com/r/techio/rust-cargo-runner/)|Rust 1.15|
|ruby-bundler-runner|A `Ruby` test runner using `bundler` for installing dependencies.|[GitHub](https://github.com/TechDotIO/ruby-bundler-runner) [DockerHub](https://hub.docker.com/r/techio/ruby-bundler-runner/)|Ruby 2.4|
