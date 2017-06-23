# TECHIO> success
# Usage

```bash
TECHIO> success STATUS
```

# Description
Define the success/fail status of a run. STATUS is a boolean value that can be either true or false.

If no success command is sent before the end of the container execution, the exit status value of the container will be used as fallback:
An exit status with a value equals to 0 means a success.
An exit status with a value different than 0 means a failure.

# Examples
Send a fail status.

```bash
TECHIO> success false
```
