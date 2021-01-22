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

5. (Optional) Install and setup mitogen

```shell
ansible-playbook kubespray/mitogen.yml
```

5. Run kubespray

```shell
pip3 install -r kubespray/requirements.txt
ansible-playbook -i kubespray-inventory/hosts.yaml --become --become-user=root kubespray/cluster.yml
```
6. Install flux (requires `flux` tool, `flux-bin` on AUR)

```shell
export GITHUB_USER=realliance-cd
export GITHUB_TOKEN=<token>
flux bootstrap github --owner=realliance --repository=k8s-config --branch=main --team infrastructure --private=false
```
