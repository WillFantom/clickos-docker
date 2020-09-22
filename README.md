# Dockerized ClickOS Image Builder

This repo does not contain any source code from `ClickOS`, but simply contains the means to build `ClickOS` images within a Docker container.

## Tags

 - `sysml`
   - This tag contains a prebuilt ClickOS image that uses the default build args. The idea for is not only to distribute images, but to make building reproducibly simple.
   - To simple get the ClickOS image, run the following command:
      ```bash
      docker run --rm -v $(pwd):/output willfantom/clickos:sysml
      ```
   - To build with arguments defined by you, run the following with any build args you need (stats_level just an example):
      ```bash
      docker build --rm -f Dockerfile --build-arg STATS_LEVEL=1 -t clickos:custom .
      ```

 - `development`
   - This tag provides an image for ClickOS development. It has the Xen and MiniOS sources and a built toolchain. It only needs you to bring your own ClickOS.
   - To get started, from your root ClickOS directory, run:
      ```bash
      docker run --rm -it -v $(pwd):/sources/clickos willfantom/clickos:development
      ```
     - The Xen/MiniOS version can also be important, so change these with the build args if needed.
        ```bash
        docker build --rm -f Dockerfile.dev --build-arg MINIOS_BR=<other-br> -t clickos:dev .
        ```

## Args

|      ARG       |         Tags          |                                                                       Description                                                                        |                Default                |
| :------------: | :-------------------: | :------------------------------------------------------------------------------------------------------------------------------------------------------: | :-----------------------------------: |
|   `XEN_REPO`   | `sysml`,`development` |                                                    The remote git repo containing the Xen source code                                                    |  https://github.com/xen-project/xen   |
|    `XEN_BR`    | `sysml`,`development` |                                                     The branch or tag of the Xen source repo to use                                                      |            RELEASE-4.11.4             |
| `MINIOS_REPO`  | `sysml`,`development` |                                                  The remote git repo containing the MiniOS source code                                                   |   https://github.com/sysml/mini-os    |
|  `MINIOS_BR`   | `sysml`,`development` |                                                    The branch or tag of the MiniOS source repo to use                                                    |                master                 |
| `CLICKOS_REPO` |        `sysml`        |                                                  The remote git repo containing the ClickOS source code                                                  | https://github.com/willfantom/clickos |
|  `CLICKOS_BR`  |        `sysml`        |                                                   The branch or tag of the ClickOS source repo to use                                                    |                latest                 |
| `STATS_LEVEL`  |        `sysml`        | The stats level to enable for ClickOS: <br> `0`: Normal Stats Level <br> `1`: Collect per-element packet counts <br> `2`: Collect CPU cycles per-element |                   0                   |
| `EXTRA_FLAGS`  |        `sysml`        |                              Any extra flags as a string for the configure stage <br> (e.g. `--with-netmap --enable-ipsec`)                              |                                       |

> The main tag here `sysml` does **not** use the `sysml/clickos` repo currently as it does not compile with the `master` MiniOS branch. It uses pretty much the same code though, just configured so it can compile.