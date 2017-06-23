
# TECHIO> message
# Usage

```bash
TECHIO> message [OPTIONS] <STRING>
```

# Description
Prints a STRING message to a channel.

- When a string is printed to the standard output stream (without the use of a command), it is an implicit command message printed to the out channel.
- When a string is printed to the standard error stream (without the use of a command), it is an implicit command message printed to the err channel.

When a message printed follows the format FILENAME:LINE where FILENAME matches with the name of a file of the client code editor, the text is transformed into an hyperlink, linking to the associated code editor and line number.

# Options

`-c, --channel <CHANNEL>` CHANNEL is a channel name where the message will be printed. if the channel is not specified, the default value is out.
The channel name can be any string. It will  create an associated channel on the client side.

# Examples
Prints hello world on the standard output channel.

```bash
TECHIO> message hello world
```

Prints This is a debug message. on the user debug channel.

```bash
TECHIO> message --channel "user debug" This is a debug message.
```

Prints a message containing an hyperlink link to the line 5 of the Main.java code editor.

```bash
TECHIO> message There is an error in the file Main.java:5
```


