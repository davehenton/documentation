---
title: Using the Jet CLI
description: Technical documentation for Codeship Pro's CLI (Jet) that allows to debug and run builds locally on the development machine
menus:
  pro/jet:
    title: Using the Jet CLI
    weight: 2
tags:
  - docker
  - jet
  - introduction
  - installation
  - running locally
  - debug
  - setup
  - troubleshooting
  - cli
categories:
  - CLI
redirect_from:
  - /docker/installation/
  - /pro/installation/
  - /pro/getting-started/installation/
  - /docker/cli/
  - /pro/cli/
  - /jet/
  - /docker/getting-started/installation/
  - /pro/builds-and-configuration/cli/
---

{% csnote info %}
If you are unfamiliar with Codeship Pro, we recommend our [getting started guide]({{ site.baseurl }}{% link _pro/quickstart/quickstart-examples.md %}) or [the features overview page](https://codeship.com/features/pro).
Note that if you are using Codeship Basic, you will not be able to use the local CLI.
{% endcsnote %}

* include a table of contents
{:toc}

## Using The Jet CLI

To list available commands, run `jet` with no parameters, `jet -h` or `jet --help`:

```shell
$ jet

Usage:
  jet [command]

Available Commands:
  cleanup     Remove docker resources left behind by jet
  decrypt     Decrypt a file using an AES key
  encrypt     Encrypt a file using an AES key
  generate    Generate an AES key for encrypting files
  help        Help about any command
  load        Pull or build service images
  run         Run a command inside a service container
  steps       Run steps
  update      Download and install the latest version of Jet
  validate    Validate codeship-services.yml and codeship-steps.yml files
  version     Display the jet version

Flags:
  -h, --help   help for jet

Use "jet [command] --help" for more information about a command.
```
## Troubleshooting With Jet

Because the Jet CLI accurately reproduces your CI/CD build pipeline locally, you can use it to quickly solve difficult problems.

For instance, if a test or command fails on a build in Codeship, you can try to reproduce the error with `jet steps`. When you want to test a change, `jet steps` will let you verify the change is working prior to committing so that you don't have to wait for the full build to run remotely to get feedback.

We recommend that developers using Codeship make use of the Jet CLI to improve productivity and solve build-related issues.

### Local Images

By default, Docker will use existing images when running `jet` locally. This may lead to builds passing locally, and failing remotely on Codeship due to the remote environment starting without any prior images and therefore building an image that may be newer or different than your existing local image.

We recommend removing any locally saved Docker images prior to running `jet steps` for a more consistent result to the remote server if you are seeing this issue.

### Results from 'jet steps' differ from my build on CodeShip Pro, why might that be?

- Jet tool is out of date
- Jet is relying on an outdated Docker image stored on your local machine Docker Host
- Resource constraints for the allotted CodeShip Pro instance size are forcing processes to be killed on CodeShip Pro builds, while processes run uninterrupted with `jet steps`
- Files are present on the local machine project folder that would not be otherwise present in a freshly cloned version of the repository
- Volumes may be configured to map absolute pathed Docker Host directories
- Outdated Docker Engine version
- Jet presumes the presence of certain CI environment variables that are not present during `jet steps`
- Golang template objects are not present for 


## Examples

### Display help text
To list the help for any command, execute the command followed by the `-h` or `--help` flag.

```shell
$ jet steps -h
Run steps

Usage:
  jet steps [flags]

Flags:
      --ci-branch string                  The name of the branch being built
      --ci-build-id string                The id of the build being run
...
```

### Option types

#### Multi
Some flags like -e=[ ] may be used multiple times in a single command line, for example:

```shell
$ jet steps -e foo=bar -e baz=qux
```

#### String and Integers
Some flags require a string like `--ci-branch` and can only be specified once.

```shell
$ jet steps --ci-branch master
```
