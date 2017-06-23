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
- [annotate](/playgrounds/408/tech-io-documentation/content/annotate): Annotate the client code editor with margin marker and an associated message.
- [message](/playgrounds/408/tech-io-documentation/content/message): Prints a STRING message to a channel.
- [open](/playgrounds/408/tech-io-documentation/content/open): Opens an http communication with the runner through a client iframe (viewer).
- [redirect-streams](/playgrounds/408/tech-io-documentation/content/redirect-streams): Redirects the standard streams (standard output stream and standard error stream) to a OUT_CHANNEL.
- [success](/playgrounds/408/tech-io-documentation/content/success): Define the success/fail status of a run.


