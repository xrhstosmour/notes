#linux #security #ssh-keys 
In order to transfer the SSH keys:
1. Inside the hidden folder which stores the SSH keys type the following command:
```
ssh-copy-id -f -i <ssh_keys_name>.pub -p <ssh_port_number> <username>@<remote_machine_IP_or_domain>"
```
2. For the transfer to be successful at the remote machine:
	1. The user, of whom the keys belong to, should already be created at the remote machine.
	2. Connecting at the remote machine should be allowed with credentials and not with SSH keys.

- - -

## Troubleshooting
* In case there was a permission error while trying to connect using your SSH keys, execute the following commands and try transferring them again:
```
sudo chmod 600 <path_to_your_private_ssh_key>
sudo chmod 600 <path_to_your_public_ssh_key>.pub
```