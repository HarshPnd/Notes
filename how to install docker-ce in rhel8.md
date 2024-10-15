How to install docker-ce in rhel8


Generally: 

        curl -sSL https://get.docker.com | sh
- is used to install docker.
---
but it fails saying that rhel8 supports only docker-ee version so in order to install docker-ce in rhel 8 the following steps are used.

- Step 1: Search for rpm install docker on google
- Step 2: Copy the link of the repository containg docker packages and use it to configure a repo just like yum was configured.
- Step 3: move to /etc/yum.repos.d using.

        cd /etc/yum.repos.d

- Step 4: create a new file with any name with `.repo` as the extension.

        gedit docker.repo

- Step 5: Paste the link in the following format

        [docker]  
        baseurl= *__link of the docker repo__*  
        gpgcheck=0   

- Step 6: Use the following command to install docker-ce

        yum install docker-ce --nobest

here `--nobest` is used to install the most compatible version of docker if the exact match of the version is not available