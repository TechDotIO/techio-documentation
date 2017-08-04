# Syntax
All commands executed by the Tech.io infrastructure have to respect a format to be recognized as a valid command.

All commands have to be sent to the standard output stream and have to begin with a command token: `TECHIO>`

Commands respects the GNU long option syntax (arguments name prefixed with double hyphen --).

Example:
```
TECHIO> message --channel "out" hello world!
```

All other values sent to the standard output and standard error stream are interpreted as message command.

# Available commands
- [annotate](/commands/command-annotate.md): Annotate the client code editor with margin marker and an associated message.
- [message](/commands/command-message.md): Prints a STRING message to a channel.
- [open](/commands/command-open.md): Opens an HTTP communication with the runner through a client <iframe> (viewer).
- [redirect-streams](/commands/command-redirect-streams.md): Redirects the standard streams (output stream and error stream) to a OUT_CHANNEL.
- [success](/commands/command-success.md): Defines the success/fail status of a run.


