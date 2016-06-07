# Dockerized go-fresh
[Fresh](https://github.com/pilu/fresh) is a wonderfull little tool that rebuild and serve your Golang project.

This docker image provides a way to be able to serve your project in a container.

# Tags

- :latest, :1.6 => go 1.6


# Usage


**Important:** your project **must** be mounted in `/go/src/<project name>` to let golang be able to import your packages.

Instead of trying to `go get` required packages for your project, please use "Godep" or (better) "[Glide](https://github.com/Masterminds/glide)". 

Get the image and serve:

```bash
# 1.6 => go version
docker pull metal3d/go-fresh:1.6
# be sure that "my-project" is the same directory name
# as your local project
PROJECT=/go/src/my-project

# Change ports to map your own project
docker run --rm -it \
    -v $(pwd)/$PROJECT \
    -w $PROJECT \
    -p 8000:8000 \
    metal3d/go-fresh:1.6
```

And now, changing your go sources will rebuild and serve again.


You can add a configuration file:

```bash
# 1.6 => go version
docker pull metal3d/go-fresh:1.6
# be sure that "my-project" is the same directory name
# as your local project
PROJECT=/go/src/my-project

# Change ports to map your own project
docker run --rm -it \
    -v $(pwd)/$PROJECT \
    -w $PROJECT \
    -p 8000:8000 \
    metal3d/go-fresh:1.6 \
    -c myconf.file
```

# With Docker-compose

An example:

```yaml
version: '2'
services:
    app:
        image: metal3d/go-fresh:1.6
        command: -c myconf.conf
        working_dir: /go/src/my-project
        volumes:
        - ./:/go/src/my-project
        ports:
        - 8000:8000
```


