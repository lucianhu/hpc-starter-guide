# SSH (Secure Shell) keys

When connecting via SSH, entering your password every time can be repetitive. SSH keys offer a password-free alternative, enhancing both convenience and security. 

!!! warning
    Smile's clusters still use passwords, while **Lulu's clusters require users to submit public keys for authentication**.

## How do SSH-Keys work?

Imagine having a two-part security system: a public key (like a lock) and a private key (like a key). Anyone can see the public key, but only your private key unlocks it. Similarly, your public key is shared with the server, while your private key stays secret.

Traditionally, the [RSA](https://en.wikipedia.org/wiki/RSA_(cryptosystem)) algorithm was used for SSH keys. However, [elliptic curve cryptography](https://en.wikipedia.org/wiki/EdDSA) (specifically, `ed25519`) has emerged as a more secure and efficient alternative. We recommend using `ed25519`` SSH keys for enhanced security and performance.

For deeper understanding, explore these Wikipedia articles about [public-key cryptography](https://en.wikipedia.org/wiki/Public-key_cryptography) and [challenge-response authentication](https://en.wikipedia.org/wiki/Challenge-response_authentication).

## Setting Up SSH Keys (macOS/Linux)

### 1. Generate a key pair: 

Check if your SSH already has a key by verifying if a file named ~/.ssh/id_xxx.pub exists. If not, create a key using the following command (including your email address for easy identification later on):

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

### 2. Upload your public key: 

Copy the output of:

```
$ cat ~/.ssh/id_ed25519.pub
```
and share it with the cluster administrator.

### 3. Connect to a cluster

```
$ ssh netid@clustername
```


## Windows

We recommend using the [Web Portal (Open OnDemand)](/clusters-at-yale/access/ood) to connect to the clusters from Windows. If you need advanced features beyond the web portal, we recommend using [MobaXterm](https://mobaxterm.mobatek.net/).


### MobaXterm
You can download, extract & install MobaXterm from [this page](https://mobaxterm.mobatek.net/download-home-edition.html). We recommend using the "Installer Edition", but make sure to extract the zip file before running the installer.

You can also use one of the [Windows Subsystem for Linux (WSL)](https://docs.microsoft.com/en-us/windows/wsl/install-win10) distributions and follow the Linux instructions above. However, you will probably run into issues if you try to use any graphical applications.

### Generate Your Key Pair on Windows

First, generate an SSH key pair if you haven't already:

* Open MobaXterm.
* From the top menu choose Tools -> MobaKeyGen (SSH key generator).
* Leave all defaults and click the "Generate" button.
* Wiggle your mouse.
* Click "Save public key" and save your public key as id_rsa.pub.
* Choose a secure passphrase and enter into the two relevant fields. Your passphrase will prevent access to your account in the event your private key is stolen.
* Click "Save private key" and save your private key as id_rsa.ppk (this one is secret, *don't give it to other people*).
* Copy the text of your public key and paste it into the text box in our [SSH key uploader](https://sshkeys.ycrc.yale.edu/).
* Your key will be synced out to the clusters in a few minutes.

### Connect with MobaXterm

To make a new connection to one of the clusters:

* Open MobaXterm.
* From the top menu select Sessions -> New Session.
* Click the SSH icon in the top left.
* Enter the cluster login node address (e.g. grace.ycrc.yale.edu) as the Remote Host.
* Check "Specify Username" and Enter your netID as the the username.
* Click the "Advanced SSH Settings" tab and check the "Use private key box", then click the file icon / magnifying glass to choose where you saved your private key (id_rsa.ppk).
* Click OK.

![Sample SSH Configuration](/img/ssh-connection.png)

In the future, your session should be saved in the sessions bar on the left in the main window.