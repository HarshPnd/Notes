# Command Quick Reference

A concise guide to essential commands and their outputs.


    firefox
- Opens Firefox web browser.
---



    which firefox
- Locates Firefox installation.
---




    gedit filename    
- Opens the specified file in the Gedit editor.
---



    date    
- Displays the current date and time.
---


    cal    
- Shows a textual calendar for the current month.
---



    espeak-ng hello    
- Speaks "hello" through the speakers.
---


    free -m    
- list the available and total RAM info.
---


    lscpu    
- list the CPU info.
---



    ifconfig    
- list the network cards and IP address.
---




    systemctl start firewalld    
- starts the firewall services.
---

    systemctl status firewalld    
- shows the status of firewall services.
---



    systemctl stop firewalld    
- stops the firewall services.
---



    systemctl enable firewalld    
- enables the firewall service to start automatically at the time of os startup.
---


    systemctl disable firewalld    
- disables the firewall service so that it does not start automatically at the time of os startup.
---


    yum remove docker-ce    
- uninstalls the docker-ce software from the os.
---



    cat filename.txt    
- read and print the contents of the file filename.txt.
---



    ping goo.gl    
- check connectivity to goo.gl by transferring packets to the site.
---


    history    
- display the list of previously used commands.
---

    !(history command no.)
    !71   
- reuse the previously used command which is indexed at the mentioned number in history. e.g.- **!71** will run the command at **number 71 in history**.
---



    touch file1    
- creates a new file.
---

    touch file{1..10}.txt    
- create 10 files with names as file1.txt, file2.txt and so on.
---

    rm filename.txt    
- delete the file with the name filename.txt.
---



    rpm -q docker-ce    
- lists the installed docker-ce version.
---


    rpm -q -f /usr/bin/date    
- lists the installed version of the package that contains the mentioned file. Here `-f` is used to tell the rpm command that we are giving you a file's location.
---




    watch -n 1 free -m    
- keeps on running the command `free -m` every 1 second and updates the output.
---



    ls    
- display a list of all the files and directoriees available in the present directory.
---



    pwd    
- display the present working directory.
---

## Set up local dns

    hostname    
- display the hostname.
---

    hostnamectl    
- display the detailed info about hostname.
---

    vi /etc/hosts    
- modify the above file to set up local dns. Use the below mentioned format - 

        192.168.x.x   node1.localdomain
- save and exit using **Esc** followed by **:wq**

        ping node1.localdomain
- You can test the DNS resolution by pinging the hostname
---

## Allow firewall for Apache Server

    sudo firewall-cmd --permanent --add-port=80/tcp
    sudo firewall-cmd --reload
    
- adds the firewall rule to open port 80.
---

    sudo firewall-cmd --list-all    
- display the list of configured Firewall rules.
---