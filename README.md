# Role: Hashicorp Vault

<table style="border:0px; width:100%"><tr><td width=160px valign=top><img src="media/icon_vault.png" alt="Vault icon" width=128 height=128></td>
<td>
Ansible role for installation, configuration, usage, and management of HashiCorp Vault.<br>Vault is a tool for securely accessing secrets. A secret is anything that you want to tightly control access to, such as API keys, passwords, certificates, and more. Vault provides a unified interface to any secret while providing tight access control and recording a detailed audit log.<br><br>Official website: `https://www.vaultproject.io/`<br><br>
</td>
</tr></table>

Ansible role Vault : [Design](docs/DESIGN.md)  |  [Examples](examples)  |  [Test](molecule)  |  [Issues]()  |<br>
Latest version:

# Actions:

<table style="border:0px; width:100%">
<tr><th>Deployment</th><th>Secrets Management</th><th>Secret Engines</th><th>Policies</th><th>AppRoles</th><th>Administration</th></tr>
<tr>
<td valign=top>install<br>uninstall<br>update<br></td>
<td valign=top>create_secret<br>destroy_secret<br>get_secret<br>import_secret<br>export_secret<br></td>
<td valign=top>create_secret_engine<br>destroy_secret_engine<br></td>
<td valign=top>create_policy<br>destroy_policy<br></td>
<td valign=top>create_approle<br>destroy_approley<br></td>
<td valign=top>configure<br>start<br>stop<br>unseal<br></td>
</tr></table>

## Deployment

action: **install**<br>
Installation of the latest version of HashiCorp Vault.<br>
variables:<br>
<kbd>vault_repository_url</kbd> : URL with the location of the container repository. Can be a URL or path to a local or remote file, for example, 'docker.io/hashicorp/vault', '/tmp/vault.tar', 'https://192.168.1.1/repo/vault1.14.tar'. By default, it points to docker.io/hashicorp/vault via defaults/main.yml.<br>
<kbd>vault_repository_tag (optional)</kbd> : Release or version number of the image. Default is 'latest'.<br>
<kbd>vault_repository_checksum (optional)</kbd> : Checksum of the container image. Example: "sha256:1234567890abcdef1234567890abcdef1234567890abcdef1234567890abcdef" or "1234567890abcdef1234567890abcdef1234567890abcdef1234567890abcdef".<br>
<kbd>vault_repository_checksum_algorithm (optional)</kbd> : Algorithm for the checksum, for example, sha256, sha512, md5, etc.<br>
<kbd>platform (optional)</kbd>  : Install on a specific platform, for example, podman, kubernetes, host. Default is autodetect. (podman, kubernetes, host)<br>
<kbd>uninstall (optional)</kbd> : true/false. When true, uninstall is started before installation.<br>

```
- name: Install HashiCorp Vault
    hosts: vault-server
    roles:
     - role: vault
         vars:
             action: install
             vault_repository_url: docker.io/hashicorp/vault

```

action: **uninstall**<br>
Uninstallation of HashiCorp Vault.<br>
variables:<br>
<kbd>keep_data (optional)</kbd> : true/false. When true, data folders are kept during uninstall. Default is false.<br>

```
- name: Uninstall HashiCorp Vault
    hosts: vault-server
    roles:
     - role: vault
         vars:
             action: uninstall
```

action: **update**<br>
Update to the latest HashiCorp Vault version.<br>
variables:<br>
<kbd>(none)</kbd> : No variables required.<br>

```
- name: Update HashiCorp Vault
    hosts: vault-server
    roles:
     - role: vault
         vars:
             action: update
```


## Secrets Management

action: **create_secret**<br>
Create a secret in Vault.<br>
variables:<br>
<kbd>vault_address</kbd> : URL to the Vault address, e.g., `http://localhost:8200`.<br>
<kbd>vault_token</kbd> : Token for Vault access.<br>

```
- name: Create secret in Vault
    hosts: vault-server
    roles:
     - role: vault
         vars:
             action: create_secret
             vault_address: http://localhost:8200
             vault_token: s.1234567890abcdef

```

action: **destroy_secret**<br>
Delete a secret from Vault.<br>
variables:<br>
<kbd>vault_address</kbd> : URL to the Vault address, e.g., `http://localhost:8200`.<br>
<kbd>vault_token</kbd> : Token for Vault access.<br>
<kbd>secret_path</kbd> : Path where the secret is stored.<br>

```
- name: Delete secret from Vault
    hosts: vault-server
    roles:
     - role: vault
         vars:
             action: delete_secret
             vault_address: http://localhost:8200
             vault_token: s.1234567890abcdef
             secret_path: secret/myapp
```

## Policies

action: **create_policy**<br>
Create a policy in Vault.<br>
variables:<br>
<kbd>vault_address</kbd> : URL to the Vault address, e.g., `http://localhost:8200`.<br>
<kbd>vault_token</kbd> : Token for Vault access.<br>
<kbd>policy_name</kbd> : Name of the policy.<br>
<kbd>policy_rules</kbd> : Rules of the policy.<br>

