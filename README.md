# Proof

Instant feedback on static web content. Once configured, allows fast
and easy iteration and sharing of static front-end content via a server
configured with [nginx](http://nginx.org).

Let's assume **you're working on a front-end project**; could be an angular app
or just iterating on a design. **You're using [gulp]() or [broccoli]()** to
build your front-end structure and assets into a `dist` directory. You want
to **get some quick feedback from a coworker or client**.

You're in your project directory: `~/code/foo` and you run

```
~/code/foo $ proof
```

and **poof** your content is available at http://static.adorable.io/foo

## Installation

1. Clone the repo

        git clone https://github.com/adorableio/proof.git

1. Copy the script

        cd proof
        cp ./proof /usr/local/bin/proof

1. Copy the example global config to your home directory

        cp .proofrc.global ~/.proofrc.global

1. Copy the `proof_rsa` and `proof_rsa.pub` files from the 1Password vault to your `~/.ssh` directory.
1. Add the following block to your `~/.ssh/config` file:

        Host proof static.adorable.io
          Hostname static.adorable.io
          User abott
          IdentityFile ~/.ssh/proof_rsa

## Usage

```
Usage: proof [-h] [-s] [-r]

Pushes static site content to a configured server.

  -h    Show usage/help
  -s    Silent mode (suppresses confirmation before acting)
  -r    Remove project from server
```

## Configuration
There are several different client configurations to manage: **global**, and
**per-project**. The global configuration manages defaults about the server,
whereas the per-project one manages any overrides or settings for the
particular project.

### Global
The global configuration is stored in `~/.proofrc.global` and defines defaults
for any project you push from your machine.

```sh
# The default server to SSH into
default_server=static.adorable.io
# The default relative directory to rsync to the server
default_target=dist
# The default root directory to rsync to on the server
default_docroot=/var/www/html/$default_server
# The key file to use for the server
default_key_file=~/.ssh/proof_rsa
# The public key to use for the server
default_pub_file=~/.ssh/proof_rsa.pub
```

### Per-Project
The per-project configuration defines the specific settings used when pushing
the current project contents to the server.

```sh
# Server this project is pushed to
server=static.adorable.io
# Local relative directory to push content from
target=dist
# Remote name/subdirectory used for the project
name=proof
```

### Server

