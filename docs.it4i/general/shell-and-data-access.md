# Accessing the Clusters

## Shell Access

All IT4Innovations clusters are accessed by the SSH protocol via login nodes at the address **cluster-name.it4i.cz**. The login nodes may be addressed specifically, by prepending the loginX node name to the address.

!!! note
    The **cluster-name.it4i.cz** alias is currently not available through VPN connection. Use **loginX.cluster-name.it4i.cz** when connected to VPN.

### Barbora Cluster

| Login address             | Port | Protocol | Login node                            |
| ------------------------- | ---- | -------- | ------------------------------------- |
| barbora.it4i.cz           | 22   | SSH      | round-robin DNS record for login[1-2] |
| login1.barbora.it4i.cz    | 22   | SSH      | login1                                |
| login2.barbora.it4i.cz    | 22   | SSH      | login2                                |

### Salomon Cluster

| Login address          | Port | Protocol | Login node                            |
| ---------------------- | ---- | -------- | ------------------------------------- |
| salomon.it4i.cz        | 22   | SSH      | round-robin DNS record for login[1-4] |
| login1.salomon.it4i.cz | 22   | SSH      | login1                                |
| login2.salomon.it4i.cz | 22   | SSH      | login2                                |
| login3.salomon.it4i.cz | 22   | SSH      | login3                                |
| login4.salomon.it4i.cz | 22   | SSH      | login4                                |

## Authentication

Authentication is available by [private key][1] only. Verify SSH fingerprints during the first logon:

Barbora:

```console
    md5:
    39:55:e2:b9:2a:a2:c4:9e:b1:8e:f0:f7:b1:66:a8:73 (RSA)
    63:29:4c:3d:17:8c:be:73:4a:99:ff:83:66:ba:dd:c3 (ECDSA)
    40:67:03:26:d3:6c:a0:7f:0a:df:0e:e7:a0:52:cc:4e (ED25519)

    sha256:
    TO5szOJf0bG7TWVLO3WABUpGKkP7nBm/RLyHmpoNpro (RSA)
    lg+AaptpqFlEu5+lBecgaVdiSlYljo5+ADLItQRSYVA (ECDSA)
    ZQzFTJVDdZa3I0ics9ME2qz4v5a3QzXugvyVioaH6tI (ED25519)
```

Salomon:

```console
    md5:
    f6:28:98:e4:f9:b2:a6:8f:f2:f4:2d:0a:09:67:69:80 (DSA)
    70:01:c9:9a:5d:88:91:c7:1b:c0:84:d1:fa:4e:83:5c (RSA)
    66:32:0a:ef:50:01:77:a7:52:3f:d9:f8:23:7c:2c:3a (ECDSA)
    ab:3d:5e:ff:82:68:c7:72:da:4a:2d:e3:ca:85:0d:df (ED25519)

    sha256:
    epkqEU2eFzXnMeMMkpX02CykyWjGyLwFj528Vumpzn4 (DSA)
    WNIrR7oeQDYpBYy4N2d5A6cJ2p0837S7gzzTpaDBZrc (RSA)
    cYO4UdtUBYlS46GEFUB75BkgxkI6YFQvjVuFxOlRG3g (ECDSA)
    bFm3stNM8ETmj8Xd7iPXNtu5X5dC2apLNXGiH3VSTuw (ED25519)
```

!!! note
    SSH fingerprints are identical on all login nodes.

Private key authentication:

On **Linux** or **Mac**, use:

```console
$ ssh -i /path/to/id_rsa username@cluster-name.it4i.cz
```

If you see a warning message **UNPROTECTED PRIVATE KEY FILE!**, use this command to set lower permissions to the private key file:

```console
$ chmod 600 /path/to/id_rsa
```

On **Windows**, use the [PuTTY SSH client][2].

After logging in, you will see the command prompt:

