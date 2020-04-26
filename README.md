# Webtin

## Depends

[TinTin++](https://tintin.mudhalla.net)

[ttyd](https://github.com/tsl0922/ttyd)

## Usage

### Quickstart

Install Docker:

* (Debian/Ubuntu): `sudo apt install docker.io`
* (Arch/Manjaro): `sudo pacman -S docker`

Add yourself to the docker group (this is optional, but avoids the need for calling `sudo` a bunch of times):

```
sudo usermod -aG docker ${USER}
```

Logout to take effect. Then:

```
docker run -it -p 3000:3000 -v $(pwd):/data rpolve/webtin
```

Point your web browser to _localhost:3000_ and it's done.

Tintin will read a _config.tin_ file script from the directory where the container was launched.

The latter can be changed by substituting `$(pwd)` with the absolute path of your choice.

### Important note on security

Add `#CONFIG {CHILD LOCK} ON` to _config.tin_ in order to prevent users from __getting command line access to the insides of the container__.

Although this is not much of a concern, given that it still is _just_ a container, it definitely is conceptually wrong when serving mulptiple users, as some of them could for example edit, rename or delete _config.tin_ (and not much else). This is an advantage of using a cointainer, instead of setting up _ttyd_ and _tt++_ separately on the host machine.

If for some reason you do not want a child locked session, you can still fine-tune permissions in the folder from which you launched the container (or any folder that will be mounted as a volume with the `-v` flag), as they will be inherited by the user inside the container.

### Port forwarding

`-p <x>:<y>` means matching port \<x> on the host to port \<y> within the container. By construction, Webtin listens to port 3000, but you can change \<x> to whichever port you like, e.g. `-p 80:3000` for default http port.

### Running in the background

Launch the container in detached mode:

```
docker run -d -p 3000:3000 -v $(pwd):/data rpolve/webtin
```

See `docker run --help` and `docker stop --help`.

### Resource constraints

Docker provides runtime options for limiting CPU and memory usage. [See here](https://docs.docker.com/config/containers/resource_constraints/).

### Raspberry Pi

An Arm compatible image is available by pulling `rpolve/webtin:rpi`.

## About Docker

[Docker intro](https://docs.docker.com/get-started/overview/).

## Acknowledgements

Thanks to Scandum and Eldakar for the much appreciated insights.
