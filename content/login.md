+++
date = "2016-12-26T10:25:35+01:00"
title = "Login"
categories = [ "general" ]
tags = [ "document" ]
+++
Morpheus is generally accessible only from **within** the CNR-ISTM network. If you
are not connected to the CNR-ISTM network, you must first activate the VPN.

#### From Linux/Unix/OSX:
``` bash
ssh -X username@istm245.istm.loc
or
ssh -X username@192.168.3.245
```
It is also possible to connect using <code>mosh</code>, the [mobile shell](https://mosh.org/)

#### From Windows
Please, use [PuTTY](http://www.putty.org/) or [MobaXTerm](http://mobaxterm.mobatek.net/).
Other clients (i.e. WinSSH) are not supported. Depending on how your machine is resolving
IP addresses, conntect to <code>istm245</code>, <code>istm245.istm.loc</code> or <code>192.168.3.245</code>.


#### From outside the CNR-ISTM network (experimental)
*ssh* to <code>vps282498.ovh.net</code> on port <code>2222</code>. E.g.:
```bash
ssh -p2222 username@vps282498.ovh.net
```
If not responding, contact D. Ceresoli.

