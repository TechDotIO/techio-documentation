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

  code to be hidden
// }
````

Example:

```
// { autofold
package com.yourself;

public class Main {
// }

public String hello() {
	return "Hello";
}

//{ autofold
}
//}
```


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

| Language   | Docker image  | command                                 | filename  |
| ---------- | ------------- | --------------------------------------- | --------- |
| java       | java:latest   | bash -c "javac Main.java" && java Main" | Main.java |
| javascript | node:latest   | node index.js                           | index.js  |
| python     | python:latest | python main.py                          | main.py   |

For any language in the `language` column you can create a snippet by specifying the language and the keyword `runnable` as seen before.

When the user presses the Run button, it automatically saves this piece of code in a file (`filename` column) stored in the specific docker image and then executes the command.

If you want us to add new language extension, feel free to contact us by giving us all required data (docker image, command, filename): [community@tech.io](mailto:community@tech.io)
