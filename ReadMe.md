# Dockerized ClickOS Image Builder

### Build ClickOS Images Reproducibly

> This `dev` branch is not an unstable branch feeding into `latest`. It is a Bring Your Own ClickOS (BYOCO) version, intended for building ClickOS images where the ClickOS source is not yet available on any public git repo.

## Usage

To use `dev`, you should run this container with you clickos root directory mounted.

```bash
docker run --rm -v $(pwd):/sources/clickos willfantom/clickos:dev
```
> *assuming you are currently in the clickos root directory*

## Build Image Yourself

If you require to use non default Xen or MiniOS versions, you should build the image yourself rather than pulling from docker hub.

To build, simply run the following command with the [build args](#args) you need:

```bash
docker build --rm --no-cache -f Dockerfile -t clickos:dev .
```

## Args

The build can be modified using build args in the following ways:

- `MINIOS_REPO` URL of public MiniOS repo
- `MINIOS_BR` branch or tag of the given repo
- `XEN_REPO` URL of public Xen Hypervisor repo
- `XEN_BR` branch or tag of the given repo
