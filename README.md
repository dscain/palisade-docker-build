# palisade-docker-build
Build images for Palisade crypto lib

# Build
First, build Ubuntu base to decrease re-build time later.

```bash
git clone https://github.com/dscain/palisade-docker-build.git
cd palisade-docker-build
docker build -f ./Dockerfile.UbuntuBase -t ubuntu-base .
```

Then build Palisade libs:

```bash
TAG=v1.11.0
docker build -f ./Dockerfile.PalisadeDevelopment -t danielscain/palisade-development:$TAG . --build-arg branch=$TAG  --build-arg tag=$TAG
docker build -f ./Dockerfile.PalisadeEncryptedCircuitEmulator -t danielscain/palisade-encrypted-circuit-emulator:$TAG . --build-arg branch=$TAG  --build-arg tag=$TAG
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
