# SSH (Secure Shell) keys

When connecting via SSH, entering your password every time can be repetitive. SSH keys offer a password-free alternative, enhancing both convenience and security. 

!!! warning 
    Smile's clusters still use passwords, while **lulu's clusters require users to submit public keys for authentication**.

!!! info
    Currently, GitHub utilizes SSH for accessing and editing data in its repositories.

## How do SSH-Keys work?

Imagine having a two-part security system: a public key (like a lock) and a private key (like a key). Anyone can see the public key, but only your private key unlocks it. Similarly, your public key is shared with the server, while your private key stays secret.

Traditionally, the [RSA](https://en.wikipedia.org/wiki/RSA_(cryptosystem)) algorithm was used for SSH keys. However, [elliptic curve cryptography](https://en.wikipedia.org/wiki/EdDSA) (specifically, `ed25519`) has emerged as a more secure and efficient alternative. We recommend using `ed25519` SSH keys for enhanced security and performance.

For deeper understanding, explore these Wikipedia articles about [public-key cryptography](https://en.wikipedia.org/wiki/Public-key_cryptography) and [challenge-response authentication](https://en.wikipedia.org/wiki/Challenge-response_authentication).

## Setting Up SSH Keys (macOS/Linux)

### 1. Generate a key pair: 

Check if your SSH already has a key by verifying if a file named `~/.ssh/id_xxx.pub` exists. If not, create a key using the following command (including your email address for easy identification later on):

```
$ ssh-keygen -t ed25519 -C "your_email@example.com"
```

Your terminal should respond:

```
Generating public/private ed25519 key pair.
```

Press Enter to accept the default value. Choose a strong passphrase to protect your account if your private key is compromised.

```
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
```

The key pair is saved in the `.ssh` directory in your home folder, with the public key located at `~/.ssh/id_ed25519.pub`. If you forget your passphrase, recovery isn't possible; you'll have to generate and upload a new SSH key pair.

The session should resemble the following:

```shell
host:~$ ssh-keygen -t ed25519 -C "your_email@example.com"
Generating public/private ed25519 key pair.
Enter file in which to save the key (/home/USER/.ssh/id_ed25519): 
Enter passphrase (empty for no passphrase):
Enter same passphrase again: 
Your identification has been saved in /home/USER/.ssh/id_ed25519.
Your public key has been saved in /home/USER/.ssh/id_ed25519.pub.
The key fingerprint is:
SHA256:Z6InW1OYt3loU7z14Kmgy87iIuYNr1gJAN1tG71D7Jc your_email@example.com
The key's randomart image is:
+--[ED25519 256]--+
|.. . . o         |
|. . . + +        |
|.    . = . .     |
|.     . +oE.     |
|.       So= o o  |
| . .   . * = + + |
|  +   o + B o o .|
| oo+. .B + + .   |
|.ooooooo*.  .    |
+----[SHA256]-----+
```

The content of ~/.ssh/id_ed25519.pub should resemble this:

```
ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIFzuiaSVD2j5y6RlFxOfREB/Vbd+47ABlxF7du5160ZH your_email@example.com
```

To avoid entering the passphrase each time, you can add your key to the SSH agent, which manages keys and remembers passphrases.

```
$ eval "$(ssh-agent -s)"
$ ssh-add
```

For MacOS connection issues with SSH keys, try:

```
$ ssh-add --apple-use-keychain
```

To verify that the agent is running and your key is loaded, use:

```
$ ssh-add -l
```

Ensure the command prints at least one key, displaying the key size, fingerprint hash, and file location in the file system.

### 2. Upload your public key: 

Copy the output of:

```
$ cat ~/.ssh/id_ed25519.pub
```
and share it with the cluster administrator.

### 3. Connect to a cluster

```
$ ssh your_username@clustername
```

## Using Windows

We recommend using MobaXterm on Windows for SSH connections as it simplifies SSH key management. 

To get MobaXterm:

* Visit https://mobaxterm.mobatek.net/download-home-edition.html
* Download either the Portable edition (blue button on the left, suitable for users without admin rights) or the Installer edition (green button on the right, requires admin rights).
* Install or unpack MobaXterm and launch the software. Remember to dismiss any firewall warnings that may appear.

Here's how to set up SSH keys with MobaXterm:

* Open MobaXterm.
* Go to Tools -> MobaKeyGen (SSH key generator).
* Click "Generate" with default settings.
* Move your mouse to generate randomness.
* Save the public key as id_rsa.pub and the private key (keep this secret!) as id_rsa.ppk.
* Upload your public key: Copy the public key text and forward it to the cluster administrator.
* Connect to a cluster using MobaXterm.

## Connecting from Another Computer/Laptop
To connect to the cluster from a different computer than the one where your SSH keys are stored, you have two options:

* Generate a new SSH key pair and submit the public part as explained earlier.
* Copy the private part of the SSH key (`~/.ssh/id_ed25519`) to the second computer in the same location.

```
$ cd ~/.ssh
$ chmod g-rwx id_ed25519*
$ ssh-add id_ed25519
```

!!! danger
    Do not keep the key on any USB stick. Delete it after transferring the file. This is sensitive data. Ensure that the files are only readable by you.





