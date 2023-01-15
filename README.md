# Project Title

Hugo static site generator with PaperMod theme for [burakozer.com](burakozer.com)

## Installation
Normally, the github action pipeline will automatically generate the static codes for .md files under  **gh-pages** branch. 


if you want to **manual** building to production:
```bash
docker-compose up # test it from localhost:1313
#or
docker-compose run server shell #then built with hugo command  
```
To use custom domain name, add your CNAME file under "/static" folder
