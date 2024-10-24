# Failed to download metadata for repo ‘AppStream’ [CentOS]
### Updated on February 10, 2022
I had installed a minimalist CentOS 8 on one of my servers. Installation went successful, however, when I tried to update the system using yum update I see this error message: Failed to download metadata for repo. Below is the complete error.

    sudo yum update
----

CentOS-8 - AppStream 70 B/s | 38 B 00:00
Error: Failed to download metadata for repo 'AppStream': Cannot prepare internal mirrorlist: No URLs in mirrorlist
Output from the /var/log/dnf.log for more DEBUG information:

2022-02-02T11:39:36Z DEBUG error: Curl error (6): Couldn't resolve host name for http://mirrorlist.centos.org/?release=8&arch=x86_64&repo=AppStream&infra=stock [Could not resolve host: mirrorlist.centos.org] (http://mirrorlist.centos.org/?release=8&arch=x86_64&repo=AppStream&infra=stock).
2022-02-02T11:39:36Z WARNING Errors during downloading metadata for repository 'AppStream':

-Curl error (6): Couldn't resolve host name for http://mirrorlist.centos.org/?release=8&arch=x86_64&repo=AppStream&infra=stock [Could not resolve host: mirrorlist.centos.org]
2022-02-02T11:39:36Z DDEBUG Cleaning up.
2022-02-02T11:39:36Z SUBDEBUG
Traceback (most recent call last):
File "/usr/lib/python3.6/site-packages/dnf/repo.py", line 573, in load
ret = self._repo.load()
File "/usr/lib64/python3.6/site-packages/libdnf/repo.py", line 394, in load
return _repo.Repo_load(self)
RuntimeError: Failed to download metadata for repo 'AppStream': Cannot prepare internal mirrorlist: Curl error (6): Couldn't resolve host name for http://mirrorlist.centos.org/?release=8&arch=x86_64&repo=AppStream&infra=stock [Could not resolve host: mirrorlist.centos.org]
But, then verified with the internet connection and DNS and it works just fine as below:

    ping google.com

PING google.com (172.217.166.206) 56(84) bytes of data.
64 bytes from del03s13-in-f14.1e100.net (172.217.166.206): icmp_seq=1 ttl=115 ti me=43.5 ms
--- google.com ping statistics ---
1 packets transmitted, 1 received, 0% packet loss, time 0ms
rtt min/avg/max/mdev = 43.508/43.508/43.508/0.000 ms
So how did I fix the issue? Here it is.

---

## Fix Failed to download metadata for repo
CentOS Linux 8 had reached the End Of Life (EOL) on December 31st, 2021. It means that CentOS 8 will no longer receive development resources from the official CentOS project. After Dec 31st, 2021, if you need to update your CentOS, you need to change the mirrors to vault.centos.org where they will be archived permanently. Alternatively, you may want to upgrade to CentOS Stream.

#### Step 1: Go to the /etc/yum.repos.d/ directory.

    cd /etc/yum.repos.d/

#### Step 2: Run the below commands

    sudo sed -i 's/mirrorlist/#mirrorlist/g' /etc/yum.repos.d/CentOS-*  

-------

    sudo sed -i 's|#baseurl=http://mirror.centos.org|baseurl=http://vault.centos.org|g' /etc/yum.repos.d/CentOS-*


#### Step 3: Now run the yum update

    sudo yum update -y
That’s it!