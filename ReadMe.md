# Dockerized ClickOS Image Builder

Container that can be used to build ClickOS unikernel images in a reproducible manner.

This branch `clickos-dev` is to be used for ClickOS development. For this, no ClickOS is pulled in via the dockerfile. It is instead expected that ClickOS will be provided via a shared volume.

## Running

To build, simply run the following command:

```bash
docker build --rm --no-cache -f Dockerfile -t clickos:dev .
```

OR just pull the version from dockerhub (be aware, this uses default values for the XEN and MINIOS versions):

```bash
docker pull willfantom/clickos:clickos-dev
```

To start the development container:
(This assumes that you are in your working ClickOS directory)

```bash
docker run --rm -v $(pwd):/sources/clickos clickos:dev
```

## Args

The build can be modified using build args in the following ways:

- Repos and Branches:
  - MINIOS_REPO
  - MINIOS_BR
  - XEN_REPO
  - XEN_BR
(Theses are pretty self explanatory)

## CI Info

The CI build pipeline simply builds a basic version of the image with all extra ClickOS element groups disabled and the stats level at 0. The tag for this is simply `latest`.

The pipeline is also triggered by my other ClickOS project(s) and the image is tagged appropriately. For example, the tags used for builds triggered by my ClickOS fork relate to their branch names.