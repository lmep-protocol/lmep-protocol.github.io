# LMEP Specification

This is the repo containing the properdocs source for `lmep-protocol.github.io`. This is also my coursework submission for A-level Computer Science. The content and associated markup files for this site are licensed under CC-BY-4.0.

## Building the site

Ensure you have the following installed:

- git
- python

Clone the repo:

```sh
$ git clone https://github.com/lmep-protocol/lmep-protocol.github.io lmep-protocol && cd lmep-protocol
```

Then, set up a virtual environment for Python

```sh
$ python -m venv .venv
```

Source the `activate` file:

```sh
$ source .venv/bin/activate # add `.fish` to the end of this command if you're on fish
```

Then, install dependencies:

```sh
$ pip install -r requirements.txt
```

Once dependencies are installed, localhost the site:
```sh
$ properdocs serve
```

Once this command is run, the site will be available on `localhost:8000`.
