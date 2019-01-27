Detailed instructions on how to install the sinusbot on docker can be found on the [Github Page](https://github.com/SinusBot/docker). You can also check out the image directly on [Docker Hub](https://hub.docker.com/r/sinusbot/docker).

```bash
docker run -d -p 8087:8087 \
    -v scripts:/opt/sinusbot/scripts \
    -v data:/opt/sinusbot/data \
    --name sinusbot sinusbot/docker
```