# GitBucket on Docker

A Dockerfile for deploying a [GitBucket](https://github.com/gitbucket/gitbucket) which is a GitHub API compatible Git platform using Docker container.

This image is registered to the [Docker Hub](https://hub.docker.com/r/nutsllc/toybox-gitbucket/) which is the official docker image registory.

## What is the GitBucket

>GitBucket is a Git platform powered by Scala offering:
>
>* easy installation
* high extensibility by plugins
* API compatibility with Github

>The current version of GitBucket provides a basic features below:

>* Public / Private Git repository (http and ssh access)
* Repository viewer and online file editing
* Wiki
* Issues / Pull request
* Email notification
* Simple user and group management with LDAP integration
* Plug-in system

[GitHub Registry](https://github.com/gitbucket/gitbucket) of the GitBucket 

## Docker Compose example

```
gitbucket:
    image: nutsllc/toybox-gitbucket:4.1.0
    links:
        - mariadb:mysql
    environment:
        - TOYBOX_UID=1000
        - TOYBOX_GID=1000
    volumes_from:
        - data
    volumes:
        - "/etc/localtime:/etc/localtime:ro"
    ports:
        - "29418:29418"
        - "8080:8080"

mariadb:
    image: nutsllc/toybox-mariadb:10.1.14
    volumes:
        - "/etc/localtime:/etc/localtime:ro"
    volumes_from:
        - data
    environment:
        - MYSQL_ROOT_PASSWORD=root
        - MYSQL_DATABASE=toybox_gitbucket
        - MYSQL_USER=toybox
        - MYSQL_PASSWORD=toybox
        - TERM=xterm
        - TOYBOX_UID=1000
        - TOYBOX_GID=1000

data:
    image: busybox:buildroot-2014.02
    volumes:
        - "./.data/gitbucket:/gitbucket"
        - "./.data/mariadb:/var/lib/mysql"
```

and then, access from web browser to ``http://<Hostname(IP Address)>:8080`` and sign-in with initial account. username: ``root`` password: ``root``

## License

* [GitBucket](https://github.com/gitbucket/gitbucket) Apache 2.0

## Contributing

We'd love for you to contribute to this container. You can request new features by creating an [issue](https://github.com/nutsllc/toybox-gitbucket/issues), or submit a [pull request](https://github.com/nutsllc/toybox-gitbucket/pulls) with your contribution.