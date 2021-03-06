<img align="right" width="100" height="100" src="/img/daemon.png">

#### Table of contents

1. [os_adm](#os_adm)
    - [package_management](#package_management)
    - [conn_strings](#conn_strings)
2. [virtualization](#virtualization)
3. [contenirization](#contenirization)
4. [ci/cd](#ci/cd)
    - [jenkinsci](#jenkinsci)
    - [ansible](#ansible)
5. [git](#git)
6. [aws](#aws)
7. [vim](#vim)
8. [not_categorized](#not_categorized)


#### [os_adm]
```bash
cat ./* |awk -F':' '{print $1}' |sort |uniq > /tmp/groupnames
for group in /tmp/groupnames; do grep -e "^${group}:" ./ |awk -F':' '{print $NF}'| tr ',' '\n' |sort |uniq > /tmp/${group}

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

find /var/lib/jenkins/workspace -type d -mtime +7 -exec rm -rf '{}' \;
# find and delete directories older than 7 days

find . -maxdepth 1 \( -name ".forward" -o -name ".ssh" \) -print 2>/dev/null
#find several item in one command

lsb_release -d | cat /etc/os-release | hostnamectl #check OS version

cat /proc/loadavg | uptime | w | top #different ways to check load avg

/var/lib/sdc-resources

ls -ltr| awk '{ print $9 }' |sed '/^[[:space:]]*$/d' # delete 1st empty line from output
ls -ltr |sed '1 d' |sed '$ d' |awk '{print $9}' # delete 1st and last lines from output

getfacl file1 | setfacl --set-file=- file2 #copy the ACL of file1 to file2

netstat -i #Show the state of interfaces which have been auto-configured
netstat -s #Show per-protocol statistics
netstat -nr #Show routing tables (-n show adresses as numbers)

sudo lsof -PiTCP -sTCP:LISTEN #show listen tcp ports  
netstat -ap tcp |egrep -i "listen" #show listen tcp ports

du -sh * |egrep "(^[0-9][^.].M|^[0-9].?.G)"

grep -iw -E "(ERROR)" `ls -lt |grep -i "Mar 11" |awk -F ' ' '{ print $9 }'` --color

pgrep -afil 'some_process_discription' # find a procces in process table
for i in `ls / |egrep -v 'sys|proc|mnt|lib'`; do sudo find /$i -type f -name *semarchy*; done |grep war
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

kinit username@DOMAIN.COM -k -t user.keytab

ktutil
addent -password -p username@MYDOMAIN.COM -k 1 -e RC4-HMAC
wkt username.keytab
q

jar tf <jarfile> #look into jarfile
jar xfv <jarfile> #extract jar artifact

rpm -qlp ~/mysql-connector-java-8.0.19-1.el7.noarch.rpm #list rpm pkg content
rpm -ivh mysql-connector-java-8.0.19-1.el7.noarch.rpm #install rpm pkg

gpg --full-generate-key
gpg --list-secret-keys --keyid-format LONG
gpg --armor --export <key_id>
gpg --armor --export <key_id> #export public part of gpg key in string format

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

##### [package_management]
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

##### [conn_strings]
```bash
!connect jdbc:hive2://hive.server2.url:10000/default;ssl=true;sslTrustStore=/opt/ssl/cacerts.jks;sslTrustStorePassword=changeit;
impala-shell -i impalad.server.net -l  --auth_creds_ok_in_clear --ssl -u <username>

beeline -u "jdbc:hive2://hive.server2.url:10000/default;ssl=true;sslTrustStore=/opt/ssl/cacerts.jks;sslTrustStorePassword=changeit"
-n <usr> -p <pwd> -f query.hql >>beeline.out

hdfs dfs -ls swebhdfs://some.namenode.url:14000/ # webhdfs url
hdfs dfs -ls hdfs://some.namenode.url:8020/      # hdfs url
```

#### [virtualization]
```bash
VBoxManage list vms                             # list existing virtualmachines;
VBoxManage unregistervm --delete "machine_name" # delete unused machine;
vagrant up                                      # create new environment along with Vagrantfile;
vagrant ssh                                     # login to running machine;
vagrant halt                                    # poweroff running machine;
vagrant destroy                                 # remove environment;
vagrant box list                                # lists all the boxes that are installed into Vagrant
```

#### [contenirization]
```bash
docker pull          # pull an image or a repository from a registry;

docker run --detach --publish 8080:8080 --volume jenkins_home:/var/jenkins_home --name jenkins jenkins/jenkins:lts

docker run           # run a command in a new container;
docker run --detach  # run container in background and print container id;
docker run --publish # publish a container's port(s) to the host;
docker run --volume  # bind mount a volume;
docker exec          # run a command in a running container;
```
#### [ci/cd]
##### [jenkinsci]
```bash
wget -q --auth-no-challenge --user USERNAME --password PASSWORD --output-document - \
'JENKINS_URL/crumbIssuer/api/xml?xpath=concat(//crumbRequestField,":",//crumb)'
# obtain Jenkins crumb in order to trigger jobs from cli;

curl -X POST \
     -H "Jenkins-Crumb:<CRUMB>" \
     localhost:8080/job/<job_name>/build?token=<TOKEN> \
     --user <usr>:<pwd>
# trigger simple Jenkins job from cli;
```

##### [ansible]
```bash
ansible -m debug -a 'var=hostvars[inventory_hostname]' <host_or_group>
# show ansible playbook variables for sertain host group

ansible -i inventory/prod all -m shell -a 'uname -n; df -Ph |egrep "(8|9)[0-9]%"'
# (#check disk space usage with trashhold >= 80%)

ansible-playbook <play>.yml --tags 'your_tag' --list-tasks
#list which tags are applied to tasks, roles, and static imports

ansible-playbook <play>.yml --list-tags
#display all tags available in specific play

ansible localhost -m debug -a var='var_name' -e "@file_with_thatvar"
# look into encrypted ansible strings

ansible-vault encrypt_string --vault-password-file a_password_file 'foobar' --name 'the_secret'
#encrypt ansible string
```

#### [git]
```bash
git log                      # show commits
git log --graph --decorate --pretty=oneline --abbrev-commit #more pretty log
git show <commit_id> --color # show commit detailed information
git log --follow -- <filename>  # show all commits related to certain file
git diff                     # see what exactly will change

#annotated tag
git tag -a v1.0 -m ‘Version 1.0’ <tagname>
git tag

git push origin --tags

git push --delete origin tagName - delete tag remotely
git tag -d tagName               - delete tag locally

#<tagname> - The object that the new tag will refer to,
#                usually a commit. Defaults to HEAD.

git push -o merge_request.create -o merge_request.target=branch_name
# create merge request with push option and choose target branch

git push --set-upstream origin feature/<some_branch_name>

git branch --set-upstream-to=origin/feature/<some_branch_name>
# setup to track remote branch 'feature/<some_branch_name>
git branch -vv
# check what which remote branch are tracking (connect local and remote branhces)

git commit --amend #do last commit again

git revert -n <bad_commit_number> #revert commit with needed changes
git commit <path/to/file/to/revert> -m 'reverted some file' #commit files that we want to change
git reset --hard Head #reset all changes to the last state

git branch --delete <branch_name> #delete branch localy
git push <remote_name(always: origin)> --delete <branch_name> #delete branch remotely

git reset --hard HEAD~1 #reset all changed to the commit previous HEAD

git config --global color.ui auto #color git output

git rev-list --count develop #count commits on certain branch

#delete all your commit history but keep the code in its current state
git checkout --orphan <tmp_branch> 
git add -A #add all the files
git commit -am "commit message"
git branch -D master
git branch -m master #rename the current branch to master
git push -f origin master #finally, force update your repository

#squashing commits into one
git rebase -i <commit_hash> #all commits above this hash up to HEAD will be merged into one
#in the pop-up editor window will be the commits list in !reverse-order!
#mark the old-one (at the top) as 'pick' and the rest of all commits as 'squash'
#save changes, make result final commit
git push --force #(--force-with-lease? in newer versions) to update upstream with local branch
#NOTE:  the pushed branch should only mirror your work, not be the authoritative branch,
#so 'force push' is acceptable.))
```

#### [aws]
```bash
aws --profile <profile_name> -ccdd --region us-west-2 ec2 describe-instance-status \
--filters Name=instance-state-name,Values=running
# describe aws running instances in specific region

aws codecommit list-repositories --region eu-central-1
# list code commit repos.

aws codecommit get-repository --repository-name MyDemoRepo --region eu-central-1
# get metadata about single repo.

aws lambda --region eu-central-1 list-functions
aws lambda create-function --function-name my-function \
--zip-file fileb://function.zip --handler index.handler --runtime python3.7 \
--role arn:aws:iam::12836736247:role/lambda-cli-role
# create lambda function

aws --region eu-central-1 lambda invoke --function-name test_lambda_invoke out \
--log-type Tail --query 'LogResult' --output text |base64 -e
#trigger lambda func

aws --profile stage s3api put-object --bucket <bucket_name> -np --key some/bucket/path/
# put empty object to s3 (folder in this case)

aws s3api list-object-versions --bucket <bucket_name> --prefix <bucket_path>
#returns metadata about all of the versions of objects in a bucket

aws --profile <profile_name> --region <aws_region> s3api put-bucket-policy \
    --bucket <bucket_name> --policy file://policy.json

aws s3api create-bucket --bucket <bucket_name> --region <aws_region> \
    --create-bucket-configuration LocationConstraint=us-west-2 --acl private
```

#### [vim]
```bash
# (:help key-notation)
# (:help map-special-chars)
# (:help mapping)
# (:help map-which-keys)
```

#### [not_categorized]
```bash
# Managing python virtualenv
python3 -m venv <env_name> #create virtual env dir
source <env_name>/bin/activate #activate virtual env
deactivate #deactivate current virtual env

#in order to install Python Packages from source:
#download package -> unpack it -> go to package directory
#-> run python3 setup.py install

conda create --prefix=test_env python=3.*
conda create --name=test_env python=3.*
```
