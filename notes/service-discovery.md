# Service Discovery

The selected target was the Vulhub Webmin CVE-2019-15107 lab.

The Docker container name was:

```text
cve-2019-15107-web-1
```

The Webmin service was reachable at:

```text
https://localhost:10000
```

The service was tested with:

```powershell
curl.exe -k https://localhost:10000
```

The response contained:

```html
<title>Login to Webmin</title>
```

This confirmed that Webmin was running on port `10000` over HTTPS.

The Docker container IP was:

```text
172.19.0.2
```

The Docker gateway was:

```text
172.19.0.1
```

The container had these useful binaries available:

```text
/bin/bash
/usr/bin/perl
/bin/sh
```
