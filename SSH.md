## Generate Key-Pair
type into a terminal: 
`ssh-keygen -t ed25519`
This will create an ssh key pair (private & public key) using the ed25519 algorithm.

It will prompt you on where to store this key (path and file name).  A good place to put it is into your device account folder and then into a subfolder called '.ssh' (ie c:\\Users\\username/.ssh/filename)

It will then prompt you to enter a new password and then re-enter to confirm.  This will need to be used everytime you use the key.  This password is optional and if you just hit enter for both prompts without typing anything, then it will not have a password and will not prompt you for the password.

After that, it will generate the key pair and then display the finger print for your key (you can just ignore this in most cases)

## Adding Key to Client
Now that you have this key, you need to actually tell your computer to use it.  On windows (in powershell), run the command `Get-Service ssh-agent | Set-Service -StartupType Automatic` to set the ssh-agent to automatically start-up when you start your computer. Then, run the command `Start-Service ssh-agent` to start the service if it isn't already running.  You can run the command `Get-Service ssh-agent` to see if the ssh-agent is running or not.  Finally, you can add the key by entering, `ssh-add $env:USERPROFILE\.ssh\filename` if you used the location I specified earlier (otherwise replace the part after 'ssh-add' with the file path that you used)

## Creating a SSh Config on Windows
An ssh config can specify default values for ssh-ing into a server so that you don't need to specifiy the value each time.
In your user account's .ssh folder, create a file named 'config' with no file extension. Edit the file and add something like:
```
Host server
  HostName server.address
  User username
  Port 22
  PreferredAuthentications publickey
  IdentityFile ~/.ssh/filename
```

replace the 'server' after host, 'server.address', 'username', and the 'filename' with the values for your needs (you may also need to change the port number, but 22 is the default).

## Adding Key to Server
To tell the server to accept your key, you will need to authorize the key.  This can easily be done on Linux by signing on to the server and going to the user account's home folder and then the '.ssh' subfolder (if it's not there, just create it with `mkdir ~/.ssh`).  Either create or edit a file named 'authorized_keys' copy the contents of your PUBLIC key (THIS NEEDS TO BE YOUR PUBLIC KEY NOT YOUR PRIVATE KEY. DO NOT USE YOUR PRIVATE KEY. YOUR PRIVATE KEY NEEDS TO BE PRIVATE!!!).  If you ssh'ed into the server you may be able to simply copy paste the key into file.  If not, you may need to either input it manually or copy the public key file using a command like `scp -i ~/.ssh/filename.pub user@server:/<filepath on host> <path on client>`.  Make sure the permissions are correct on the authorized_keys file.  If you enter the command 'ls -alh' inside the .ssh folder, you should see on the left side, a section with r's w's x's and -'s.  This specifies file premissions for Reads, Writes, and eXecutes for the file/folder.  The file should have only read and write privileges for the user (ie -rw-------).  If this isn't the case, you can change the file permissions by entering `chmod 600 authorized_keys` (this is binary where 6 is 110 for the first three --- and 0 for the other two sets of ---).

## Disable Password
On Linux, go to the file `/etc/ssh/sshd_config` and look for the line `#PasswordAuthentication yes` then replace it with `PasswordAuthentication no`. Save and exit the file to confirm the change.  Finally, restart the ssh service to implement the new changes with `sudo service ssh restart`.