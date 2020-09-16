# Configuring and Running Beacon and ECDSA Nodes

### 1. Preparation

Launch the terminal of our server on the site where the server was created or through special programs described in the section:

{% page-ref page="../../getting-started/technical-requirements.md" %}

### 2. Setting up Ubuntu

Update packages on the server to the latest versions:

```text
sudo apt update && sudo apt upgrade -y
```

Install the git package if it is not installed on the server:

```text
yes | sudo apt install git
```

Install Docker:

```text
sudo apt install docker.io curl -y
```

Activate Docker:

```text
sudo systemctl start docker
sudo systemctl enable docker
```

### 3. Firewall configuration

Open ports 22, 3919 and 3920 and activate the Firewall:

```text
sudo ufw allow 22 && sudo ufw allow 3919 && sudo ufw allow 3920 && yes | sudo ufw enable
```

Check the status of open ports with the command:

```text
sudo ufw status
```

### 4. Setting up nodes

First, download the repository to the github server with all the folders and configs for running two nodes with the command:

```text
git clone https://github.com/icohigh/keep-nodes.git
```

1. In the commands below, replace "YOUR ETH ADDRESS" with the address of your ETH wallet. 
2. "YOUR PASSWORD" for the password from the ETH wallet. 
3. "CONTENT OF FILE UTC--2020-08-24T16-27-57" to the contents of the file downloaded when creating the ETH wallet. 
4. Enter all these commands.

```text
echo 'YOUR ETH ADDRESS' >> $HOME/keep-nodes/data/eth-address.txt
echo 'YOUR PASSWORD' >> $HOME/keep-nodes/data/eth-address-pass.txt
echo 'CONTENT OF FILE UTC--2020-08-24T16-27-57' >> $HOME/keep-nodes/data/keep_wallet.json
```

It should look like this:

{% code title="\#EXAMPLE" %}
```text
echo '0x208E233b930aacC7E17768F02106b6429B822133' >> $HOME/keep-nodes/data/eth-address.txt
echo 'qwerty123' >> $HOME/keep-nodes/data/eth-address-pass.txt
echo '{"version":3,"id":"d01c210a-1206-4754-9202-9f3g87472afe","address":"0x208E233b930aacC7E17768F02106b6429B822133","crypto":{"ciphertext":"85b53ab95e6fbea53f123123b5p234ujdce2122b08f6a73310f2d131e700","cipherparams":{"iv":"13d3efdead3523501ae8ede4328duwh4158"},"cipher":"aes-128-ctr","kdf":"scrypt","kdfparams":{"dklen":32,"salt":"ffad567d42eb5b3f1907e91023478fhs234r720234fs21a0a324cffc9e6c119137","n":131072,"r":8,"p":1},"mac":"c3b300aa4db1531add1c7c78d73d88f75a387485627g46539f1027999c66517"}}' >> $HOME/keep-nodes/data/keep_wallet.json
```
{% endcode %}

   5. Write the export data of your Password and server IP to the .profile file by entering the commands:

```text
echo 'export ETH_PASSWORD=$(cat $HOME/keep-nodes/data/eth-address-pass.txt)' >> $HOME/.profile
echo 'export SERVER_IP=$(curl ifconfig.co)' >> $HOME/.profile
```

   6. Now we need to add in the config file INFURA ID from your account [https://infura.io/](https://infura.io/) created earlier.   
Insert instead of "YOUR\_INFURA\_ID\_BEACON\_NODE" and "YOUR\_INFURA\_ID\_ECDSA\_NODE", respectively, the ID of the Beacon and ECDSA nodes.

```text
grep -rl INFURA_BEACON_ID $HOME/keep-nodes/beacon/config* | xargs perl -p -i -e 's/INFURA_BEACON_ID/YOUR_INFURA_ID_BEACON_NODE/g'
grep -rl INFURA_ECDSA_ID $HOME/keep-nodes/ecdsa/config* | xargs perl -p -i -e 's/INFURA_ECDSA_ID/YOUR_INFURA_ID_ECDSA_NODE/g'
```

It should look like this:

{% code title="\#EXAMPLE" %}
```text
grep -rl INFURA_BEACON_ID $HOME/keep-nodes/beacon/config* | xargs perl -p -i -e 's/INFURA_BEACON_ID/6e6a4ed128a5f7s82bcc470710fb0/g'
grep -rl INFURA_ECDSA_ID $HOME/keep-nodes/ecdsa/config* | xargs perl -p -i -e 's/INFURA_ECDSA_ID/a888cf7gy6e888b0d21ee96b4201e0/g'
```
{% endcode %}

    7. Now let's export the password with the command:

```text
export ETH_PASSWORD=$(cat $HOME/keep-nodes/data/eth-address-pass.txt)
```

   8. Everything is ready to go!

### 5. Launching a Beacon node

Launch the Bacon node with the command below:

```text
sudo docker run -d \
--entrypoint /usr/local/bin/keep-client \
--restart always \
--volume $HOME/keep-nodes/data:/mnt/data \
--volume $HOME/keep-nodes/beacon/config:/mnt/beacon/config \
--volume $HOME/keep-nodes/beacon/persistence:/mnt/beacon/persistence \
--env KEEP_ETHEREUM_PASSWORD=$ETH_PASSWORD \
--env LOG_LEVEL=debug \
--name keep-client \
-p 3919:3919 \
keepnetwork/keep-client:v1.3.0-rc.4 --config /mnt/beacon/config/config.toml start
```

### 6. Launching an ECDSA node

Launch the ECDSA node with the following command:

```text
sudo docker run -d \
--entrypoint /usr/local/bin/keep-ecdsa \
--restart always \
--volume $HOME/keep-nodes/data:/mnt/data \
--volume $HOME/keep-nodes/ecdsa/config:/mnt/ecdsa/config \
--volume $HOME/keep-nodes/ecdsa/persistence:/mnt/ecdsa/persistence \
--env KEEP_ETHEREUM_PASSWORD=$ETH_PASSWORD \
--env LOG_LEVEL=debug \
--name keep-ecdsa \
-p 3920:3919 \
keepnetwork/keep-ecdsa-client:v1.2.0-rc.5 --config /mnt/ecdsa/config/config.toml start
```

### 7. Stop and delete

The container can be stopped and removed using the following commands:

```text
sudo docker stop keep-client && sudo docker rm keep-client
sudo docker stop keep-ecdsa && sudo docker rm keep-ecdsa
```

### 8. Important!

{% page-ref page="../updating-a-node.md" %}

