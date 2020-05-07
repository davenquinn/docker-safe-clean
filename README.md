# docker-safe-clean

**Safely clean up docker volumes, containers, and images.**

Docker-centric development workflows can clog your machine with
images, containers, and volumes. Mostly, these can be deleted easily,
but when you are using Docker's opaque volume architecture
[as recommended](https://docs.docker.com/storage/volumes/) you often wind up with
gigabytes of cruft (build cache, dangling `node_modules` folders, etc.)
intermingled with critical data (e.g. database clusters).
The commands required to safely delete *some* but not *all* data
(particularly, volumes) are user-unfriendly
and prone to fat-finger error.

## Usage

This repository includes two `bash` commands that encode some hard-won
best practices for safely cleaning up Docker artifacts:

- `docker-volume-clean` deletes volumes that *don't* match
  a pattern (the default is to keep volumes with names including `_db`,
  `database`, and `_cluster`). The pattern is configurable using the
  `DOCKER_VOLUME_RETENTION_PATTERN` environment variable.
- `docker-safe-clean` runs `docker system prune`, `docker system prune -a`,
  and `docker-volume-clean`
  in sequence, guiding you through deleting different levels of data.

## Installation

Download or clone this repository, and link the two scripts onto your `PATH`!

