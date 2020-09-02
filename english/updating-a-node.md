# Updating a node

You don't need to change anything in the node config files to update. After the official announcement of new contracts or peers, they will be promptly added to my github repository.

### Commands for quick updates

1. Stop containers:

```text
sudo docker stop keep-client && sudo docker rm keep-client
sudo docker stop keep-ecdsa && sudo docker rm keep-ecdsa
```

   2. We enter the following commands to update the contract addresses:

```text
grep -rl 0xf417b31104631280adF9F6828ee19985BC299fdC $HOME/keep-nodes/beacon/config* | xargs perl -p -i -e 's/0xf417b31104631280adF9F6828ee19985BC299fdC/0xC8337a94a50d16191513dEF4D1e61A6886BF410f/g'
grep -rl 0x8117632eC1D514550b3880Bc68F9AC1A76c9C67B $HOME/keep-nodes/beacon/config* | xargs perl -p -i -e 's/0x8117632eC1D514550b3880Bc68F9AC1A76c9C67B/0x234d2182B29c6a64ce3ab6940037b5C8FdAB608e/g'
grep -rl 0xd83248e311DC2Ba0d2A051e86f0678d8857f6ADD $HOME/keep-nodes/beacon/config* | xargs perl -p -i -e 's/0xd83248e311DC2Ba0d2A051e86f0678d8857f6ADD/0x6c04499B595efdc28CdbEd3f9ed2E83d7dCCC717/g'
grep -rl 0xb37c8696cD023c11357B37b5b12A9884c9C83784 $HOME/keep-nodes/ecdsa/config* | xargs perl -p -i -e 's/0xb37c8696cD023c11357B37b5b12A9884c9C83784/0x9EcCf03dFBDa6A5E50d7aBA14e0c60c2F6c575E6/g'
grep -rl 0x9F3B3bCED0AFfe862D436CB8FF462a454040Af80 $HOME/keep-nodes/ecdsa/config* | xargs perl -p -i -e 's/0x9F3B3bCED0AFfe862D436CB8FF462a454040Af80/0xc3f96306eDabACEa249D2D22Ec65697f38c6Da69/g'
```

Everything, after that, your nodes are completely ready for launch.

Next, go to the section Configuring and Running Beacon and ECDSA Nodes and perform steps 5 and 6.

{% page-ref page="installation-guide/configuring-and-running-beacon-and-ecdsa-nodes.md" %}

### Upgrade issues

If for some reason you cannot update with the command above, then enter the command that completely removes all node directories from your server:

```text
rm -R keep-nodes
```

And then go to the section Configuring and Launching Beacon and ECDSA nodes and rerun starting from point 4.

{% page-ref page="installation-guide/configuring-and-running-beacon-and-ecdsa-nodes.md" %}

