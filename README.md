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
- [VirtualBox](https://www.virtualbox.org/wiki/Downloads) 5.2.x
- [Ansible](http://docs.ansible.com/ansible/latest/intro_installation.html) 2.4.x

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
vagrant plugin install vagrant-hostsupdater
vagrant box update
vagrant up
```

If everything went well..

- web server: [http://vagrant-scaffold.dev](http://vagrant-scaffold.dev)
- mysql admin : [http://vagrant-scaffold.dev/phpmyadmin](http://vagrant-scaffold.dev/phpmyadmin)
