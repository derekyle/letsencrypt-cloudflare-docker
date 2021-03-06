## Synopsis

A docker container which handles letsencrypt certificate creation and renewal with DNS validation using the Cloudflare DNS API.

## Code Example

Should be run with:

    docker run --rm -it \
    --name="letsencrypt" \
    -e CF_EMAIL='<CLOUDFLARE_EMAIL>' \
    -e CF_KEY='<CLOUDFLARE_KEY>' \
    -e CERT_DOMAINS='<DOMAIN_NAMES>'
    -v letsencrypt/accounts:/letsencrypt/accounts \
    -v letsencrypt/certs:/letsencrypt/certs \
    -v letsencrypt/domains.txt:/letsencrypt/domains.txt:ro \
    tnwhitwell/letsencrypt.sh-cloudflare

The mapped volumes (/letsencrypt/accounts, /letsencrypt/certs, /letsencrypt/domains.txt) should be mapped somewhere static. The certificates will be created in the /certs folder. You can also omit the domains.txt volume map if you are including the CERT_DOMAINS variable. 

## Installation

    git clone https://github.com/tnwhitwell/letsencrypt-cloudflare-docker
    cd letsencrypt-cloudflare-docker
    cp run.sh.example run.sh
    
    open run.sh in an editor
    edit "<CLOUDFLARE_EMAIL>" and "<CLOUDFLARE_KEY>" to match your cloudflare account
    
    cp domains.txt.example domains.txt
    open domains.txt in an editor
    enter domains, one line per certificate, with SAN names as per:

    example.com alternate.com subdomain.example.com

    ./run.sh
    


## Credits

Dig for Alpine:
https://github.com/sequenceiq/docker-alpine-dig/

Inspiration for script:
https://github.com/kappataumu/letsencrypt-cloudflare-hook
