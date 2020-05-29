# Instalação do K8s via ansible

Role criada para instalar os pacotes necessários para criar um cluster kubernetes.

## Para executar a playbook

* Primeiro, insira os IPs dentro do arquivo **hosts.yml**, colocando-os nos grupos corretos:

  * No grupo **[all]** deve conter todos os IPs
  * No grupo **[master]** o IP da máquina que será o Master do cluster
  * No grupo **[workers]** os IPs das máquinas que serão os Workers

    Exemplo:
   ```bash
        [all]
        35.192.33.162
        35.188.212.119
        35.225.194.119

        [master]
        35.192.33.162

        [workers]
        35.188.212.119
        35.225.194.119
    ```

* Segundo, execute a role que vai instalar o docker, o kubeadm, kubebelet, kubectl em todas as máquinas, dessa forma:
    ```bash
     ansible-playbook -i hosts.yml install-k8s-playbook.yml
    ```
* Terçeiro, execute a role que vai configurar e iniciar o cluster no master, com esse comando:
    ```bash
     ansible-playbook -i hosts.yml init-master.yml
    ```
* Quarto, execute a role que vai configurar os workers do cluster com o comando:
    ```bash
     ansible-playbook -i hosts.yml init-workers.yml
    ```