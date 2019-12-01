# RoonBridge
Dockerfile for RoonBridge on Linux x86, x86_64, armv7hf, and armv8




Open Questions

- [ ] Roon data files are stored in /var/roon. is this necessary to persist?

You currently must use the "host" networking driver with this.




## Building

```bash
docker build -t roonbridge .
```

## Running

```bash
docker run --name RoonBridge --net=host -d -v /home/roon:/var/roon roonbridge
```



