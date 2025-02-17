# RoonBridge
Dockerfile for RoonBridge on Linux x86, x86_64, armv7hf, and armv8

I don't push this to a public registry, so it's best to build it yourself. Roon auto updates can be applied inside the container as with normal installs.

## Building it

```bash
docker build -t roonbridge .
```

## Running it

```bash
docker run --name RoonBridge --rm --device /dev/snd --net=host -d -v roonbridge:/var/roon roonbridge
```

- `host` networking is required because Roon relies on a multicast protocol (SSDP I think, need to verify) to discover the Roon core.
- `/dev/snd` needs to be shared with the container as well. This assumes only 1 sound device is on the system, and already configured.
- A named volume is used to persist logs and the settings file.

## Example setups

### Running on ODroid XU4/HC (armv7hf)

This works great with the provided Ubuntu 18.04 LTS image. I'm using a USB DAC (Meridian Explorer) with the line output hooked up to my home theatre system.

In addition to building the container, I needed to make sure that the `snd-usb-audio` module was loaded.

1. Run `modprobe snd-usb-audio`
2. Modify `/etc/modules-load.d/modules.conf` and add `snd-usb-audio`

### Raspberry Pi 2 (armv7hf)

Same instructions as above to build & run on `Raspbian GNU/Linux 10 (buster)`. I didn't need any extra steps to get `snd-usb-audio` loaded.

### Compulab Fitlet2 (x86_64)

Verified to build & run, haven't tested with audio yet

### Rock64 (armv8)

Not tested yet, hardware not booting after a power glitch
