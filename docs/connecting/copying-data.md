# File Transfer

Moving files/folders to or from the HPC offers various methods. 

## Secure Copy `scp`

For single file/folder transfers, `scp` through ssh is convenient and widely compatible. Here's a basic usage:

```
scp [from] [to]
```
The source (`from`) and destination (`to`) can each be a filename or a directory on your local machine or a remote host.

**Upload a File from Your Computer to a Cluster**

```
$ scp foobar.txt your_username@clustername:/path/to/remote/directory
```

In this scenario, `foobar.txt` is copied to the directory `/path/to/remote/directory` on remote machine. If `foobar.txt` is not in your current directory, you can specify the full path:

**Upload a Directory to a Cluster**

```
$ scp -r your_directory your_username@clustername:/path/to/remote/directory
```

**Download a File from the Cluster to Your Computer**

```
$ scp your_username@clustername:/path/to/remote/foobar.txt .
```

Here, `.` represents your current working directory. To specify a different destination, replace `.` with the full path:

```
$ scp your_username@clustername:/path/to/remote/foobar.txt /path/to/local/your_folder
```
Further documentation on `scp` can be found [here](https://www.hypexr.org/linux_scp_help.php).

## `rsync`

For more complex transfers, `rsync` offers efficiency, especially for multiple files or entire directory trees. Here's a basic command:

```
$ rsync [options] [source] [destination]
```

```
# Connect to the transfer node from the login node
$ ssh transfer

# Copy a Directory from Local to Remote Server
$ rsync -avzh path/to/local your_username@clustername:/path/to/remote/directory

# Copy a Directory from Remote to Local Server
$ rsync -avzh your_username@clustername:/path/to/remote/directory path/to/local
```

The `-azvh` options enable compressed transfer with readable output, preserving timestamps. Another common option, `-r``, synchronizes all subdirectories recursively.

Further `rsync` documentation is available [here](https://www.tecmint.com/rsync-local-remote-file-synchronization-commands/).

## Rclone

Use Rclone for cloud storage (Box, Dropbox, Wasabi, AWS S3, or Google Cloud Storage, etc.) transfers. Configure Rclone for each storage type and protect configurations with passwords.

```
# Configure Rclone for each storage type using
$ rclone configure
```

During configuration, assign a unique name (e.g., `mys3`) and provide connection details. After saving, connect to the transfer node (via `ssh transfer` from the login node) and use the assigned name for file transfers.

```
# Copy files to cloud storage
$ rclone copy localpath/myfile mys3:bucketname/

$ rclone sync localpath/mydir mys3:bucketname/remotedir
```

An example of executing rclone can be found [here](https://docs.ycrc.yale.edu/clusters-at-yale/guides/rclone/).

## File Transfer Protocol (ftp)

FTP, utilized with programs like [Filezilla](https://filezilla-project.org/), [WinSCP (Windows)](https://winscp.net/eng/index.php) or [Cyberduck  (OS/Windows)](https://cyberduck.io/), is a network protocol for file exchange with a server. Utilizing such programs with graphical interfaces offers beginners flexibility and ease of use.