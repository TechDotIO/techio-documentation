# TECHIO> open
# Usage

```bash
TECHIO> open [--port <PORT>] [PATH]
TECHIO> open [--static-dir <DIR>] [PATH]
```

# Description
Opens an http communication with the runner through a client iframe. The PATH used to load the iframe is / if no value is specified.

A maximum life time of 2 minutes is set to your runner after the last received request. Thus, your runner can live longer than the standard 30 maximum seconds allowed.

# Options

`-p, --port <PORT>` PORT that will receive the request from the client. If not specified, the system will try to use the first exposed port in your Dockerfile (through the EXPOSE directive). If no port is exposed, the default value is 80.


`-s, --static-dir <DIR>` The system can consider the given DIR as a directory of static file to serve as static resources to your iframe. In this case, the files can be served even after the end of the runner execution. No extra time is added to the standard Runner lifetime.


# Examples
Serves the content of the /data/public_html directory to the client iframe and load the default path: /

```bash
TECHIO> open --static-dir /project/target/data/public_html
```

Serves and forward the client requests to a tomcat server (running in the Runner container on the port 8080). Loads as initial path: /pages/lesson2.jsp.

```bash
TECHIO> open --port 8080 /project/target/pages/lesson2.jsp
```
