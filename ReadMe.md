# Dockerized ClickOS Image Builder

Container that can be used to build ClickOS unikernel images in a reproducible manner.

## Running

To build, simply run the following command:

```bash
docker build --rm --no-cache -f Dockerfile -t clickos:dev .
```

To get the images:

```bash
docker run --rm -v $(pwd):/output clickos:dev
```

## Args

The build can be modified using build args in the following ways:

- Repos and Branches
  - Set the repo and/or branch of sources with args such as `CLICKOS_REPO` and `CLICKOS_BR`
 - Set extra configure flags for ClickOS with `EXTRA_FLAGS`
 - Set the stats collection level in ClickOS with `STATS_LEVEL`

## CI Info

The CI build pipeline simply builds a basic version of the image with all extra ClickOS element groups disabled and the stats level at 0. The tag for this is simply `latest`.

The pipeline is also triggered by my other ClickOS project(s) and the image is tagged appropriately. For example, the tags used for builds triggered by my ClickOS fork relate to their branch names.