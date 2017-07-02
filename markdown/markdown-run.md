# Run extension
The run extension allows lessons to contain interactive code sections in which the user can modify and run the associated source code.

This code section can contains multiple source file stubs.
This extension also allows the writer of the playground to define the command that will be sent to an associated code runner. (See Runner Reference Documentation for more details)

# Simple Example
The following code snippet:
```
@[Hello World Example]({"stubs": ["HelloWorld.java"], "command": "javac HelloWorld.java && java HelloWorld"})
```

will generate an interactive code section

# Run syntax
The *Run* command is composed of 2 elements
- A label surrounded by square brackets `[ ]` and prefixed by the `@` token.
- A JSON object defining all the command parameters, surrounded by parenthesis ( ).


# Run JSON parameter
The JSON parameter is a map with the following keys/values:

```javascript
{
  /*
    List all the file paths that should be used for the default displayed stubs.
    The syntax highlighter format is detected from the stub file extension.
    type: Array of String [MANDATORY]
  */
  "stubs": ["path/to/file1.cpp", "/path/to/file2.html"],
  /*
    A command that is sent as parameter of the project runner entry point. For instance, it can
    be a unix command if the entry point is a bash interpreter. It can also be
    the name of a test case in case of a unit test runner.
    type: String [MANDATORY]
  */
  "command": "javac HelloWorld.java && java HelloWorld",
  /*
    Name of the associated project.    
    (Defined in techio.yml).
    The project defines the name of the Docker image used as a Runner (name:version).
    Remember, by default, your project is mounted in /project/target.
    type: String
    default value: The first project defined in techio.yml
    [OPTIONAL]
  */
  "project": "myproject",
  /*
    Layout used to display the interactive IDE in the playground  
    “inline”: Display the content in a 1 column layout.
    “aside”: merge the stubs files of all the aside layout into a large IDE,
    displayed in a column dedicated to the IDE.
    type: String
    default value: inline
    [OPTIONAL]
  */
  "layout": "aside"
}
```

