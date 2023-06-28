---
name: dockertfazremote
description: Develop inside Docker containers using your local daemon
tags: [local, docker]
icon: /icon/docker.png
---

# Docker - Terraform, Azure CLI & Powershell

## code-server

`code-server` is installed via the `startup_script` argument in the `coder_agent`
resource block. The `coder_app` resource is defined to access `code-server` through
the dashboard UI over `localhost:13337`.

## Repo clone

This template will also clone the requested Git repository

## Locations

This template can be deployed in the same server as Coder or customized to offer options to deploy in other Docker hosts