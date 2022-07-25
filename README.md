# Jellyfin Synology transcode - Docker mod for HW transcoding with Jellyfin on Synology NAS

This mod adds packages to enable transcoding for synology NAS to jellyfin, to be installed/updated during container start.

Successfully tested on a DS918+. I enabled VAAPI, was not able to get QSV to work for now.

In jellyfin docker arguments, set an environment variable `DOCKER_MODS=kevynb/mods:jellyfin-syno-transcode`

If adding multiple mods, enter them in an array separated by `|`, such as `DOCKER_MODS=kevynb/mods:jellyfin-syno-transcode|linuxserver/mods:jellyfin-mod2`

Do not forget to add the devices to the compose file

```
    devices:
      - /dev/dri/renderD128:/dev/dri/renderD128
      - /dev/dri/card0:/dev/dri/card0
```

You also need to give access to the device from the NAS.

Quick and dirty way is to run this command on the synology:

```
sudo chmod 666 /dev/dri/renderD128
```

A better way would be to create a group and add the user running jellyfin to it and then to only `chmod 660` but I was not able to get this working properly (and did not want to spent too much time investigating).