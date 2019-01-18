# xelatex

Use this image:

```bash
docker run --rm -i --volume "$PWD":/data --workdir /data alexislefebvre/docker-images:xelatex bash -c "xelatex main.tex && xelatex main.tex"
```
