# Getting started with `pygame` on Basilisp

## Overview

This project template is designed to help you quickly get started using the [pygame](https://www.pygame.org) library with [Basilisp](https://basilisp.readthedocs.io/en/latest/index.html).

The project uses the [Poetry](https://python-poetry.org/) tool to simplify Python dependency management and handle virtual environments. For installation details, see the [Poetry introduction guide](https://python-poetry.org/docs/).

## Project Anatomy

```
.
├── basilisp.edn             (B)
├── poetry.lock              (1)
├── pyproject.toml           (2)
├── src
│   ├── basilex_pygame       (N)
│   │   └── demo.lpy         (3)
│   └── dev
│       └── nrepl.lpy        (4)
└── tests
    └── __init__.py
    └── basilex_pygame       (N)
        └── test_demo.lpy    (5)
```

🄑 An empty file indicating to Clojure-enabled editors that this is a Basilisp Project.

🄝 The project's namespace.

① A lock file generated by Poetry that records the exact versions of dependencies installed.

② The configuration file where project metadata, dependencies, and Poetry settings are defined.

③ The `pygame` demo source code.

④ An auxiliary namespace that facilitates access to the async nREPL server during development.

⑤ A unit test for the demo code.

## Project Setup

Before running the project for the first time, install the dependencies in a new virtual environment by running
```shell
poetry install
```

Next, activate the project's virtual environment for development with
```bash
poetry shell
```

## Usage

Check the example code in [src/basilex_pygame/demo.lpy](src/basilex_pygame/demo.lpy), which creates a `pygame` window with a cube that can be moved using the cursor keys.

![demo](demo.png)

To interact with Python code from Basilisp, you might want to familiarize yourself with [Basilisp's Python Interop features](https://basilisp.readthedocs.io/en/latest/pyinterop.html).

## Running and Developing the Code

The following steps assume you are using the [`basilisp` CLI tool](https://basilisp.readthedocs.io/en/latest/cli.html) within the activated virtual environment.

To load the namespace and run the demo, use the `run -n` option

```shell
basilisp run -n basilex-pygame.demo
pygame 2.6.0 (SDL 2.28.4, Python 3.11.4)
Hello from the pygame community. https://www.pygame.org/contribute.html
nREPL server started on port 53666 on host 127.0.0.1 - nrepl://127.0.0.1:53666
```

This command will also start an asynchronous nREPL server bound to the local interface on a random port number. Additionally, it creates a `.nrepl-port` file in the current working, directory your favorite Clojure-enabled editor to discover the server.

The async nREPL server is integrated within `pygame`'s main loop, enabling cooperative multitasking between the server and `pygame` on the same thread.

> [!NOTE]
> Using the core `basilisp nrepl-server` is discouraged, as it can cause crashes. This is because running the main loop and the nREPL server on separate threads is not supported by `pygame` or most Python libraries, which require single threaded executions.

## Testing

You can run the sample test located at [tests/basilex-pygame/test_demo.lpy](tests/basilex-pygame/test_demo.lpy) with

```bash
basilisp test
```

Happy coding with Basilisp!