```console

  ___   _____   _  _     ___                                           _     _
 |_ _| |_   _| | || |   |_ _|  _ __    _ __     ___   __   __   __ _  | |_  (_)   ___    _ __    ___
  | |    | |   | || |_   | |  | '_ \  | '_ \   / _ \  \ \ / /  / _` | | __| | |  / _ \  | '_ \  / __|
  | |    | |   |__   _|  | |  | | | | | | | | | (_) |  \ V /  | (_| | | |_  | | | (_) | | | | | \__ \
 |___|   |_|      |_|   |___| |_| |_| |_| |_|  \___/    \_/    \__,_|  \__| |_|  \___/  |_| |_| |___/

                                     http://www.it4i.cz/?lang=en

Last login: Tue Jul 9 15:57:38 2013 from your-host.example.com
[username@login2.cluster-name ~]$
```

!!! note
    The environment is **not** shared between login nodes, except for [shared filesystems][3].

## Data Transfer

Data in and out of the system may be transferred by SCP and SFTP protocols.

### Barbora Cluster

| Address                  | Port | Protocol |
| ------------------------- | ---- | ------- |
| barbora.it4i.cz           | 22   | SCP     |
| login1.barbora.it4i.cz    | 22   | SCP     |
| login2.barbora.it4i.cz    | 22   | SCP     |

### Salomon Cluster

| Address                | Port | Protocol  |
| ---------------------- | ---- | --------- |
| salomon.it4i.cz        | 22   | SCP, SFTP |
| login1.salomon.it4i.cz | 22   | SCP, SFTP |
| login2.salomon.it4i.cz | 22   | SCP, SFTP |
| login3.salomon.it4i.cz | 22   | SCP, SFTP |
| login4.salomon.it4i.cz | 22   | SCP, SFTP |

Authentication is by [private key][1] only.

!!! note
    If you experience degraded data transfer performance, consult your local network provider.

On Linux or Mac, use an SCP or SFTP client to transfer data to Barbora:

```console
$ scp -i /path/to/id_rsa my-local-file username@cluster-name.it4i.cz:directory/file
```

```console
$ scp -i /path/to/id_rsa -r my-local-dir username@cluster-name.it4i.cz:directory
```

or

```console
$ sftp -o IdentityFile=/path/to/id_rsa username@cluster-name.it4i.cz
```

A very convenient way to transfer files in and out of cluster is via the fuse filesystem [SSHFS][b].

```console
$ sshfs -o IdentityFile=/path/to/id_rsa username@cluster-name.it4i.cz:. mountpoint
```

Using SSHFS, the user's Barbora home directory will be mounted on your local computer, just like an external disk.

Learn more about SSH, SCP, and SSHFS by reading the manpages:

```console
$ man ssh
$ man scp
$ man sshfs
```

On Windows, use the [WinSCP client][c] to transfer data. The [win-sshfs client][d] provides a way to mount the cluster filesystems directly as an external disc.

More information about the shared file systems is available [here][4].

## Connection Restrictions

Outgoing connections from cluster login nodes to the outside world are restricted to the following ports:

| Port | Protocol |
| ---- | -------- |
| 22   | SSH      |
| 80   | HTTP     |
| 443  | HTTPS    |
| 873  | Rsync    |

!!! note
    Use **SSH port forwarding** and proxy servers to connect from cluster to all other remote ports.

Outgoing connections from cluster compute nodes are restricted to the internal network. Direct connections from compute nodes to the outside world are cut.

## Port Forwarding

### Port Forwarding From Login Nodes

!!! note
    Port forwarding allows an application running on cluster to connect to arbitrary remote hosts and ports.

It works by tunneling the connection from cluster back to the user's workstations and forwarding from the workstation to the remote host.

Select an unused port on the cluster login node (for example 6000) and establish the port forwarding:

```console
$ ssh -R 6000:remote.host.com:1234 cluster-name.it4i.cz
```

In this example, we establish port forwarding between port 6000 on the cluster and port 1234 on the `remote.host.com`. By accessing `localhost:6000` on the cluster, an application will see the response of `remote.host.com:1234`. The traffic will run via the user's local workstation.

Port forwarding may be done **using PuTTY** as well. On the PuTTY Configuration screen, load your cluster configuration first. Then go to *Connection > SSH > Tunnels* to set up the port forwarding. Click the _Remote_ radio button. Insert 6000 to the _Source port_ textbox. Insert `remote.host.com:1234`. Click _Add_, then _Open_.

Port forwarding may be established directly to the remote host. However, this requires that the user has an SSH access to `remote.host.com`.

```console
$ ssh -L 6000:localhost:1234 remote.host.com
```

!!! note
    Port number 6000 is chosen as an example only. Pick any free port.

### Port Forwarding From Compute Nodes

Remote port forwarding from compute nodes allows applications running on the compute nodes to access hosts outside the cluster.

First, establish the remote port forwarding from the login node, as [described above][5].

Second, invoke port forwarding from the compute node to the login node. Insert the following line into your jobscript or interactive shell:

```console
$ ssh  -TN -f -L 6000:localhost:6000 login1
```

In this example, we assume that port forwarding from `login1:6000` to `remote.host.com:1234` has been established beforehand. By accessing `localhost:6000`, an application running on a compute node will see the response of `remote.host.com:1234`.

### Using Proxy Servers

Port forwarding is static; each single port is mapped to a particular port on a remote host. Connection to another remote host requires a new forward.

!!! note
    Applications with inbuilt proxy support experience unlimited access to remote hosts via a single proxy server.

To establish a local proxy server on your workstation, install and run the SOCKS proxy server software. On Linux, SSHD demon provides the functionality. To establish the  SOCKS proxy server listening on port 1080 run:

```console
$ ssh -D 1080 localhost
```

On Windows, install and run the free, open source Sock Puppet server.

Once the proxy server is running, establish the SSH port forwarding from cluster to the proxy server, port 1080, exactly as [described above][5]:

```console
$ ssh -R 6000:localhost:1080 cluster-name.it4i.cz
```

Now, configure the applications proxy settings to `localhost:6000`. Use port forwarding to access the [proxy server from compute nodes][5], as well.

## Graphical User Interface

* The [X Window system][6] is the principal way to get a GUI access to the clusters.
* [Virtual Network Computing][7] is a graphical desktop-sharing system that uses a Remote Frame Buffer protocol to remotely control another computer.

## VPN Access

* Access IT4Innovations internal resources via [VPN][8].

[1]: ../general/accessing-the-clusters/shell-access-and-data-transfer/ssh-keys.md
[2]: ../general/accessing-the-clusters/shell-access-and-data-transfer/putty.md
[3]: ../anselm/storage.md#shared-filesystems
[4]: ../anselm/storage.md
[5]: #port-forwarding-from-login-nodes
[6]: ../general/accessing-the-clusters/graphical-user-interface/x-window-system.md
[7]: ../general/accessing-the-clusters/graphical-user-interface/vnc.md
[8]: ../general/accessing-the-clusters/vpn-access.md

[b]: http://linux.die.net/man/1/sshfs
[c]: http://winscp.net/eng/download.php
[d]: http://code.google.com/p/win-sshfs/