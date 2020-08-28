# Known errors

### Error 1

If you get an error, as in the screenshot below, then the first thing you need to do is check if the contracts are authorized in the KEEP dashboard - [https://dashboard.test.keep.network/applications/random-beacon](https://dashboard.test.keep.network/applications/random-beacon).   
If everything is authorized, then the problem is most likely in the Infura account.

![](../.gitbook/assets/image%20%2824%29.png)

1. You need to log into your Infura account 
2. Select the project BEACON NODE \(you can name it whatever you like\)

![](../.gitbook/assets/image%20%2820%29.png)

   3. Go to project settings

![](../.gitbook/assets/image%20%2823%29.png)

   4. And in the ALLOWLIST CONTRACT ADDRESSES field, insert your ETH address and press ADD

![](../.gitbook/assets/image%20%2819%29.png)

   5. Do the same for the ECDSA node project.   
   6. Done.

### Error 2

If after launching we see similar text in the logs, then we have a problem with the password.

> FATAL keep-main error reading config file: password is required; set in the config file, set environment variable KEEP\_ETHEREUM\_PASSWORD to the password, or set the same environment variable to 'prompt' to be prompted for the password at startup

![](../.gitbook/assets/image%20%2826%29.png)

1.  Let's re-export the password with the command:

```text
export ETH_PASSWORD=$(cat $HOME/keep-nodes/data/eth-address-pass.txt)
```

   2. If this does not help, then you need to write your password directly into the launch command as in the screenshot below instead of $ETH\_PASSWORD:

![Replace $ETH\_PASSWORD with your wallet password](../.gitbook/assets/image%20%2825%29.png)

   3. You can run your nodes.

