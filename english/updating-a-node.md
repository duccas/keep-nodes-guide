# Updating a node

You don't need to change anything in the node config files to update. After the official announcement of new contracts or peers, they will be promptly added to my github repository.

### Commands for quick updates

1. Stop containers:

```text
sudo docker stop keep-client && sudo docker rm keep-client
sudo docker stop keep-ecdsa && sudo docker rm keep-ecdsa
```

   2. Enter the following command to download the latest updated files from github:

```text
cd keep-nodes && git pull && cd
```

Everything, after that, your nodes are completely ready for launch.

Next, go to the section Configuring and Running Beacon and ECDSA Nodes and perform steps 5 and 6.

{% page-ref page="obtaining-a-keep-grant/configuring-and-running-beacon-and-ecdsa-nodes.md" %}

### Upgrade issues

If for some reason you cannot update with the command above, then enter the command that completely removes all node directories from your server:

```text
rm -R keep-nodes
```

And then go to the section Configuring and Launching Beacon and ECDSA nodes and rerun starting from point 4.

{% page-ref page="obtaining-a-keep-grant/configuring-and-running-beacon-and-ecdsa-nodes.md" %}

