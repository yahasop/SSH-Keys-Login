# SSH-Keys-Login

This guide is for connecting passwordless into another Linux instance, from both a Linux or Windows machine.

    1st Generate a SSH key for sharing the public key of the windows machine using powershell to copy after into the linux instance

ssh-keygen

We can skip when asked for a passphrase by typing enter 3 times. At the end a id_rsa.pub file will be generated into a hidden .ssh folder in our user home folder.

    2nd We can copy the generated key with from a linux instance to another linux instance ssh-copy-id <user@ipadress-of-instance> but  since PoweShell doesn't have this command in windows we have to do it manually or use this single line command.

type $env:USERPROFILE\.ssh\id_rsa.pub | ssh {IP-ADDRESS-OR-FQDN} "cat >> .ssh/authorized_keys"

The type command is an alias for the Get-Content cmdlet which outputs the content of a file. The pipeline grab the input and outputs by concatenating then in the authorized_keys file of the user or ipadress we previously stated to connect by ssh.

We have to replace our IP adresss of the instance and the user <user@ipadress-of-instance> where {IP-ADDRESS-OR-FQDN} is

It will prompt for the password and in the end we will have the public key of the windows machine into the authorized keys file of our linux machine.

 

References:

    From Linux to Linux: https://levelup.gitconnected.com/how-to-connect-without-password-using-ssh-passwordless-9b8963c828e8

    From Windows to Linux: https://chrisjhart.com/Windows-10-ssh-copy-id/ 

    Solutions on how to do it manually or with other methods: https://serverfault.com/questions/224810/is-there-an-equivalent-to-ssh-copy-id-for-windows 
