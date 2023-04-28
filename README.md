# PC do Manual

## Configurando o PC do Manual pela primeira vez
Antes de rodar o Ansible pela primeira vez, precisamos criar o usuário no servidor que irá rodar os comandos remotamente.

Use os seguintes comandos **no servidor**:
```bash
# adiciona o usuário pcdomanual sem senha, no grupo sudo
$ adduser --disabled-password --gecos "" pcdomanual
$ adduser pcdomanual sudo

# habilita a elevação de privilégios sem senha
$ echo 'pcdomanual ALL=(ALL) NOPASSWD:ALL' > /etc/sudoers.d/pcdomanual

# cria o diretório e arquivo que com as chaves SSH
$ mkdir /home/pcdomanual/.ssh
$ touch /home/pcdomanual/.ssh/authorized_keys

# agora copie sua chave SSH para o arquivo /home/pcdomanual/.ssh/authorized_keys

# ajuste as permissões do arquivo com a chave SSH
$ chown -R pcdomanual:pcdomanual /home/pcdomanual/.ssh
```

## Configurando o servidor
Usamos a ferramenta de automação [Ansible](https://www.ansible.com/) para configurar o servidor. Ela permite que escrevemos toda a configuração em código e a executamos com um comando!

Use o comando abaixo para configurar o servidor:
```
$ ansible-playbook -i hosts --limit production site.yml 
```

Pode-se também usar `tags` para executar somente uma parte da configuração:
```
$ ansible-playbook -i hosts --limit production site.yml --tags nitter
```

## Testando localmente
Você pode usar o [Vagrant](Vagrantfile) para rodar uma versão do PC do Manual localmente.

Instale o [Vagrant](https://developer.hashicorp.com/vagrant/docs/installation), [VirtualBox](https://www.virtualbox.org/) e o [Ansible]().

No terminal, inicialize a máquina virtual do Vagrant:
```
$ vagrant up
```

Execute o Ansible usando a chave SSH do Vagrant:
```
$ ansible-playbook -i hosts --limit vagrant site.yml --key-file "$PWD/.vagrant/machines/default/virtualbox/private_key"
```

Para acessar um serviço, adiciona uma linha no seu arquivo `/etc/hosts` apontando o IP `192.168.56.10` para o endereço `<serviço>.pcdomanual.local`. Por exemplo:

```
$ cat /etc/hosts

182.168.56.10 nitter.pcdomanual.local
```

Ao acessar `nitter.pcdomanual.local` no seu navegador, você receberá um alerta de certificado inválido. Você pode ignorar o alerta e prosseguir, já que se trata de uma versão local para testes.
