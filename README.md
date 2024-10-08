# 🐳  Velocity Docker Image

[![Watch velocity release](https://github.com/treysu/velocity/actions/workflows/watch-releases.yaml/badge.svg)](https://github.com/treysu/velocity/actions/workflows/watch-releases.yaml)
[![GitHub](https://img.shields.io/github/license/treysu/velocity?color=informational)](https://github.com/treysu/velocity/blob/main/LICENSE)

This project is a work in progress. It is a fork of another project, now archived.

This is a [Velocity](https://velocitypowered.com/) docker image with optimized Java flag provided by official [docs](https://velocitypowered.com/wiki/users/getting-started/).

We use [GitHub Actions](https://github.com/treysu/velocity/actions) to track Velocity builds and automatically build Docker image.

## What is Velocity?

Velocity is a next-generation Minecraft proxy focused on scalability and flexibility.
It allows server owners to link together multiple Minecraft servers so they may appear as one.

### Blazing fast, extensible, and secure — choose three.

Velocity is blazing fast. 
Fast logins, fast server switches, optimizations to get the most from your server's hardware, and a focus on security means you can finally have plugins, a highly optimized proxy resilient to attacks, and protection against your backend servers being accessed by malicious users — no compromises required.

### Always there for you.
Velocity powers some of the world's largest Minecraft networks along with numerous small networks. 
Velocity can scale to thousands of players per proxy instance. Best of all, it works with Paper, Sponge, Forge, Fabric, and all versions of Minecraft from 1.7.2 to 1.18.1.

For more information, please reach to [Velocity official documentation](https://velocitypowered.com/wiki).

![Velocity](assets/velocity.png)

## How to use this image

### Start a Velocity server

With this image, you can create a new Velocity Minecraft proxy server with one command.
Here is an example:

```bash
sudo docker run -p 25577:25577 treysu/velocity:stable
```

While this command will work just fine in many cases, it is only the bare minimum required to start a functional server and can be vastly improved by specifying some options.

## How to extend this image

There are many ways to extend the `treysu/velocity` image. Without trying to support every possible use case, here are just a few that we have found useful.

### Environment Variables

The `treysu/velocity` image uses several environment variables which are easy to miss.
`JAVA_MEMORY` environment variable is not required, but it is highly recommended to set an appropriate value according to your usage.

#### `JAVA_MEMORY`

This variable is not required, but is highly recommended.
By setting this value, you set the java `-Xms` and `Xmx` flag.
For more information about JVM memory size, refer to this [Oracle guide](https://docs.oracle.com/cd/E21764_01/web.1111/e13814/jvm_tuning.htm#PERFM160).

Default: `512M`

#### `JAVA_FLAGS`

This optional environment variable is used in conjunction with `JAVA_MEMORY` to provide additional java flag.
We use [Velocity officially recommended value](https://velocitypowered.com/wiki/users/getting-started/) as the default value.

Default: `-XX:+UseStringDeduplication -XX:+UseG1GC -XX:G1HeapRegionSize=4M -XX:+UnlockExperimentalVMOptions -XX:+ParallelRefProcEnabled -XX:+AlwaysPreTouch`

### Volume

The server data is stored in `/data` folder, and we create a volume for you.
To use your host directory to store data, please mount volume by adding the following options:

Using volume:
```bash
-v <my_volume_name>:/data
```

Using bind mount:
```bash
-v </path/to/folders>:/data
```

## Image Variants

The `treysu/velocity` images come in many flavors, each designed for a specific use case.

### `treysu/velocity:stable`

This is the stable image.
If you are unsure about what your needs are, you probably want to use this one.
It is designed to be used both as a throw away container (mount your source code and start the container to start your app), as well as the base to build other images off of.

### `treysu/velocity:latest`

This is the development build of the image.
Only use this image when you need the cutting edge features or want to try something new.

**It is not recommended to run this image in production environment.**

### `treysu/velocity:<version>-SNAPSHOT`

This is the snapshot image for each development build. 
The latest snapshot build is tagged `latest`.

**It is not recommended to run these image in production environment.**

## LICENSE

Be careful using this container image as you must meet the obligations and conditions of the [GPLv3 ](https://github.com/PaperMC/Velocity/blob/dev/3.0.0/LICENSE) provided by the [Velocity](https://github.com/PaperMC/Velocity) development team.

The code for the [project](https://github.com/treysu/velocity) that builds the [`treysu/velocity`](https://hub.docker.com/r/treysu/velocity) image and pushes it to Docker Hub is distributed under the [MIT License](https://github.com/treysu/velocity/blob/main/LICENSE).

Please, don't confuse the two licenses.
