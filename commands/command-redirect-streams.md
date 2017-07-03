
# TECHIO> redirect-streams
# Usage

```bash
TECHIO> redirect-streams [OPTIONS] <OUT_CHANNEL>
```

# Description

Redirects the standard streams (standard output stream and standard error stream) to a OUT_CHANNEL.

If the OUT_CHANNEL is not specified, the default value is out.

The special null channel is used to redirect the stream to a void channel. Thus, the printed content will not be displayed.

# Options

`-i, --input <CHANNEL>[,CHANNEL,…]` List of input CHANNELS to redirect to the OUT_CHANNEL. It can be 'out' for the standard output stream, 'err' for the standard error stream or any other channel you define. The default value is out,err.


`-p, --pattern <PATTERN>` Redirects only the strings matching the given regular expression PATTERN.


`-r, --reset` Cancel all the redirections and restore the default behaviour. This option should be used online (exclusion of other)


# Examples

Redirect both standard output and standard error stream to the out channel:

```bash
TECHIO> redirect-streams out
```

Redirect the standard error stream err to the compilation error channel:

```bash
TECHIO> redirect-streams --input "err" "compilation error"
```

Redirect the strings written on the standard error stream and starting with the value [DEBUG]: to the debug channel:

```bash
TECHIO> redirect-streams --input "err" --pattern "^\[DEBUG\]:" debug
```

Reset all redirections:

```bash
TECHIO> redirect-streams --reset
```


