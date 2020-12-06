# Blocked servers
This endpoint lists SHA1 hashes of all of the server IPs & domains that Mojang blocks.

The following description is from [wiki.vg](https://wiki.vg/Mojang_API):

Clients check the lowercase name, using the ISO-8859-1 charset, against this list. They will also attempt to check subdomains, replacing each level with a `*`. Specifically, it splits based off of the `.` in the domain, goes through each section removing one at a time. For instance, for `mc.example.com`, it would try `mc.example.com`, `*.example.com`, and `*.com`. With IP addresses (verified by having 4 split sections, with each section being a valid integer between 0 and 255, inclusive) substitution starts from the end, so for `192.168.0.1`, it would try `192.168.0.1`, `192.168.0.*`, `192.168.*`, and `192.*`.

This check is done by the bootstrap class in netty. The default netty class is overridden by one in the com.mojang:netty dependency loaded by the launcher. This allows it to affect any version that used netty (1.7+).

### Request
- **Method:** `GET`
- **Endpoint:** `/blockedservers`
- **Full URL:** `https://sessionserver.mojang.com/blockedservers`

### Response
Line-separated list of all the SHA1 hashes of domains / IP addresses that Mojang blocks.

Some hashes have been cracked. If you wish to attempt cracking these hashes, feel free to try using `hashcat`.

Sample response (first 10 lines):

```
72fd29f430c91c583bb7216fe673191dc25a7e18
e38e82a54b47c7c5394670bb34b3aa941219959b
d1bab7fcb1d44a0ad1084fb201006d79d05ae6e7
1822a17662c7e0cf3b815c257d32c2aa0245fad0
7905e1eeee5d57268bb9cbea2e0acbb5421a667b
56c7a4ccff309d6eb3c5737fe9509c3555e7f5fa
cf2f874a649da0118f717f7edb1f5fffcbae8c6b
c800614f07e155ca842e23f84c6a553973ccdb1f
dcc63fadc759ee712cdd5b7bade3bb3eff804637
96ea6aaf66aea5881b38ebbf66df686e8613f1db
```
