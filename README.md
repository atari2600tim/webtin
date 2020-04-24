# Webtin

## Usage

### About Docker

[Docker intro](https://docs.docker.com/get-started/overview/)

### Quickstart

Install Docker:

(Arch) `sudo pacman -S docker`
(Ubuntu) `sudo apt install docker.io`

Add yourself to the docker group (optional, otherwise you'll need `sudo` a bunch of times):

```bash
sudo usermod -aG docker ${USER}
```

Logout to take effect. Then:

```bash
docker run -it -p 3000:3000 -v $(pwd):/data rpolve/webtin
```

Point your web browser to _localhost:3000_ and it's done.

Tintin will read a _config.tin_ file script from the current directory.

### Port forwarding

`-p <x>:<y>` means forward port <x> on the host to match port <y> in the container. By construction, webtin listens to port 3000 but you can match it with any port you like on your host by changing <x>, like `-p 80:3000` for default http port.

### Running it in the background

Launch the container in detached mode:

```bash
docker run -d -p 3000:3000 -v $(pwd):/data rpolve/webtin
```

See `docker run --help` and `docker stop --help`.

## Depends

[TinTin++](https://tintin.mudhalla.net)
[ttyd](https://github.com/tsl0922/ttyd)
