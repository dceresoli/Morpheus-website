+++
date = "2016-12-26T10:25:35+01:00"
title = "Adding a new user"
categories = [ "admin" ]
tags = [ "document" ]
+++
The script <code>crea_utente.sh</code> performs the following operations:
```
$ adduser username      # (not useradd)
$ make -C /var/yp
$ U=username 
$ mkdir /scratch/$U
$ chown $U.$U /scratch/$U
$ drbl-doit mkdir /local_scratch/$U
$ drbl-doit chown $U.$U /local_scratch/$U
$ addgroup $U gaussian
```
