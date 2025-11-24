<!-- DOCSIBLE START -->

# 📃 Role overview

## role-hardened-docker



Description: hardened setup for Docker on Linux, client TLS for TCP port access to the daemon


| Field                | Value           |
|--------------------- |-----------------|
| Readme update        | 24/11/2025 |








### Defaults

**These are static variables with lower priority**

#### File: defaults/main.yml

| Var          | Type         | Value       |
|--------------|--------------|-------------|
| [rhd_restart_docker](defaults/main.yml#L3)   | bool | `True` |    
| [rhd_docker_restart_handler_state](defaults/main.yml#L4)   | str | `restarted` |    
| [rhd_secured_tcp_listener](defaults/main.yml#L7)   | bool | `False` |    
| [rhd_system_tmp](defaults/main.yml#L11)   | str | `/tmp` |    
| [rhd_country](defaults/main.yml#L12)   | str | `XX` |    
| [rhd_state](defaults/main.yml#L13)   | str | `Default State` |    
| [rhd_locality](defaults/main.yml#L14)   | str | `Default City` |    
| [rhd_organization](defaults/main.yml#L15)   | str | `Default Company` |    
| [rhd_host](defaults/main.yml#L16)   | str | `127.0.0.1` |    
| [rhd_common_name](defaults/main.yml#L17)   | str | `{{ rhd_host }}` |    
| [rhd_passphrase](defaults/main.yml#L18)   | str | `changeme` |    
| [rhd_server_cert_path](defaults/main.yml#L19)   | str | `/etc/docker` |    
| [rhd_client_cert_path](defaults/main.yml#L20)   | str | `~/.docker` |    
| [rhd_days](defaults/main.yml#L21)   | int | `365` |    
| [rhd_ca_days](defaults/main.yml#L22)   | str | `{{ rhd_days }}` |    
| [rhd_server_days](defaults/main.yml#L23)   | str | `{{ rhd_days }}` |    
| [rhd_client_days](defaults/main.yml#L24)   | str | `{{ rhd_days }}` |    
| [rhd_ca_cert_subj](defaults/main.yml#L25)   | str | `/C={{ rhd_country }}/ST={{ rhd_state }}/L={{ rhd_locality }}/O={{ rhd_organization }}/CN={{ rhd_common_name }}` |    


### Vars

**These are variables with higher priority**
#### File: vars/main.yml

| Var          | Type         | Value       |
|--------------|--------------|-------------|
| [rhd_temp_path](vars/main.yml#L2)   | str | `{{ rhd_system_tmp }}/ansible_rhd` |    
| [rhd_passfile](vars/main.yml#L3)   | str | `{{ rhd_temp_path }}/passphrase.txt` |    
| [rhd_csr_form_file](vars/main.yml#L4)   | str | `{{ rhd_temp_path }}/csr_form.txt` |    
| [rhd_extfile](vars/main.yml#L5)   | str | `{{ rhd_temp_path }}/extfile.cnf` |    
| [rhd_server_extfile](vars/main.yml#L6)   | str | `{{ rhd_temp_path }}/server_extfile.cnf` |    
| [rhd_ca_key](vars/main.yml#L7)   | str | `{{ rhd_temp_path }}/ca-key.pem` |    
| [rhd_ca_cert](vars/main.yml#L8)   | str | `{{ rhd_temp_path }}/ca.pem` |    
| [rhd_cl_key](vars/main.yml#L9)   | str | `{{ rhd_temp_path }}/key.pem` |    
| [rhd_cl_csr](vars/main.yml#L10)   | str | `{{ rhd_temp_path }}/client.csr` |    
| [rhd_cl_cert](vars/main.yml#L11)   | str | `{{ rhd_temp_path }}/cert.pem` |    
| [rhd_sv_key](vars/main.yml#L12)   | str | `{{ rhd_temp_path }}/server-key.pem` |    
| [rhd_sv_csr](vars/main.yml#L13)   | str | `{{ rhd_temp_path }}/server.csr` |    
| [rhd_sv_cert](vars/main.yml#L14)   | str | `{{ rhd_temp_path }}/server-cert.pem` |    


### Tasks


#### File: tasks/cleanup.yml

| Name | Module | Has Conditions |
| ---- | ------ | -------------- |
| Delete intermediary files | ansible.builtin.file | False |
| Get stats of the passphrase file | ansible.builtin.stat | False |
| Delete passphrase file | ansible.builtin.file | True |

#### File: tasks/generate_ca_cert.yml

| Name | Module | Has Conditions |
| ---- | ------ | -------------- |
| Get stats of the created CA private key | ansible.builtin.stat | False |
| Get stats of the to be created CA cert | ansible.builtin.stat | False |
| If the file doesn't already exist, generate the CA | block | True |
| Generate CA keys | ansible.builtin.command | False |
| Generate ca certificate | ansible.builtin.command | False |

#### File: tasks/generate_client_cert.yml

| Name | Module | Has Conditions |
| ---- | ------ | -------------- |
| Get stats of the created CA private key | ansible.builtin.stat | False |
| Get stats of the created CA cert | ansible.builtin.stat | False |
| Get stats of the created client cert | ansible.builtin.stat | False |
| Get stats of the created client key | ansible.builtin.stat | False |
| Get stats of the created client CSR | ansible.builtin.stat | False |
| Proceed with client cert creation if CA and its private key exist | block | True |
| Create client key | ansible.builtin.command | False |
| Create client CSR | ansible.builtin.command | False |
| Add extendedKeyUsage to extfile | ansible.builtin.lineinfile | False |
| Create the client certificate | ansible.builtin.command | False |

#### File: tasks/generate_server_cert.yml

| Name | Module | Has Conditions |
| ---- | ------ | -------------- |
| Get stats of the created CA private key | ansible.builtin.stat | False |
| Get stats of the created CA cert | ansible.builtin.stat | False |
| Get stats of the server cert (not running if already exists) | ansible.builtin.stat | False |
| Get stats of the created server key | ansible.builtin.stat | False |
| Get stats of the created server CSR | ansible.builtin.stat | False |
| Proceed with server cert creation if CA and its private key exist | block | True |
| Create server key | ansible.builtin.command | False |
| Create the server CSR | ansible.builtin.command | False |
| Add alt name to extfile | ansible.builtin.lineinfile | False |
| Set the docker daemon's key extended usage attributes to only server authentication | ansible.builtin.lineinfile | False |
| Create the server certificate | ansible.builtin.command | False |

#### File: tasks/main.yml

| Name | Module | Has Conditions |
| ---- | ------ | -------------- |
| Check that docker is installed | ansible.builtin.command | False |
| Check that docker has active systemd service | ansible.builtin.systemd_service | False |
| Unnamed | ansible.builtin.include_tasks | False |
| Unnamed | ansible.builtin.include_tasks | False |
| Unnamed | ansible.builtin.include_tasks | False |
| Unnamed | ansible.builtin.include_tasks | False |
| Unnamed | ansible.builtin.include_tasks | False |
| Unnamed | ansible.builtin.include_tasks | True |
| Unnamed | ansible.builtin.include_tasks | False |
| Unnamed | ansible.builtin.include_tasks | False |

#### File: tasks/organise_cert_files.yml

| Name | Module | Has Conditions |
| ---- | ------ | -------------- |
| Check that the cert paths exists | ansible.builtin.file | False |
| Copy server certs | ansible.builtin.command | False |
| Set file permissions for server certs | ansible.builtin.file | False |
| Copy client certs | ansible.builtin.command | False |
| Set file permissions for client certs | ansible.builtin.file | False |

#### File: tasks/output.yml

| Name | Module | Has Conditions |
| ---- | ------ | -------------- |
| Collect output the dates for client cert | ansible.builtin.command | False |
| Show output of dates for client cert | ansible.builtin.debug | False |
| Collect output the dates for serve cert | ansible.builtin.command | False |
| Show output of dates for serve cert | ansible.builtin.debug | False |

#### File: tasks/prepare.yml

| Name | Module | Has Conditions |
| ---- | ------ | -------------- |
| Create a temp directory | ansible.builtin.file | False |
| Create file with passphrase | ansible.builtin.copy | False |

#### File: tasks/setup_daemon_authenticated_tcp_listener.yml

| Name | Module | Has Conditions |
| ---- | ------ | -------------- |
| Creates directory | ansible.builtin.file | False |
| Enable systemd socket for unix socket access | ansible.builtin.systemd_service | False |
| Create an override for docker systemd service | ansible.builtin.template | False |




## Playbook

```yml
---
- name: Example Usage
  hosts: all
  gather_facts: true # Disable if your role does not rely on facts
  tasks:
    - name: Update apt cache.
      apt: update_cache=yes cache_valid_time=600
      when: ansible_facts.os_family == 'Debian'
    - name: Install docker
      ansible.builtin.import_role:
        name: geerlingguy.docker
      vars:
        docker_service_manage: true
        docker_daemon_options:
          log-opts:
            max-size: "50m"
            max-file: "3"
    - name: Secure Docker with client TLS
      ansible.builtin.include_role:
        name: rmenage.hardened_docker
      vars:
        rhd_server_cert_path: /etc/docker
        rhd_client_cert_path: /vagrant/docker-client-certs
        rhd_host: "0.0.0.0"
        rhd_secured_tcp_listener: yes

```


## Author Information
rmenage

#### License

MIT

#### Minimum Ansible Version

2.15.1

#### Platforms

- **Ubuntu**: ['noble']
- **Rocky**: ['all']


#### Dependencies

No dependencies specified.
<!-- DOCSIBLE END -->
