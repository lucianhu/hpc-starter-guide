# SSH Connection

SSH, or Secure Shell, lets you securely connect to remote computers (usually Linux/UNIX) over a network. 

Imagine you have a powerful computer cluster far away. SSH allows you to connect to those machines and control them from your own computer.

Here's how to get started:

## 1. Installation

Linux/UNIX: Install the `openssh-client` package.

Windows: Consider tools like MobaXterm or Putty.

## 2. Connection

Your local machine is the "client" and the remote one is the "server." You'll need the server's hostname, IP address (maybe port number), username, and password.

### For Linux/UNIX :

Open a terminal and type:

```
# Default port
$ ssh <username>@<hostname-or-ip-address>

# Non-default port
$ ssh <username>@<hostname-or-ip-address> -p <port-number>
```

### For Windows (MobaXterm):

* Open MobaXterm

* Create a new session (Sessions -> New Session)

* Select the SSH icon and enter the cluster login node address (e.g., tcp.ap.ngrok.io for SMILE's Cluster or giangnguyen.zapto.org for LULU's Cluster)

* Specify your account_name as the username

* Under "Advanced SSH Settings," enable "Use private key" and choose your private key file (`id_rsa.ppk`)

* Click OK

* Your saved session should appear in the MobaXterm main window

### Configure SSH Client

For a more convenient connection to the cluster, create a personalized SSH configuration file. This reduces typing significantly. Add these lines to `~/.ssh/config`, replacing `USER_NAME` with your cluster username. Customize Host naming as preferred.

```
Host smile
    HostName tcp.ap.ngrok.io
    User USER_NAME

Host lulu
    HostName giangnguyen.zapto.org
    User USER_NAME
```

After configuring this file, you can simply type the following command to connect without needing to recall the login node's hostname:

```
$ ssh smile
```