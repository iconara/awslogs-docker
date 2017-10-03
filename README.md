# awslogs

The CloudWatch Logs agent packaged as a Docker image.

## Usage

The image is set up to have `aws logs push` as entrypoint, so to get the documentation you can run `help`:

```shell
$ docker run --rm --init iconara/awslogs:latest help
```

You can push log events from stdin to a stream:

```shell
$ tail -f path/to/some.log | docker run --rm --init --interactive iconara/awslogs:latest --region eu-west-1 --log-group-name my-group-name --log-stream-name my-stream-name
```

Notice the `--interactive` flag, it is required to make stdin open.

To watch and push log events from one or multiple files you must create a configuration file, mount it into the container, and also mount the directories containing the files:

```shell
$ docker run --rm --init --mount type=bind,source=$(pwd)/conf/my.conf,destination=/etc/awslogs/my.conf --mount type=bind,source=$(pwd)/logs,destination=/var/log/my-logs iconara/awslogs:latest --region eu-west-1 --config-file /etc/awslogs/my.conf
```

Run `help` to see examples of log files. Make sure that the `file` directive in the config file refers to the mount point _inside_ the container.

## Copyright & License

© 2017 Theo Hultberg and contributors, use as much as as you like.
