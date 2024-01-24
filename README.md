# Hashicorp Vault

<table border="0">
  <tr>
    <td width="160px" valign="top"><img src="media/icon_vault.png" align="left" height="128" width="128" /></td>
    <td>Ansible role voor installatie, configuratie, gebruik en beheer van Hashicorp Vault.<br/>
        Afhankelijk van de infrastructuur wordt deze als Podman pod (docker container), kubernetes container of direct op het besturingssysteem geinstalleerd.<br/>
        Vooralsnog is alleen installatie en configuratie als Podman pod beschikbaar.<br/>
        <br/>
        Website leverancier: `https://vaultproject.io`<br/>
        <br/>
    </td>
  </tr>
</table>

# Diensten:


action: **install**<br/>
Installatie van laatste versie van Hashicorp Vault. Basis configuratie.<br/>
variables:<br/>
<kbd>repository_url</kbd> : URL met locatie van container repository. Kan een url zijn of pad naar lokaal bestand.<br/>
<kbd>repository_tag (optioneel)</kbd> : Release of versienummer van het image. Standaard is 'latest'.<br/>
<kbd>platform (optioneel)</kbd> : installeer op specifiek platform, bijvoorbeeld podman, kubernetes, linux. Standaard is autodetect.<br/>
<kbd>uninstall (optioneel)</kbd> : true/false. Wanneer, true wordt voor installatie eerst uninstall gestart.<br/>


action: **uninstall**<br/>
De-installatie van Hashicorp Vault.<br/>
variables:<br/>
<kbd>(geen)</kbd> : Geen variabelen benodigd.<br/>


action: **update**<br/>
Update Hashicorp Vault naar de laatste versie. (backlog).<br/>
variables:<br/>
<kbd>repository_url</kbd> : URL met locatie van container repository. Kan een url zijn of pad naar lokaal bestand.<br/>
<kbd>repository_tag (optioneel)</kbd> : Release of versienummer van het image. Standaard is 'latest'.<br/>
<kbd>platform (optioneel)</kbd> : installeer op specifiek platform, bijvoorbeeld podman, kubernetes, linux. Standaard is autodetect.<br/>


action: **unseal**<br/>
Unseal Vault zodat deze gereed is voor gebruik.<br/>
variables:<br/>
<kbd>vault_address</kbd> : URL naar Vault, bijvoorbeeld `https://192.168.1.0:8200`.<br/>
<kbd>vault_unseal_keys</kbd> : Unseal keys van Vault. Dit zijn de keys die zijn gegenereerd tijdens de installatie.<br/>


action: **create_secret_engine**<br/>
Nader in te vullen.<br/>
variables:<br/>
<kbd>vault_address</kbd> : url naar vault adres voor toegang vault, bijvoorbeeld `http://localhost:8081`<br/>
<kbd>vault_token</kbd> : token voor toegang tot vault.<br/>
<kbd>vault_name</kbd> : naam secret engine.<br/>
<kbd>vault_description</kbd> : omschrijving van secret engine.<br/>
<kbd>vault_type</kbd> : secret engine type, bijvoorbeeld `kv`, `pki`.<br/>


action: **destroy_secret_engine**<br/>
Nader in te vullen.<br/>
variables:<br/>
<kbd>(geen)</kbd> : Geen variabelen benodigd.<br/>


action: **get_secret**<br/>
Nader in te vullen.<br/>
variables:<br/>
<kbd>(geen)</kbd> : Geen variabelen benodigd.<br/>


action: **create_secret**<br/>
Nader in te vullen.<br/>
variables:<br/>
<kbd>(geen)</kbd> : Geen variabelen benodigd.<br/>


action: **destroy_secret**<br/>
Nader in te vullen.<br/>
variables:<br/>
<kbd>(geen)</kbd> : Geen variabelen benodigd.<br/>


action: **import_secrets**<br/>
Nader in te vullen.<br/>
variables:<br/>
<kbd>(geen)</kbd> : Geen variabelen benodigd.<br/>


action: **export_secrets**<br/>
Exporteer secrets uit Vault naar een bestand.<br/>
variables:<br/>
<kbd>vault_address</kbd> : URL naar Vault, bijvoorbeeld `https://192.168.1.0:8200`.<br/>
<kbd>vault_token</kbd> : Token voor toegang tot Vault.<br/>
<kbd>vault_name</kbd> : Naam van de vault (secret_engine) om secrets te exporteren.<br/>
<kbd>secret_name</kbd> : Secret naam.<br/>
<kbd>file_name</kbd> : Bestandsnaam voor export secrets.<br/>


Voorbeeld:
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
  Wijzigingen logboek.<br/>
  Zie [changelog](CHANGELOG.md)<br/>



- **roadmap**<br/>
  Visie en toekomstige ontwikkelingen.<br/>
  Zie [roadmap](ROADMAP.md)<br/>


***


## Voorbereidingen
(geen).<br/>



## Afhankelijkheden
Afhankelijkheden zijn benoemd in het **requirements.yml** bestand. Gebruik `ansible-galaxy install -r requirements.yml --force` voor installatie.<br/>

Indien deze role in andere playbooks of Ansible projecten wordt gebruikt, dient de URL van deze rol te worden toegevoegd aan het `requirements.yml` bestand. Via bovenstaand command wordt de rol dan in de juiste folderstructuur geplaatst.<br/>
<br/>

## Installatie
Geen installatie benodigd.<br/>



## Configuratie
(geen).<br/>



## Overige informatie
(geen).<br/>



## Licentie
MIT



## Auteur
Marcel Venema
