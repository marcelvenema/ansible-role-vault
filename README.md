# role: Hashicorp Vault

<table border="0">
  <tr>
    <td width="160px" valign="top"><img src="media/icon_vault.png" align="left" height="128" width="128" /></td>
    <td>Ansible role for installation, configuration, usage, and management of Hashicorp Vault.<br/>
        Depending on the infrastructure, it can be installed as a Podman pod (docker container), Kubernetes container, or directly on the operating system.<br/>
        Currently, only installation and configuration as a Podman pod are available.<br/>
        <br/>
        Vendor website: `https://vaultproject.io`<br/>
        <br/>
    </td>
  </tr>
</table>

[Design Ansible role Vault](docs/DESIGN.md)<br/>

# Actions:

action: **install**<br/>
Installation of the latest version of Hashicorp Vault. Basic configuration.<br/>
variables:<br/>
<kbd>vault_repository_url</kbd> : URL with the location of the container repository. Can be a URL or path to a local or remote file, for example, 'docker.io/hashicorp/vault', '/tmp/vault.tar', 'https://192.168.1.1/repo/vault1.14.tar'. By default, it points to docker.io/hashicorp/vault via defaults/main.yml.<br/>
<kbd>vault_repository_tag (optional)</kbd> : Release or version number of the image. Default is 'latest'.<br/>
<kbd>vault_repository_checksum (optional)</kbd> : Checksum of the container image. Example: "sha256:1234567890abcdef1234567890abcdef1234567890abcdef1234567890abcdef" or "1234567890abcdef1234567890abcdef1234567890abcdef1234567890abcdef".<br/>
<kbd>vault_repository_checksum_algorithm (optional)</kbd> : Algorithm for the checksum, for example, sha256, sha512, md5, etc.<br/>
<kbd>platform (optional)</kbd>  : Install on a specific platform, for example, podman, kubernetes, host. Default is autodetect. (podman, kubernetes, host)<br/>
<kbd>uninstall (optional)</kbd> : true/false. When true, uninstall is started before installation.<br/>


action: **uninstall**<br/>
Uninstallation of Hashicorp Vault.<br/>
variables:<br/>
<kbd>keep_data (optional)</kbd> : true/false. When true, data folders are preserved during uninstall. Default is false.<br/>


action: **update**<br/>
Update Hashicorp Vault to the latest version. (backlog).<br/>
variables:<br/>
<kbd>vault_repository_url</kbd> : URL with the location of the container repository. Can be a URL or path to a local or remote file, for example, 'docker.io/hashicorp/vault', '/tmp/vault.tar', 'https://192.168.1.1/repo/vault1.14.tar'. By default, it points to docker.io/hashicorp/vault via defaults/main.yml.<br/>
<kbd>vault_repository_tag (optional)</kbd> : Release or version number of the image. Default is 'latest'.<br/>
<kbd>vault_repository_checksum (optional)</kbd> : Checksum of the container image. Example: "sha256:1234567890abcdef1234567890abcdef1234567890abcdef1234567890abcdef" or "1234567890abcdef1234567890abcdef1234567890abcdef1234567890abcdef".<br/>
<kbd>vault_repository_checksum_algorithm (optional)</kbd> : Algorithm for the checksum, for example, sha256, sha512, md5, etc.<br/>
<kbd>platform (optional)</kbd>  : Install on a specific platform, for example, podman, kubernetes, host. Default is autodetect. (podman, kubernetes, host)<br/>


action: **start**<br/>
Start of Hashicorp Vault service. (backlog).<br/>
variables:<br/>
<kbd>(none)</kbd> : No variables required.<br/>


action: **stop**<br/>
Stop of Hashicorp Vault service. (backlog).<br/>
variables:<br/>
<kbd>(none)</kbd> : No variables required.<br/>


action: **unseal**<br/>
Unseal Vault to make it ready for use.<br/>
variables:<br/>
<kbd>vault_address</kbd> : URL to Vault, for example, `https://192.168.1.0:8200`.<br/>
<kbd>vault_unseal_keys</kbd> : Unseal keys of Vault. These are the keys generated during installation.<br/>


When the variable action is not filled in, it is detected whether Nexus Repository OSS is already installed. If not, the action value is set to **install**. If yes, the action value is set to **start**.<br/>


Example:
```
---
- hosts: lab_server
  vars:
  roles:
    - role: vault
      vars:
        action        : install
        vault_repository_url: "\tmp\vault.tar"

```

## Secret Engines

action: **create_secret_engine**<br/>
To be filled in.<br/>
variables:<br/>
<kbd>vault_address</kbd> : URL to vault address for vault access, for example, `http://localhost:8081`<br/>
<kbd>vault_token</kbd> : Token for access to vault.<br/>
<kbd>vault_name</kbd> : Name of the secret engine.<br/>
<kbd>vault_description</kbd> : Description of the secret engine.<br/>
<kbd>vault_type</kbd> : Secret engine type, for example, `kv`, `pki`.<br/>


action: **destroy_secret_engine**<br/>
To be filled in.<br/>
variables:<br/>
<kbd>(none)</kbd> : No variables required.<br/>


action: **get_secret**<br/>
To be filled in.<br/>
variables:<br/>
<kbd>(none)</kbd> : No variables required.<br/>


action: **create_secret**<br/>
To be filled in.<br/>
variables:<br/>
<kbd>(none)</kbd> : No variables required.<br/>


action: **destroy_secret**<br/>
To be filled in.<br/>
variables:<br/>
<kbd>(none)</kbd> : No variables required.<br/>


action: **import_secrets**<br/>
To be filled in.<br/>
variables:<br/>
<kbd>(none)</kbd> : No variables required.<br/>


action: **export_secrets**<br/>
Export secrets from Vault to a file.<br/>
variables:<br/>
<kbd>vault_address</kbd> : URL to Vault, for example, `https://192.168.1.0:8200`.<br/>
<kbd>vault_token</kbd> : Token for access to Vault.<br/>
<kbd>vault_name</kbd> : Name of the vault (secret_engine) to export secrets from.<br/>
<kbd>secret_name</kbd> : Secret name.<br/>
<kbd>file_name</kbd> : Filename for export secrets.<br/>


Example:
```

# Export Vault secret to json file
- name: Export secrets from Vault
  hosts: localhost
  roles:
   - role: vault
     vars:
      action        : export_secrets
      vault_address : "http://192.168.29.20:8200"
      vault_token   : "hvs.9MGoUtPEGZWRgLX3dxZYkqxV"
      vault_name    : "os_template_factory"
      secret_name   : "windowsserver2022"
      filename      : "secrets_windowsserver2022.json"

```

***

- **changelog**<br/>
  Change log.<br/>
  See [changelog](CHANGELOG.md)<br/>


- **roadmap**<br/>
  Vision and future developments.<br/>
  See [roadmap](ROADMAP.md)<br/>


***

## Preparations
(none).<br/>


## Dependencies
Dependencies are listed in the **requirements.yml** file. Use `ansible-galaxy install -r requirements.yml --force` for installation.<br/>

If this role is used in other playbooks or Ansible projects, the URL of this role must be added to the `requirements.yml` file. Using the above command, the role will be placed in the correct folder structure.<br/>
<br/>

## Installation
Installation via action 'install'.<br/>
Example for installing Hashicorp Vault:

```
---
- hosts: localhost
  vars:
  roles:
    - role: vault
      vars:
        action        : install
        vault_repository_url: "\tmp\vault.tar"

```


## Configuration
(none).<br/>


## Other information
(none).<br/>


## License
MIT


## Author
Marcel Venema
