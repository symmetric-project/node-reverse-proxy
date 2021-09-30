![license](https://img.shields.io/github/license/symmetric-project/node-reverse-proxy)
![stars](https://img.shields.io/github/stars/symmetric-project/node-reverse-proxy)
![forks](https://img.shields.io/github/forks/symmetric-project/node-reverse-proxy)
![issues](https://img.shields.io/github/issues/symmetric-project/node-reverse-proxy)
![size](https://img.shields.io/github/repo-size/symmetric-project/node-reverse-proxy)
# node-reverse-proxy
The reverse proxy for a Symmetric node. Reddit-like decentralized discussion platform.

## Localhost SSL certificate for development purposes
### Making and trusting your own certificates

Anyone can make their own certificates without help from a CA. The only difference is that certificates you make yourself won’t be trusted by anyone else. For local development, that’s fine. The simplest way to generate a private key and self-signed certificate for localhost is with this openssl command:
```
openssl req -x509 -out localhost.crt -keyout localhost.key \
  -newkey rsa:2048 -nodes -sha256 \
  -subj '/CN=localhost' -extensions EXT -config <( \
   printf "[dn]\nCN=localhost\n[req]\ndistinguished_name = dn\n[EXT]\nsubjectAltName=DNS:localhost\nkeyUsage=digitalSignature\nextendedKeyUsage=serverAuth")
```
You can then configure your local web server with localhost.crt and localhost.key, and install localhost.crt in your list of locally trusted roots.

If you want a little more realism in your development certificates, you can use minica to generate your own local root certificate, and issue end-entity (aka leaf) certificates signed by it. You would then import the root certificate rather than a self-signed end-entity certificate.

You can also choose to use a domain with dots in it, like www.localhost, by adding it to /etc/hosts as an alias to 127.0.0.1. This subtly changes how browsers handle cookie storage.
