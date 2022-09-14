# Validated Pattern Utility Container 

utility container for simplified execution of imperative commands in each of the patterns.

This container is built as an Ansible Execution Environment, which is usable as such.

The tag used on the image represents the `oc` client version installed. <br/>
For example: `quay.io/hybrid-cloud-patterns/utility-container:stable-4.10.3` means that the openshift client (oc) version is `4.10.3`

```bash
$ podman run quay.io/hybrid-cloud-patterns/utility-container:stable-4.10.3` oc version 
Client Version: 4.10.3
```

The image is based on UBI, and adds some RHEL content, installs some additional binaries, and adds some pip modules to support various functions for the utility container. More dependencies may be added later.

### Installed Software

|    name     |  type   |
|:-----------:|:-------:|
|    make     | package |
|    git      | package |
|    make     | package |
|    gawk     | package |
|     jq      | package |
|   argocd    | binary  |
|    tkn      | binary  |
|     yq      | binary  |
|  kustomize  | binary  |
|    helm     | binary  |
| jmespath    |   pip   |
| kubernetes  |   pip   |
|  openshift  |   pip   |
|    boto3    |   pip   |
|  botocore   |   pip   |
|   awscli    |   pip   |
|  azure-cli  |   pip   |
|   gcloud    |   pip   |


### The ansible-galaxy collection installed:
| ansible-collections |
| ------------------- |
| ansible.posix |
| oasis_roles.system |
| fedora.linux_system_roles |
| community.general |
| containers.podman |
| community.okd |
| awx.awx |
| kubernetes.core |
| redhat_cop.controller_configuration |

### Usage
**Pull the image**
```bash
podman pull quay.io/hybrid-cloud-patterns/utility-container:stable-4.10.3
```

**Use image to execute a playbook**
```bash
podman run quay.io/hybrid-cloud-patterns:stable-4.10.3 ansible-playbook <playbook>.yml 
```

**Use the image to mimic the user's home directory for managing patterns
```bash
podman run -it \
    --security-opt label=disable \
    -e KUBECONFIG="${KUBECONFIG}" \
    -v ${HOME}:/home/runner \
    -v ${HOME}:${HOME} \
    -v ${HOME}:/root \
    -w $(pwd) \
    quay.io/hybrid-cloud-patterns/utility-container:stable-4.10.3 \
    make install
```
