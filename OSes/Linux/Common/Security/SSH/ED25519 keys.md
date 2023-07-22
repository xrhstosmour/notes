#linux #security #ssh-keys #ed25519
In order to create elliptic curve ED25519 SSH keys:
1. Create a hidden .ssh folder, at local machine.
2. Inside the hidden folder type the following command:
```
ssh-keygen -t ed25519 -f ./<ssh_keys_name> -C "<comment_of_your_choice>"
```
3. The below command will create one private SSH and one public SSH key (the one ending in .pub)