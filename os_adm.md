# Table of contents

- [main](#main)
- [package_management](#package_management)
- [conn_strings](#conn_strings)

# [main]
```bash
cat ./* |awk -F':' '{print $1}' |sort |uniq > /tmp/groupnames

for group in /tmp/groupnames; do \
	grep -e "^${group}:" ./ |awk -F':' '{print $NF}'| tr ',' '\n' |sort |uniq > /tmp/${group}

# use the `dd` utility to write an image.
dd if=/path/to/image.iso of=/dev/sdX bs=8M status=progress oflag=direct

find . -maxdepth 1 -type f -exec '{}' '+' |tr ' ' '\n'
# (find only files in current dir and replace ' ' '\n')

find . -name '.?*' -maxdepth 1 -user `whoami` -exec du -sh {} \; |egrep -i '(^[0-9].?.[K|M])'
# (find files in current directory starts with . having sizes in Kb and Mb, and print them to stdout)

#these're similiar commands:
find . -type f -exec echo {} + |tr ' ' '\n' |wc -l
find . -type f |xargs echo |tr ' ' '\n' |wc -l

find . -type d -empty #find empty directories

find . -type f -perm -0700 -print 2>/dev/null
# find files in current dir with permissions exaclty equal to 0700

find /home/ -type f -name '*.yml' |xargs grep -n 400 |\

grep -v 'gid:\|status_code:\|nrusca-clp\|port_range\|install\|inactive_interval\|avro\|kylo\|86400\|14000'
# find sertain files and grep them for something

chown/chmod --reference=file1 file2 # copy owner/permissions from file1 to file2

# look into last killed process by OOM
grep -i 'killed process' /var/log/messages
dmesg |grep -Ei 'killed process'

journalctl _COMM=sshd # check sshd logs

find /var/lib/jenkins/workspace -type d -mtime +7 -exec rm -rf '{}' \;
# find and delete directories older than 7 days

find . -maxdepth 1 \( -name ".forward" -o -name ".ssh" \) -print 2>/dev/null
#find several item in one command

find . ! -name . -prune -print | grep -c / # count files in a current dir

lsb_release -d | cat /etc/os-release | hostnamectl #check OS version

cat /proc/loadavg | uptime | w | top #different ways to check load avg

cat /proc/sys/kernel/random/entropy_avail # check the available entropy on a system

/var/lib/sdc-resources

ls -ltr |awk '{ print $9 }' |sed '/^[[:space:]]*$/d' # delete 1st empty line from output
ls -ltr |sed '1 d' |sed '$ d' |awk '{print $9}' # delete 1st and last lines from output

getfacl file1 | setfacl --set-file=- file2 #copy the ACL of file1 to file2

netstat -i #Show the state of interfaces which have been auto-configured
netstat -s #Show per-protocol statistics
netstat -nr #Show routing tables (-n show adresses as numbers)

sudo lsof -PiTCP -sTCP:LISTEN #show listen tcp ports  
netstat -ap tcp |grep -Ei "listen" #show listen tcp ports

du -sh * |grep -E "(^[0-9][^.].M|^[0-9].?.G)"

grep -iw -E "(ERROR)" `ls -lt |grep -i "Mar 11" |awk -F ' ' '{ print $9 }'` --color

pgrep -afil 'some_process_discription' # find a procces in process table

for i in `ls / |grep -Ev 'sys|proc|mnt|lib'`; do sudo find /$i -type f -name *semarchy*; done |grep war
#search in all catalogs except of systems dirs some file with name *semarchy*

strings (1)          # print the strings of printable characters in files
foremost (1)         # Recover files using their headers, footers, and data structures
exiftool (1)         # Read and write meta information in files

lsof #lists all open files can be used to check sockets ports etc.
lsof -i |egrep -i "(listen|established)" #list open network connections
nettop #web traffic info (macOS utility)
nmap -A -T4 <host> #this flags from man page (has a wide range of functionality)
netstat #show network status
nc -w3 -vz <host> <port> #check connection to the port
sudo nmap -Pn -O -T4 <host> #-Pn scan all ports -O try to guess os -T4 speed level(0-5)
uptime | iostat #another way to check loadavarage

top -u -s10
fs_usage -f filesys 
fs_usage -f network
vm_stat
diskutil list

brctl log #Manage the CloudDocs daemon
#launchd -- daemon/agent manager
launchctl #Interfaces with launchd

pmset # manipulate power management settings
echo $[2#00000010] # converting binary to decimal

systemctl list-unit-files --type=service --all
# displays the status of all installed services that have init scripts
# Enabled means it has a symlink in a .wants directory
# Disabled means it does not
# Static means the service is missing the [Install] section in its init script
# Static services are usually dependencies of other services

strace -f `command` 2>${file}
# (a great deal can be learned about a system and its system calls by tracing even ordinary  programs)

gdb
# (allow you to see what is going  on  ‘‘inside’’  another program)

tree / -L 1 --inodes #print catalog's tree with inodes and max depth 1

od          # dump files in octal and other formats
hexdump -C  # display file contents in ascii, decimal, hexadecimal, or octal + Canonical hex+ASCII display.
dd          # convert and copy a file
nc          # Concatenate and redirect sockets

df -Ph
lsblk
dzdo fdisk /dev/xvdh
dzdo pvcreate /dev/xvdh1
dzdo vgextend VolGroup00 /dev/xvdh1
dzdo lvextend -L +10G /dev/VolGroup00/LogVol07
dzdo resize2fs /dev/VolGroup00/LogVol07
#mount new volumes to the system
lvdisplay
vgdisplay
vgs
pvs
# usefull commands during mounting volumes

mtr    # combines the functionality of the traceroute and ping programs in a
       # single network diagnostic tool.

ldapsearch -D "login@domain.com" -W -h host.domain.com -b "DC=domain,DC=com" -s sub "(cn=<some_name>)"
# (search in domain <domain.com> with servers host.domain.com all that below DC=domain,DC=com in Directory Server tree)

ssh -L 80:intra.example.com:80 gw.example.com
# (This example opens a connection to the gw.example.com jump server,
# and forwards any connection to port 80 on the local machine to port 80
# on intra.example.com.)

tcpdump -D
tcpdump -r beeline.dump
tcpdump -vv port 10000 -tttt -w beeline.pcap
tcpdump port 10000 -tttt -vv -XX -w beeline.pcap # -XX for ACSII and HEX format output
tcpdump -i 1 -vv -nn -c 10 'host <host1> and <host2>' # capture traffic between 2 host

kinit username@DOMAIN.COM -k -t user.keytab

ktutil
addent -password -p username@MYDOMAIN.COM -k 1 -e RC4-HMAC
wkt username.keytab
q

jar tf <jarfile> #look into jarfile
jar xfv <jarfile> #extract jar artifact

rpm -qlp ~/mysql-connector-java-8.0.19-1.el7.noarch.rpm #list rpm pkg content
rpm -ivh mysql-connector-java-8.0.19-1.el7.noarch.rpm #install rpm pkg

ldapsearch -D "<ldapuser>@<domen>.com" -W -h <controller>.<domen>.com \
    -b "DC=<domen>,DC=com" -s sub "(userPrincipalName=<user_principal>@<domen>.com)"

yum --showduplicates list httpd
yum info
yum list installed

repoquery --show-duplicates mysql-community-server

pidof <process_name>
top -Hbn1 -p <process_id> #run top with batch mod with 1 iteration, and view threads information

ls -l /proc/<process_id>/task #is also shows process' thread

mysqldump –u [UserName] –p[Password] –R [DB_Name] > [DB_Name].sql
```

# [package_management]
```bash
repoquery --requires --resolve <pkg> # check pkg dependencies
rpm --install --test <pkg> # dont install just check pkg for deps conflicts
rpm -qa #list of all installed pkgs
rpm -q --info <pkg> #show info about installed pkgs
rpm -ql #list pkg files
rpm -q --requires <pkg> #list pkg deps
yum list installed #list installed pkgs
yum list available 
yum deplist --showduplicates
```

# [conn_strings]
```bash
!connect jdbc:hive2://hive.server2.url:10000/default;ssl=true;sslTrustStore=/opt/ssl/cacerts.jks;sslTrustStorePassword=changeit;
impala-shell -i impalad.server.net -l  --auth_creds_ok_in_clear --ssl -u <username>

beeline -u "jdbc:hive2://hive.server2.url:10000/default;ssl=true;sslTrustStore=/opt/ssl/cacerts.jks;sslTrustStorePassword=changeit"
-n <usr> -p <pwd> -f query.hql >>beeline.out

hdfs dfs -ls swebhdfs://some.namenode.url:14000/ # webhdfs url
hdfs dfs -ls hdfs://some.namenode.url:8020/      # hdfs url

# NordVPN CLI - login command
# if MFA is enabled
# `nordvpn login` - will generate a link which could be pasted to a browser window, in browser's login page copy `login` link
# and provide token part to the `nordvpn login --callback` command
nordvpn login
nordvpn login --callback nordvpn://login?action=login&exchange_token=<TOKEN_INFO_%3D%3D&status=done>
```
