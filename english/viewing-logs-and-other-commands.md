# Viewing logs and other commands

### Viewing logs

There are several options for viewing logs.

1. View running containers

```text
docker ps -a
```

![](../.gitbook/assets/image%20%2818%29.png)

   2. Full logs of Beacon and ECDSA nodes:

```text
sudo docker logs keep-client -f --since 1m
sudo docker logs keep-ecdsa -f --since 1m
```

   3. Output of only connected peers \(number of connected peers\):

{% code title="\#FOR BEACON NODE" %}
```text
sudo docker logs -f keep-client --tail 1000 2>&1 | grep "number of connected peers:"
```
{% endcode %}

{% code title="\#FOR ECDSA NODE" %}
```text
sudo docker logs -f keep-ecdsa --tail 1000 2>&1 | grep "number of connected peers:"
```
{% endcode %}

![](../.gitbook/assets/image%20%2821%29.png)

### Additional commands

1. Stopping and removing a container:

```text
sudo docker stop keep-client && sudo docker rm keep-client
sudo docker stop keep-ecdsa && sudo docker rm keep-ecdsa
```

### Save logs to file 

Saving container logs to a file for the last 30 minutes:

```text
sudo docker logs keep-ecdsa --since 30m >& ecdsa.log
```

