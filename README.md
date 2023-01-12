# Project Title

Hugo static site generator with PaperMod theme for [burakozer.com](burakozer.com)

## Installation

for building to production

```bash
docker-compose up # test from localhost:1313

docker-compose run server shell
hugo --destination docs # built with hugo command for prod  
```
Make sure that Github Pages being built from "/Docs" folder <br>
To use custom domain name, add your CNAME file under "/static" folder
