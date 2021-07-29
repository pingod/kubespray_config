# kubespray_config

#### Usage

```bash
# Install dependencies from ``requirements.txt``
sudo pip3 install -r requirements.txt

# Copy ``inventory/sample`` as ``inventory/mycluster``
#cp -rfp inventory/sample inventory/mycluster

# Update Ansible inventory file with inventory builder
declare -a IPS=(10.10.1.3 10.10.1.4 10.10.1.5)
CONFIG_FILE=inventory/kubespray_config/pan_at_dc_bj/hosts.yml python3 contrib/inventory_builder/inventory.py ${IPS[@]}

# Review and change parameters under ``inventory/mycluster/group_vars``
cat inventory/kubespray_config/pan_at_dc_bj/group_vars/all/all.yml
cat inventory/kubespray_config/pan_at_dc_bj/group_vars/k8s_cluster/k8s-cluster.yml

# Deploy Kubespray with Ansible Playbook - run the playbook as root
# The option `--become` is required, as for example writing SSL keys in /etc/,
# installing packages and interacting with various systemd daemons.
# Without --become the playbook will fail to run!
#ansible-playbook -i inventory/kubespray_config/pan_at_dc_bj/hosts.yaml  --become --become-user=root cluster.yml
ansible-playbook -i inventory/kubespray_config/pan_at_dc_bj/hosts.yaml  -u root cluster.yml
```

