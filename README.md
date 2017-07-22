# dartmonit
Monitor Dart scripts, and run them on startup. This is very early in the development stages, so expect some changes.

Running `dartmonit` as a daemon is currently only supported on Linux and Windows.
# Installation

For Unix/Linux variants:
```bash
pub global activate dartmonit
```

On Windows, you need to clone this repository, and add `bin/dartmonit.bat` to
your `PATH`. The reason for this is that having `dartmonit` saved on your
filesystem allows the `install` command to install the included Windows service,
written in C#, and compiled to an `.exe`.

```batch
git clone https://github.com/thosakwe/dartmonit.git
SET PATH="<dartmonit-root>\bin";%PATH%
```

See
[here](https://www.java.com/en/download/help/path.xml)
for a look at how to set environment variables system-wide.

To add a script to `/etc/init.d`:
```bash
sudo dartmonit env "PATH=$PATH" install
```

Now, you can run it as a service:

```bash
sudo service dartmonit start
sudo /etc/init.d/dartmonit start
```

You may have better luck with the `/etc/init.d` variant, rather than
`service`.

# Usage
dartmonit is essentially an HTTP server,
which runs as a daemon and exposes a simple API.

Most of the CLI commands query a running API.

To manually start the server (not as a daemon):
```bash
dartmonit start
dartmonit start --port 2245
```

`2245` is the default port.

# Commands

```
Usage: dartmonit <command> [arguments]

Global options:
-h, --help    Print this usage information.

Available commands:
  help        Display help information for dartmonit.
  install     Configures dartmonit to run at startup.
  kill        Halts the execution of a given command.
  remove      Removes a command from the list of processes to execute.
  run         Spawns a child process at the given absolute path.
  start       Starts the dartmonit HTTP server.
  status      Fetches the status of a given process.
  stop        Instructs an active dartmonit server to shut down.
  uninstall   Uninstalls the dartmonit daemon.

Run "dartmonit help <command>" for more information about a command.
```

# API
TODO: API documentation