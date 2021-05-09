# Accesser

*forked from [github.com/URenko/Accesser](https://github.com/URenko/Accesser)*

A tool for bypassing SNI-based HTTPS Filtering using [Domain Fronting](https://en.wikipedia.org/wiki/Domain_fronting)

[Supported sites](https://notyet.yogas.ml/ac.yaml)

## Usage

Move to <https://rentry.co/Accesser_Usage>

## Requirements
- Python3.9
- [pyopenssl](https://pyopenssl.org/)
- [sysproxy](https://github.com/Noisyfox/sysproxy)(for Windows)
- dnspython
- [dnscrypt-proxy](https://github.com/jedisct1/dnscrypt-proxy)
- tornado
- tld



## Explanation

Accesser tries TLS handshake without sending SNI

You can add rules in [config.json](config.json.default)'s `alert_hostname`, ordering Accesser use specified SNI for specified site, Accesser will check the certificates is correct for that SNI, print a WARNING if not match, but wont abort connection.

Accesser would abort connection for expired or self-signed certificates.

## Notes for CDNs

Move to <https://rentry.co/Accesser_Notes_For_CDNs>
