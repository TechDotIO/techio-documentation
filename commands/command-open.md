# TECHIO> open
# Usage

```bash
TECHIO> open [--port <PORT>] [PATH]
TECHIO> open [--static-dir <DIR>] [PATH]
```

# Description
Opens an HTTP communication with the runner through a client <iframe>. The PATH used to load the <iframe> is `/` if no value is specified.

A maximum lifetime of 2 minutes is set to your runner after the last received request. Thus, your runner can live longer than the standard 30 seconds maximum allowed.

# Options

`-p, --port <PORT>` PORT that will receive the request from the client. If it is not specified, the system will try to use the first exposed port in your Dockerfile (through the EXPOSE directive). If no port is exposed, the default value is 80.


`-s, --static-dir <DIR>` The system can consider the given DIR as a directory of static files to serve as resources to your <iframe>. In this case, the files can be served even after the end of the runner execution. No extra time is added to the standard Runner lifetime.


# Examples
Serves the content of the /data/public_html directory to the client <iframe> and load the default path: /

```bash
TECHIO> open --static-dir /project/target/data/public_html
```

Serves and forwards the client requests to a tomcat server (running within the Runner container on the port 8080). Loads as initial path: /pages/lesson2.jsp.

```bash
TECHIO> open --port 8080 /project/target/pages/lesson2.jsp
```
