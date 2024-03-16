# LittleYCoin-web

## Develop

run local http server under the folder which contains index.html
```bash
python3 -m http.server
```
and use link provided by vscode to visit

## Register domain
Registered littleycoin.com in aws Route 53 manually. Added A and AAAA records for ipv4 and ipv6, respectively. Added CNAME for www subdomain. 

## Hosted in Github Pages
put `index.html` and `404.html` in root folder or `docs` folder. 
