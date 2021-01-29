# Realliance Server Config

## Installation

1. Boot into Flatcar Linux ISO

2. Install Flatcar Linux

```shell
wget https://raw.githubusercontent.com/realliance/server-config/main/ignition.json
flatcar-install -d /dev/<disk> -i ignition.json
```

3. Reboot

4. (Optional) Setup python virtual environment

```shell
python3 -m venv ~/path/to/venv
source ~/path/to/venv/bin/activate
```

5. Install requirements
```shell
pip3 install -r kubespray/requirements.txt
```

6. (Optional) Install and setup mitogen

```shell
ansible-playbook kubespray/mitogen.yml
```

7. Run kubespray

```shell
ansible-playbook -i kubespray-inventory/hosts.yaml --become --become-user=root kubespray/cluster.yml
```

8. Install flux from [k8s-config](https://github.com/realliance/k8s-config)

```shell
kubectl apply -k k8s-config/cluster/flux-system
```
