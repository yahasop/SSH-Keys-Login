# SSH-Keys-Login

This guide is for connecting passwordless into another Linux instance, from both a Linux or Windows machine.

**Linux**

Generate a SSH key for sharing the public key of our local Linux machine using any shell to copy into the remote Linux instance

    ssh-keygen

We can skip when asked for a passphrase by typing enter 3 times. At the end an id_rsa.pub file will be generated into a hidden .ssh folder in our user's home folder.
Then we have to copy the generated key with from our linux instance to the remote linux instance with:

    ssh-copy-id <user@ipadress-of-instance>

It will prompt for the password and in the end we will have the public key of the Linux machine into the authorized keys file of our linux machine.
And after that, the output itself will tell us how to connect passwordless to the instance which will be with:
    
    ssh <user@ipadress-of-instance>

**Windows**

Generate a SSH key for sharing the public key of our local Windows machine using any shell to copy into the remote Linux instance

    ssh-keygen

We can skip when asked for a passphrase by typing enter 3 times. At the end an id_rsa.pub file will be generated into a hidden .ssh folder in our user's home folder.
Since PowerShell doesn't have a native ssh-copy-id command in Windows we have to do it manually (copy the id_rsa.pub key and then log into our remote Linux machine and then copy the key into /home/"our-user"/.ssh/authorized_keys) or use this single line command. We have to replace the IP adresss of the instance and the user where {IP-ADDRESS-OR-FQDN} is:

    type $env:USERPROFILE\.ssh\id_rsa.pub | ssh {IP-ADDRESS} "cat >> .ssh/authorized_keys"

The type command is an alias for the Get-Content cmdlet which outputs the content of a file. Then we pipe it to use the output as input of the next command and concatenating the contents into said authorized_keys file in the user's home directory.
It will prompt for the password and in the end we will have the public key of the Linux machine into the authorized keys file of our Linux machine.
And after that, the output itself will tell us how to connect passwordless to the instance which will be with:
    
    ssh <user@ipadress-of-instance>



References:

    From Linux to Linux: https://levelup.gitconnected.com/how-to-connect-without-password-using-ssh-passwordless-9b8963c828e8

    From Windows to Linux: https://chrisjhart.com/Windows-10-ssh-copy-id/ 

    Solutions on how to do it manually or with other methods: https://serverfault.com/questions/224810/is-there-an-equivalent-to-ssh-copy-id-for-windows 
