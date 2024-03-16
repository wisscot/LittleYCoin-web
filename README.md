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
1. put `index.html` and `404.html` in root folder or `docs` folder. 
2. Verify the domain in User profile - Setting (Note not in the repo - Setting)
3. Add A, AAAA and CNAME to the domain name provider DNS records.  Similar to [DNS records for your custom domain](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/managing-a-custom-domain-for-your-github-pages-site#dns-records-for-your-custom-domain)