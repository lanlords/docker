Lanlords Docker Images
----------------------

Docker images for the game servers used on Lanlords. At the moment these are not
automatically build.

> ***Note:***
> *Some games like Call of Duty require game files. These files are not included.*
> *For Lanlords specifically, the links to these files can be found in the wiki.*

| Game                             | Image                                                                                    |
|----------------------------------|------------------------------------------------------------------------------------------|
| Battlefield 2                    | [lanlords/bf2](https://cloud.docker.com/u/lanlords/repository/docker/lanlords/bf2)       |
| Battlefield 1942                 | [lanlords/bf1942](https://cloud.docker.com/u/lanlords/repository/docker/lanlords/bf1942) |
| Battlefield 2142                 | [lanlords/bf2142](https://cloud.docker.com/u/lanlords/repository/docker/lanlords/bf2142) |
| Battalion 1944                   | [lanlords/bt1944](https://cloud.docker.com/u/lanlords/repository/docker/lanlords/bt1944) |
| Chivalry: Medieval Warfare       | [lanlords/cmw](https://cloud.docker.com/u/lanlords/repository/docker/lanlords/cmw)       |
| Call of Duty 2                   | [lanlords/cod2](https://cloud.docker.com/u/lanlords/repository/docker/lanlords/cod2)     |
| Call of Duty 4                   | [lanlords/cod4](https://cloud.docker.com/u/lanlords/repository/docker/lanlords/cod4)     |
| Call of Duty 5                   | [lanlords/cod5](https://cloud.docker.com/u/lanlords/repository/docker/lanlords/cod5)     |
| Counter-Strike: Global Offensive | [lanlords/csgo](https://cloud.docker.com/u/lanlords/repository/docker/lanlords/csgo)     |
| Team Fortress 2                  | [lanlords/tf2](https://cloud.docker.com/u/lanlords/repository/docker/lanlords/tf2)       |

#### Directories

* The `games` directory contains all game server docker image data.
* The `system` directory contains all system/infrastructure docker image data.

#### Development

To locally build the images you will have to cd to the game directory and execute a build, for example:
```
cd games/cod2
docker build -t cod2:test .
```

#### Commands

Run container in the background:
```
docker run -d -t cod2:test
```
Run container and start a shell (for debugging):
```
docker run -ti cod2:test /bin/bash
```
Open a shell in running container (for debugging):
```
docker exec -it --user root [container_id] /bin/bash
```
