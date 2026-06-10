# Troubleshooting

Several issues happened because the commands were being run in Windows PowerShell instead of Linux Bash.

## curl issue

The command:

```powershell
curl -k https://localhost:10000
```

did not work correctly because PowerShell treats `curl` differently.

The working command was:

```powershell
curl.exe -k https://localhost:10000
```

## grep issue

The command:

```powershell
docker inspect cve-2019-15107-web-1 | grep '"IPAddress"'
```

did not work because `grep` is not a PowerShell command.

The PowerShell replacement was:

```powershell
docker inspect cve-2019-15107-web-1 | Select-String '"IPAddress"'
```

A cleaner command was:

```powershell
docker inspect -f "{{range .NetworkSettings.Networks}}{{.IPAddress}}{{end}}" cve-2019-15107-web-1
```

## Container name issue

The correct container name was:

```text
cve-2019-15107-web-1
```

The incorrect container name used earlier was:

```text
cve-2019-15107_web_1
```

The issue was fixed by using the correct hyphenated container name.

## Metasploit connection issue

Using the container IP `172.19.0.2` caused Metasploit check errors.

The working target address was:

```text
RHOSTS 127.0.0.1
```

because Docker exposed Webmin on:

```text
https://localhost:10000
```

The Docker gateway was used for callback testing:

```text
LHOST 172.19.0.1
```

The exploit reached the endpoint, but no reverse shell session was created during the recorded attempt.