```
- name: Create policy in Vault
    hosts: vault-server
    roles:
     - role: vault
         vars:
             action: create_policy
             vault_address: http://localhost:8200
             vault_token: s.1234567890abcdef
             policy_name: my-policy
             policy_rules: |
                 path "secret/*" {
                     capabilities = ["create", "read", "update", "delete", "list"]
                 }
```

action: **delete_policy**<br>
Delete a policy from Vault.<br>
variables:<br>
<kbd>vault_address</kbd> : URL to the Vault address, e.g., `http://localhost:8200`.<br>
<kbd>vault_token</kbd> : Token for Vault access.<br>
<kbd>policy_name</kbd> : Name of the policy.<br>

```
- name: Delete policy from Vault
    hosts: vault-server
    roles:
     - role: vault
         vars:
             action: delete_policy
             vault_address: http://localhost:8200
             vault_token: s.1234567890abcdef
             policy_name: my-policy
```

## Audit

action: **enable_audit**<br>
Enable audit logging in Vault.<br>
variables:<br>
<kbd>vault_address</kbd> : URL to the Vault address, e.g., `http://localhost:8200`.<br>
<kbd>vault_token</kbd> : Token for Vault access.<br>
<kbd>audit_path</kbd> : Path where the audit logs will be stored.<br>

```
- name: Enable audit logging in Vault
    hosts: vault-server
    roles:
     - role: vault
         vars:
             action: enable_audit
             vault_address: http://localhost:8200
             vault_token: s.1234567890abcdef
             audit_path: file
```

action: **disable_audit**<br>
Disable audit logging in Vault.<br>
variables:<br>
<kbd>vault_address</kbd> : URL to the Vault address, e.g., `http://localhost:8200`.<br>
<kbd>vault_token</kbd> : Token for Vault access.<br>
<kbd>audit_path</kbd> : Path where the audit logs are stored.<br>

```
- name: Disable audit logging in Vault
    hosts: vault-server
    roles:
     - role: vault
         vars:
             action: disable_audit
             vault_address: http://localhost:8200
             vault_token: s.1234567890abcdef
             audit_path: file
```

## Administration

action: **start**<br>
Start of HashiCorp Vault service.<br>
variables:<br>
<kbd>(none)</kbd> : No variables required.<br>

```
- name: Start HashiCorp Vault service
    hosts: vault-server
    roles:
     - role: vault
         vars:
             action: start
```

action: **stop**<br>
Stop of HashiCorp Vault service.<br>
variables:<br>
<kbd>(none)</kbd> : No variables required.<br>

```
- name: Stop HashiCorp Vault service
    hosts: vault-server
    roles:
     - role: vault
         vars:
             action: stop
```

action: **unseal**<br>
Unseal Vault to make it ready for use.<br>
variables:<br>
<kbd>vault_address</kbd> : URL to Vault, for example, `https://192.168.1.0:8200`.<br>
<kbd>vault_unseal_keys</kbd> : Unseal keys of Vault. These are the keys generated during installation.<br>



***

- **changelog**<br>
    Change log.
    See [changelog](CHANGELOG.md)<br>

- **roadmap**<br>
    Vision and future developments.
    See [roadmap](ROADMAP.md)<br>

***

## Preparations
(none).<br>

## Dependencies
Dependencies are listed in the **requirements.yml** file. Use `ansible-galaxy install -r requirements.yml --force` for installation.<br>
If this role is used in other playbooks or Ansible projects, the URL of this role must be added to the `requirements.yml` file. Using the above command, the role will be placed in the correct folder structure.<br>
<br>

## Installation
Installation Vault via action 'install'.<br>
Example for installing Vault:

```
- name: Install Vault
    hosts: vault-server
    tasks:
        - name: Install HashiCorp Vault
            ansible.builtin.include_role:
                name: vault
                vars:
                    action: install
                    vault_version: latest
                    vault_binary_url: "https://releases.hashicorp.com/vault/latest/vault_latest_linux_amd64.zip"
```

## Configuration
(none).<br>

## Other information

**Global variables**

# Create list of all variables used in /vars/main.yml

| Variable                             | Description                                                                 |
|--------------------------------------|-----------------------------------------------------------------------------|
| vault_version                        | Version of Vault to install.                                                |
| vault_binary_url                     | URL to download the Vault binary.                                           |
| vault_checksum                       | Checksum of the Vault binary.                                               |
| vault_checksum_algorithm             | Algorithm for the checksum, e.g., sha256.                                   |
| platform                             | Install on a specific platform, e.g., podman, kubernetes, host.             |
| uninstall                            | When true, uninstall is started before installation.                        |
| vault_address                        | URL to the Vault address for Vault access.                                  |
| vault_token                          | Token for Vault access.                                                     |
| secret_path                          | Path where the secret will be stored.                                       |
| secret_data                          | Data of the secret in key-value pairs.                                      |
| policy_name                          | Name of the policy.                                                         |
| policy_rules                         | Rules of the policy.                                                        |
| audit_path                           | Path where the audit logs will be stored.                                   |
|--------------------------------------|-----------------------------------------------------------------------------|

## License
MIT

## Author
Marcel Venema
