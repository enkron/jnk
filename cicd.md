# Table of contents

- [jenkinsci](#jenkinsci)
- [ansible](#ansible)

# [jenkinsci]
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

# [ansible]
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
