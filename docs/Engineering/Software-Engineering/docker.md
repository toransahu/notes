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
