###install ansible###
apt-get install ansible

###clone project ansible###
git clone

###copy file ansible to /ect/ansible###
cp -r host /etc/ansible/
cp -r roles /etc/ansible/

###Run Ansible###
ansible-playbook install_package.yml -K
