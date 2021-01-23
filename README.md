# Accesser

*forked from [github.com/URenko/Accesser](https://github.com/URenko/Accesser)*

Evading SNI-based TCP reset attack using [Domain Fronting](https://en.wikipedia.org/wiki/Domain_fronting)

[Supported sites](https://notyet.yogas.ml/ac.yaml)

## Usage
0. If you set dnscrypt true in `config.json`, you must place the executable `dnscrypt-proxy` in `dnscrypt` folder
1. `python3 accesser.py` 
2. Import `CERT/root.crt` as Root CA
3. Use proxy `http://localhost:8000` for desired sites


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

**If no rules is to applied for the site, Accesser will NOT check certificate**

**An MITM attack is possible**

## Notes for CDNs

Move to <https://rentry.co/Accesser_Notes_For_CDNs>