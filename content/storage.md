+++
date = "2016-12-26T10:25:35+01:00"
title = "Filesystems and storage"
categories = [ "general" ]
tags = [ "document" ]
+++
The master node provides the following filesystem to the cluster via NFS:

- <code>/home</code>
  - 1 Tb total
  - store only inputs/outputs, not large binary files!
  -  disk quotas will be activated soon
  -  periodic backup will be activated soon

- <code>/scratch</code>
  - 3 Tb total
  - you can store large binary/restart files
  - access to /scratch from the nodes is slow! use instead local scratch ares
  - no disk quotas but periodic file deletion
  - no backup

- <code>/mnt/neo-niobe</code>
  - external USB HD containing backups from old clusters

In addition, the compute nodes provide a local and fast scratch area under
<code>/local_scratch</code>. If your code perform a lot of I/O, please use
this one instead of <code>/scratch</code>.

