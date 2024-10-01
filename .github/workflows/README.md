# Automated build & deployment with Github Actions

This Jekyll workflow triggers consecutive actions on a remote GitHub Actions server for each push to the master branch : 
- Clone repo & build jekyll website (into folder "_site")
- rename _site folder to www
- scp to ENS server (ssh key)

## Usage
To use it, you only have to setup the ssh connection properly.

### 1. Setup an ssh key
The ssh key must be **without** a passphrase. You can enter the following command, and then when asked for a passphrase & confirmation, tap *enter*.
```
# rsa
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"

# ed25519
ssh-keygen -t ed25519 -a 200 -C "your_email@example.com"
```
Add the public key to the ENS server (.ssh/authorized_keys)

### 2. Store Secret variables
Got into the repositories settings, then "Secrets and variables", then Actions.
**4 secret variables** must be stored. Add or replace existing ones if needed.
- **HOST** : ssh host adress
- **USERNAME** : Username for ssh connection, must be the same used for dropping the public key on the server.
- **TARGET_PATH** : remote path for storing the www folder : /XXX/XXXX/
- **PRIVATE_SSH_KEY** : Paste private ssh key

### All logs are available in the Actions section of the repository, with each run named after the commit or push that triggered it.
