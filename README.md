# palisade-docker-build
Docker images for Palisade crypto lib https://gitlab.com/palisade  It can be helpful to kick-off development without having to know too much about the build process. Also, since the artifacts are in the image, builds are incremental and thus faster.

```
docker pull danielscain/palisade-development
```

Other images
* https://hub.docker.com/repository/docker/danielscain/palisade-development
* https://hub.docker.com/repository/docker/danielscain/palisade-encrypted-circuit-emulator



# Build
First, build Ubuntu base to decrease re-build time later.

```bash
git clone https://github.com/dscain/palisade-docker-build.git
cd palisade-docker-build
docker build -f ./Dockerfile.UbuntuBase -t ubuntu-base .
```

Then build Palisade libs and push the images:

```bash
TAG=v1.11.0-dev
docker build -f ./Dockerfile.PalisadeDevelopment -t danielscain/palisade-development:$TAG . --build-arg tag=$TAG
docker build -f ./Dockerfile.PalisadeEncryptedCircuitEmulator -t danielscain/palisade-encrypted-circuit-emulator:$TAG . --build-arg tag=$TAG
docker push danielscain/palisade-development:$TAG
docker push danielscain/palisade-encrypted-circuit-emulator:$TAG
```

## Test
```bash
docker run -v $(pwd):/palisade -p 50022:22 -ti danielscain/palisade-development /bin/bash
```

# Pushing
Push the images:
```bash
TAG=v1.11.0
docker push danielscain/palisade-development:$TAG
docker push danielscain/palisade-encrypted-circuit-emulator:$TAG
```
