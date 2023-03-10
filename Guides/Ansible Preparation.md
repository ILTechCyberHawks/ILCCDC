- need Ansible SSH keypair on Windows 10
  - transfer [ssh-keypair.sh](../Scripts/ssh-keypair.sh) onto WSL
  - `chmod +x ssh-keypair.sh`
  - `./ssh-keypair.sh`
  - DO NOT SET A PASSWORD -> just press enter
    - if you accidentally set a password, enter the following:
```
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/ansible_id_rsa
```
- no SSH server on Ubuntu workstation and mirrors too old to use
  - `sudo sed -i -re 's/([a-z]{2}\.)?archive.ubuntu.com|security.ubuntu.com/old-releases.ubuntu.com/g' /etc/apt/sources.list`
  - might have to fix DNS - then try `ping google.com`
  - `sudo apt-get update`
  - `sudo apt-get install -y openssh-server python --upgrade`
- Python on Splunk outdated and mirrors too old to use
- Python 3 on Fedora21 outdated and mirrors contain only outdated versions
  - `yum install zlib-devel`
  - `wget https://www.python.org/ftp/python/3.5.8/Python-3.5.8.tgz`
  - `tar -xf Python-3.5.8.tgz`
  - `cd Python-3.5.8`
  - `./configure --enable-optimizations`
  - `make altinstall`
  - run with `python3.5` (not necessary to do - just a note)
  - optional: `ln -s /usr/local/bin/python3.5 /usr/bin/python3`
- Windows 2016 firewall is blocking access from external subnets
  - either update Windows Firewall rule (not recommended) or do the following:
  - in Palo Alto GUI: POLICIES -> NAT -> source zone: external, destination zone: internal, source address: 172.31.24.5, static-ip 172.20.240.3, bi-directional: yes -> Commit
  - if you followed the competition day checklist, you shouldn't have to do this
- Windows 2012 (AD/DHCP/DNS) results in StackOverflowException
  - download https://s3.amazonaws.com/ansible-ci-files/hotfixes/KB2842230/463941_intl_x64_zip.exe
  - run it to extract the needed hotfix exe
  - run the extracted hotfix exe
- WinRM not installed on Windows 10
  - `winrm quickconfig`
