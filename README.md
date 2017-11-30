# Vagrant Scaffold

A starter kit for provisioning a development server using Vagrant and Ansible.

## Stack

The server will feature the following development environment:

- [Ubuntu](http://releases.ubuntu.com/16.04/) - 16.04 (lts)
- [PHP](http://php.net/releases/7_1_0.php) - 7.1
- [MySQL](https://dev.mysql.com/doc/relnotes/mysql/5.7/en/) - 5.7
- [Node.js](https://nodejs.org/en/blog/release/v8.9.0/) 8.9 (lts)
- [nginx](http://nginx.org/en/CHANGES-1.12) - 1.12 (stable)

## Requirements

The following programs must be install on your machine before you may install.

- [Vagrant](https://www.vagrantup.com/downloads.html) 2.0.x

  ```bash
  export VAGRANT_RELEASES="https://releases.hashicorp.com/vagrant"
  export VAGRANT_VERSION="2.0.1"
  export VAGRANT_DEB="vagrant_${VAGRANT_VERSION}_x86_64.deb"
  curl -O "${VAGRANT_RELEASES}/${VAGRANT_VERSION}/${VAGRANT_DEB}"
  sudo dpkg -i ${VAGRANT_DEB}
  rm ${VAGRANT_DEB}
  ```

- [VirtualBox](https://www.virtualbox.org/wiki/Downloads) 5.2.x

  ```bash
  export VBOX_PATH="http://download.virtualbox.org/virtualbox/debian"
  wget -q -O- ${VBOX_PATH}/oracle_vbox_2016.asc | sudo apt-key add -
  echo "deb ${VBOX_PATH} $(lsb_release -cs) contrib" | sudo tee /etc/apt/sources.list.d/virtualbox.list
  sudo apt-get update
  sudo apt-get install virtualbox-5.2
  ```

- [Ansible](http://docs.ansible.com/ansible/latest/intro_installation.html) 2.4.x

  ```bash
  sudo add-apt-repository -y ppa:ansible/ansible
  sudo apt-get update
  sudo apt-get install -y ansible
  ```

## How To Install

#### 1. Clone the project repo:
    
```bash
git clone https://github.com/jabes/vagrant-scaffold.git
cd vagrant-scaffold
```

#### 2. Copy the Ansible key into the vault:
  
**IMPORTANT:** The key below is for the localhost environment only.
Make sure that you use a different secret key for production environments.

```bash
mkdir -p ~/.ansible-vault
echo "SuperSecretPassword" > ~/.ansible-vault/vagrant-scaffold
```

You can now view secret info using Ansible vault commands:

```bash
cd ansible
ansible-vault view inventories/local/group_vars/secrets.yml
```

#### 3. Fetch required Ansible packages:

```bash
cd ansible
ansible-galaxy install -r requirements.yml
```

#### 4. Download and provision the server:

**NOTE:** The boxes are pretty large and provisioning can take a while.
This is a good time to take a coffee break.

```bash
vagrant plugin install vagrant-vbguest
vagrant plugin install vagrant-hostsupdater
vagrant up
```

If everything went well..

- web server: [http://vagrant-scaffold.dev](http://vagrant-scaffold.dev)
