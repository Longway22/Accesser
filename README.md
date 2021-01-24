# Accesser

*forked from [github.com/URenko/Accesser](https://github.com/URenko/Accesser)*

Evading SNI-based TCP reset attack using [Domain Fronting](https://en.wikipedia.org/wiki/Domain_fronting)

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

You can add rules in [config.json](config.json.default)'s `alert_hostname`, ordering Accesser use specified SNI for specified site, Accesser will check the certificates is correct for that SNI

**But for an incorrect certificate Accesser only print a WARNING and won't abort the connection**


**A MITM attack is possible**

## Notes for CDNs

Move to <https://rentry.co/Accesser_Notes_For_CDNs>
