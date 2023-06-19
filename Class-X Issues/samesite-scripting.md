# Same Site Scripting
A common practice while configuring nameservers is to install records of following type.
```bash
localhost. IN A 127.0.0.1
```
A mistake, which seems harmless, is to leave off trailing dot at the end. Server parses configuration file in way that localhost is interpreted as hostname within the current domain, instead of domain in itself. What this means is that if you try to use ping command for localhost.target.com, query will resolve.
```bash
ping localhost.target.com
```
# Impact :

This is not high severity vulnerability like XSS, as to exploit this, an attacker needs to be on same machine as you are. If they’re not, they can’t open network port over which, they can serve HTTP traffic to your browser from local machine.

# Attack Scenario :
This DNS misconfiguration makes victims susceptible to attacks if they’re using multi-user systems.

    On shared UNIX system, an attacker listens on an unprivileged port[0] and then uses typical XSS attack vector(eg. img src = …) to lure victim into requesting “http://localhost.target.com:1024/cutedogs.gif”.
    The response shown to victim, when he tries to visit above-mentioned URL is something like “Failed to load image”.
    In the background, however, request is logged.


# [EXPLOIT SAME SITE SCRIPTING HARD WAY>>>>=](https://seclists.org/bugtraq/2008/Jan/270)

