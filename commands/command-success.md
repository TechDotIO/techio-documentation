# TECHIO> success

# Usage

```bash
TECHIO> success STATUS
```

# Description

Define the status of a run (whether it was succesful or not). STATUS is a boolean value that can be either true or false.

If no success command is sent before the end of the container execution, the exit status value of the container will be used as fallback:
An exit status with the value of 0 equals a success. Anything else means equals a failure.

# Examples

Send a fail status.

```bash
TECHIO> success false
```
