---
tags: vpn setup
---

# VPN
This process is created by following this [guide](https://flathub.org/apps/details/net.shrew.ike.qikea)
## Flatpak
Install Flatpak
```bash
sudo apt-get install flatpak
```

Install Shrew Soft VPN via Flatpak
```bash
flatpak install flathub net.shrew.ike.qikea
```

If there's an error during the installation, follow the [instructions](https://itsfoss.com/no-remote-ref-found-flatpak/) running
```bash
flatpak remote-add --if-not-exists flathub https://flathub.org/repo/flathub.flatpakrepo
****```

To run the VPN service, we need a daemon running in the computer. Since this option is not supported since Ubuntu 18.04, we have found this [docker image](https://hub.docker.com/r/beardoverflow/ike) as a workaround.

In order to pull this image, we can either use the original one or use a snapshot built by Teldat for easier use.
```bash
# Teldat image (recommended)
scp <goliath_user>@192.168.213.72:/var/www/html/repo/linux_devenvs/iked.tar iked.tar && docker image load -i iked.tar

# Original image
docker pull beardoverflow/ike
```

Run the daemon with the following command
```bash
docker run -d --name=iked --net=host --privileged -v /etc/resolv.conf:/etc/resolv.conf -v /run:/run beardoverflow/ike
```

## Automate the docker
For easier use, we recommend automating the docker image process so it's automatically executed during startup so we can connect to the VPN with Shrew soft without issue.

Create the file `~/.profile_on_startup` with the following command:
```bash
# VPN Configuration:
# Run iked docker
docker rm -f iked &> /dev/null && docker run -d --name=iked --net=host --privileged -v /etc/resolv.conf:/etc/resolv.conf -v /run:/run beardoverflow/ike
```

Append to the end of  `~/.profile` to call the new file
```bash
# Call on startup
if [ -f ~/.profile_on_startup ]; then
    . ~/.profile_on_startup
fi
# End of calls on startup
```

