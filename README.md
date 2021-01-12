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

###Akamai

Support TLS handshake without SNI, and does not require SNI extension and HTTP Host header to contain the same domain

###Amazon CloudFront


It does not support TLS handshake without SNI

You must specific correct SNI in [config.json](config.json.default)

#### Example:

For `www.wsj.com` 
Run

$ `dig @208.67.222.222 -p 5353 -t CNAME www.wsj.com | grep CNAME`

```
www.wsj.com.		87	IN	CNAME	dlp0y1mxy0v3u.cloudfront.net. [AWS CloudFront]
```

Or run (If MS Windows)

\> `nslookup -q=cname -port=5353 www.wsj.com 208.67.222.222`

```
Server:		208.67.222.222
Address:	208.67.222.222#5353

Non-authoritative answer:
www.wsj.com	canonical name = dlp0y1mxy0v3u.cloudfront.net.

Authoritative answers can be found from:
```

Add below in [config.json](cnfig.json.default)'s `alert_hostname` field

```
"www.wsj.com": "dlp0y1mxy0v3u.cloudfront.net"
```

### CloudFlare

By default(most sites), it does not support TLS handshake without SNI, and will check if SNI extension and HTTP Host header contains the same domain

Domain Fronting is not possible

### Fastly

Support TLS handshake without SNI, and does not require SNI extension and HTTP Host header to contain the same domain

### StackPath

Support TLS handshake without SNI, and does not require SNI extension and HTTP Host header to contain the same domain

Note: this IP `151.139.128.11` has been blocked using QoS filtering

Other IPs in the range 151.139.128.0/24 is not
