DNS verification hook for [acmetool](https://github.com/hlandau/acme) using cloudflare API.

## Usage


Download `dns.hook` to your server. 
Install dependencies: 
- `python3` & request package
- `dig` (usually available in the `dnsutils` apt package)

Allow only yourself to read/write/execute it:
```
$ chmod 700 dns.hook
```

Edit `dns.hook` script. Put your [API_TOKEN](https://dash.cloudflare.com/profile/api-tokens) in the following line and uncomment that:
```python
import requests
import signal
import subprocess
import sys
import time

#KEY = "Your API TOKEN" 

TIMEOUT = 60

```

Test run:
```
$ ./dns.hook test [sub.yourdomain.tld]
```
The script will try to create a TXT record `_acme-challenge.[sub.yourdomain.tld]`, verify it, and delete it.

If it works, copy/move the script to acmetool hooks dir (e.g. `/usr/lib/acme/hooks/`):
```
$ sudo mv dns.hook /usr/lib/acme/hooks/
```

After that, acmetool will find this hook, and it can proceed with dns challange method...
