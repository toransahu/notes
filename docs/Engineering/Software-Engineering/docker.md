# Docker

# Dockerfile

## `RUN`

- https://docs.docker.com/engine/reference/builder/#run

## `CMD`

- https://docs.docker.com/engine/reference/builder/#cmd

## `ENTRYPOINT`

- https://docs.docker.com/engine/reference/builder/#entrypoint

## RUN vs CMD vs ENTRYPOINT


- RUN executes command(s) in a new layer and creates a new image. E.g., it is often used for installing software packages.
- CMD sets default command and/or parameters, which can be overwritten from command line when docker container runs.
- ENTRYPOINT configures a container that will run as an executable.

Ref:

- https://codewithyury.com/docker-run-vs-cmd-vs-entrypoint/

## `COPY`

# Pull

# Push

# Build
- build outside docker context
    - https://www.jamestharpe.com/docker-include-files-outside-build-context/
    - https://stackoverflow.com/questions/60713751/where-to-put-dockerignore

# Run

# exec

# mount volume

# mount/bind executables?

# networks

# Docker at GCP
- https://cloud.google.com/build/docs/build-push-docker-image#build_using_dockerfile

# Best Practices

## Multiple RUN Vs Single Chained RUN


Dockerfile.1 executes multiple RUN:

```docker
FROM busybox
RUN echo This is the A > a
RUN echo This is the B > b
RUN echo This is the C > c
```

Dockerfile.2 joins them:

```docker
FROM busybox
RUN echo This is the A > a &&\
    echo This is the B > b &&\
    echo This is the C > c
```

Each RUN creates a layer, so I always assumed that fewer layers is better and thus Dockerfile.2 is better.

This is obviously true when a RUN removes something added by a previous RUN (i.e. yum install nano && yum clean all), but in cases where every RUN adds something, there are a few points we need to consider:

- Layers are supposed to just add a diff above the previous one, so if the later layer does not remove something added in a previous one, there should not be much disk space saving advantage between both methods.
- Layers are pulled in parallel from Docker Hub, so Dockerfile.1, although probably slightly bigger, would theoretically get downloaded faster.
- If adding a 4th sentence (i.e. echo This is the D > d) and locally rebuilding, Dockerfile.1 would build faster thanks to cache, but Dockerfile.2 would have to run all 4 commands again.

So, the question: Which is a better way to do a Dockerfile?
Ref: https://stackoverflow.com/questions/39223249/multiple-run-vs-single-chained-run-in-dockerfile-which-is-better

A. Can't be answered in general as it depends on the situation and on the use of the image (optimize for size, download speed, or building speed) 
B. When possible, I always merge together commands that create files with commands that delete those same files into a single RUN line.
C. Split up layers based on their potential for reuse in other images and expected caching usage.
D. Order in the Dockerfile is important when looking at image cache reuse. Look at any components that will update very rarely, possibly only when the base image updates and put those high up in the Dockerfile. Towards the end of the Dockerfile, include any commands that will run quick and may change frequently, e.g. adding a user with a host specific UID or creating folders and changing permissions.
E. In each of these groups of changes, consolidate as best you can to minimize layers.
F. Use multi-stage builds whenever possible.

Ref: https://medium.com/@esotericmeans/optimizing-your-dockerfile-dc4b7b527756

# FAQ

Q.

```
 > [9/9] RUN apt-get update     && apt-get install -y libffi-dev git     && rm -rf /var/lib/apt/lists/*     && pip install --no-cache-dir --upgrade pip     && pip install --no-cache-dir -r /dataflow/plombier/src/requirements.txt     && pip download --no-cache-dir --dest /tmp/dataflow-requirements-cache -r /dataflow/plombier/src/requirements.txt:
#13 0.931 Get:1 http://security.debian.org/debian-security bullseye-security InRelease [44.1 kB]
#13 0.931 Get:2 http://deb.debian.org/debian bullseye InRelease [116 kB]
#13 1.324 Err:1 http://security.debian.org/debian-security bullseye-security InRelease
#13 1.324   At least one invalid signature was encountered.
#13 1.485 Err:2 http://deb.debian.org/debian bullseye InRelease
#13 1.485   At least one invalid signature was encountered.
#13 1.715 Get:3 http://deb.debian.org/debian bullseye-updates InRelease [39.4 kB]
#13 1.815 Err:3 http://deb.debian.org/debian bullseye-updates InRelease
#13 1.815   At least one invalid signature was encountered.
#13 1.821 Reading package lists...
#13 1.833 W: GPG error: http://security.debian.org/debian-security bullseye-security InRelease: At least one invalid signature was encountered.
#13 1.833 E: The repository 'http://security.debian.org/debian-security bullseye-security InRelease' is not signed.
#13 1.833 W: GPG error: http://deb.debian.org/debian bullseye InRelease: At least one invalid signature was encountered.
#13 1.833 E: The repository 'http://deb.debian.org/debian bullseye InRelease' is not signed.
#13 1.833 W: GPG error: http://deb.debian.org/debian bullseye-updates InRelease: At least one invalid signature was encountered.
#13 1.833 E: The repository 'http://deb.debian.org/debian bullseye-updates InRelease' is not signed.
------
executor failed running [/bin/sh -c apt-get update     && apt-get install -y libffi-dev git     && rm -rf /var/lib/apt/lists/*     && pip install --no-cache-dir --upgrade pip     && pip install --no-cache-dir -r $PYTHON_REQUIREMENTS_FILE     && pip download --no-cache-dir --dest /tmp/dataflow-requirements-cache -r $PYTHON_REQUIREMENTS_FILE]: exit code: 100
```

A: https://stackoverflow.com/questions/62473932/atleast-one-invalid-signature-was-encountered

```
docker builder prune
```
