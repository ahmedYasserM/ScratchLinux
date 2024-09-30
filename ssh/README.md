# SSH

## Connection

### Connect to Remote Server

```bash
ssh user@host-ip
```

### Connect to Remote Server with Port Number

```bash
ssh -p port user@host-ip
```

### Connect to Remote Server with Private Key

```bash
ssh -i path/to/private-key user@host-ip
```

> By default, SSH searches for id_rsa, id_ecdsa, id_ecdsa_sk, id_ed25519, id_ed25519_sk, and id_dsa files. The keys do not have to be named like this, you can name it mykey just as well, or even place it in a different directory. However, if you do either of those, then you need to explicitly reference the key in the ssh command

## Configure SSH Client

### Create SSH Config File

```bash
touch ~/.ssh/config
```

> This file is for user-specific configuration. You can also create a system-wide configuration file at `/etc/ssh/ssh_config`.

### Add Configuration

```bash
Host host-alias
    HostName host-ip
    User user
    Port port
    IdentityFile path/to/private-key
```

### Connect to Remote Server with Configuration

```bash
ssh host-alias
```

## Key Generation

### Generate RSA Key

```bash
ssh-keygen -t rsa  -C "Your Comment"
```

### Generate ed25519 Key (Recommended)

```bash
ssh-keygen -t ed25519 -C "Your Comment"
```

## Add Public Key to Remote Server

### Copy Public Key to Remote Server

```bash
ssh-copy-id user@host-ip
```

> This command will copy the public key to the remote server and add it to the authorized_keys file.

## SSH Agent

- SSH agent is a program that runs in the background and stores your private keys. When you use SSH to connect to a server, the SSH agent will automatically use the correct private key to authenticate you.
- The passphrase is only required once when you add the key to the agent.
- If you are using graphical desktop environment, the SSH agent is started automatically when you log in. If you are using a terminal, you need to start the SSH agent manually.

### Start SSH Agent

```bash
eval $(ssh-agent -s) # for bash, zsh
eval $(ssh-agent -c) # for fish
```

> This will persist the SSH agent in the terminal session. If you close the terminal, the agent will be closed as well.

### Add SSH Key to SSH Agent

```bash
ssh-add path/to/private-key
```

> This will add the private key to the SSH agent. You will be prompted to enter the passphrase of the key.

## Configure SSH Server

- The ssh server is represented by the `sshd` service.

- The configuration file for the ssh server is located at `/etc/ssh/sshd_config`.

- Some options you can configure are:
  | Option | Description |
  | --- | --- |
  | Port | The port the ssh server listens on. |
  | PermitRootLogin | Allow or disallow root login. |
  | PasswordAuthentication | Allow or disallow password authentication. (Check any included files also) |


> After changing the configuration file, you need to restart the ssh server for the changes to take effect.

