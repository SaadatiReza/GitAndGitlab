# Setup SSH
To setup ssh connection with key-pairs, you should create a key-pair based on your needed.
you could use the below command.
```bash
ssh-keygen -t ed25519
```
**Note:** during the execution of the above command you will be asked to define passphrase, it has been highly recommended to use passphrase to protect your keys in case of that anyone has took access to your keys.

regarding to your ```/home/$(whoami)/.ssh``` and in windows are stored in ```C:\Users\[YourUsername]\.ssh```.

Now you must copy your public key in the target machine.
```bash
vim /home/$(whoami)/.ssh/authorized_keys
``` 
then append your public key in that file.

