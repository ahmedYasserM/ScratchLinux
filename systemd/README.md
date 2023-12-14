# Systemd

**Systemd** is the most popular **initialization systems** (also refered to as **init** systems). It is the default init system for most major Linux distributions nowadays.

System initialization time is reduced because services are started in parallel.

## Runlevels

Runlevels are a concept from the old **SysV init** system. They are a way to group services together. For example, runlevel 3 is the default runlevel for servers and runlevel 5 is the default runlevel for desktops.

You can think of a runlevel as a preset of services that should be running (A state in which the operating system is running)

### SysV init runlevels

| Runlevel | Name                         | Description                                                                                                                                                                                 |
| -------- | ---------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 0        | **Halt**                     | 📌 All services are shut down and the system is powered off                                                                                                                                 |
| 1 or S   | **Single User Mode**         | 📌 The root account is automatically logged in to the system <br> 📌 Other users can't log in <br> 📌 Only the command line interface is available <br> 📌 Network services are not started |
| 2        | **Multi-User Mode**          | 📌 Users can log in to the system <br> 📌 Only the command line interface is available <br> 📌 Network services are not started                                                             |
| 3        | **Extended Multi-User Mode** | 📌 Users can log in to the system <br> 📌 Only the command line interface is available <br> 📌 Network services are started <br> 📌 Common runlevel for servers                             |
| 4        | **User Definded**            | 📌 Users can customize this runlevel                                                                                                                                                        |
| 5        | **Graphical Mode**           | 📌 Users can log in to the system <br> 📌 Command line and graphical user interfaces is available <br> 📌 Network services are started <br> 📌 Common runlevel for desktops                 |
| 6        | **Reboot**                   | 📌 All services are shut down and the system is rebooted                                                                                                                                    |

## Systemd Unit Types

A **unit** is a resource that the system knows how to manage, consisting of a **name**, **type** and **configuration file**.

| Unit Type | Description                                                                                                                                                                                                                                                                                     |
| --------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Service   | 📌 A process that runs in the background and does not require user input. <br> 📌 Started when the system boots and runs until the system is shut down. <br> 📌 Can be started, stopped, restarted, reloaded, enabled, disabled, masked, and unmasked. <br> 📌 Is defined by a `.service` file. |
| Target    | 📌 A group of other units. <br> 📌 Similar to a runlevel in SysV init. <br> 📌 can be started, stopped, enabled, disabled, and masked. <br> 📌 Is defined by a `.target` file.                                                                                                                  |
| Device    | 📌 A physical or virtual hardware device. <br> 📌 Started when the system boots and runs until the system is shut down. <br> 📌 Can be started, stopped, enabled, disabled, and masked. <br> 📌 Defined by a `.device` file.                                                                    |
| Mount     | 📌 A file system mount point. <br> 📌 Started when the system boots and runs until the system is shut down. <br> 📌 Can be started, stopped, enabled, disabled, and masked. <br> 📌 Defined by a `.mount` file.                                                                                 |
| Automount | 📌 A file system mount point that is automatically mounted when accessed. <br> 📌 Started when the system boots and runs until the system is shut down. <br> 📌 Can be started, stopped, enabled, disabled, and masked. <br> 📌 Defined by a `.automount` file.                                 |
| Path      | 📌 A file or directory in a file system. <br> 📌 Started when the system boots and runs until the system is shut down. <br> 📌 Can be started, stopped, enabled, disabled, and masked. <br> 📌 Defined by a `.path` file.                                                                       |
| Socket    | 📌 A communication endpoint. <br> 📌 Started when the system boots and runs until the system is shut down. <br> 📌 Can be started, stopped, enabled, disabled, and masked. <br> 📌 Defined by a `.socket` file.                                                                                 |
| Snapshot  | 📌 A saved state of the systemd manager configuration. <br> 📌 Not started when the system boots. <br> 📌 Can be started, stopped, enabled, disabled, and masked. <br> 📌 Defined by a `.snapshot` file.                                                                                        |

The Linux system unit configuration files are located in the following directories

1. `/etc/systemd/system `
2. `/usr/lib/systemd/system `
3. `/lib/systemd/system`

### Systemd Targets

**Runlevels** are called **Target Units** in **systemd**.

**Systemd** targets are similar to **SysV init** runlevels. They are a way to group services together. For example, the `multi-user.target` is the default target for servers and `graphical.target` is the default target for desktops.

| Target Unit          | Corresponding Runlevel      | Description                                                                                                                                                                                                                          |
| -------------------- | --------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **powerofftarget**   | analogous to runlevel **0** | 📌 Shuts down the system and powers off the machine <br> 📌 Similar to runlevel 0 in SysV init                                                                                                                                       |
| **rescuetarget**     | analogous to runlevel **1** | 📌 Starts the system in rescue mode <br> 📌 The root account is automatically logged in to the system <br> 📌 Other users can't log in <br> 📌 Only the command line interface is available <br> 📌 Network services are not started |
| **multi-usertarget** | analogous to runlevel **3** | 📌 Starts the system in multi-user mode <br> 📌 Users can log in to the system <br> 📌 Only the command line interface is available <br> 📌 Network services are started                                                             |
| **graphicaltarget**  | analogous to runlevel **5** | 📌 Starts the system in graphical mode <br> 📌 Users can log in to the system <br> 📌 Command line and graphical user interfaces are available <br> 📌 Network services are started                                                  |
| **reboottarget**     | analogous to runlevel **6** | 📌 Shuts down the system and reboots the machine                                                                                                                                                                                     |

### Default Target

The default target is the target that is started when the system boots. The default target is analogous to the runlevel that is started when the system boots.

The default target is defined by a symbolic link at `/etc/systemd/system/default.target`. The default target is a symbolic link to the target unit that should be started when the system boots.

> NOTE
>
> Systemd will search for files in the following directories in the order listed below. If a file is found in an earlier directory, the file in the later directories will be ignored.
> 1. `/etc/systemd/system`
> 3. `/usr/lib/systemd/system`


---

---

## Commands cheat sheet

| Command                                    | Usage                                                                                   |
| ------------------------------------------ | --------------------------------------------------------------------------------------- |
| `systemctl status <service>`               | 📌 Show status of service                                                               |
| `systemctl start <service>`                | 📌 Start service                                                                        |
| `systemctl stop <service>`                 | 📌 Stop service                                                                         |
| `systemctl restart <service>`              | 📌 Restart service                                                                      |
| `systemctl enable <service>`               | 📌 Enable service to start on boot                                                      |
| `systemctl disable <service>`              | 📌 Disable service to start on boot                                                     |
| `systemctl is-enabled <service>`           | 📌 Check if service is enabled                                                          |
| `systemctl is-active <service>`            | 📌 Check if service is active                                                           |
| `systemctl get-default`                    | 📌 Get default target (runlevel)                                                        |
| `systemctl set-default <target>`           | 📌 Set default target (runlevel)                                                        |
| `systemctl poweroff`                       | 📌 Shutdown system                                                                      |
| `systemctl reboot`                         | 📌 Reboot system                                                                        |
| `systemctl daemon-reload`                  | 📌 Reload systemd manager configuration                                                 |
| `systemctl list-units`                     | 📌 List all currently active units                                                      |
| `systemctl list-units --type=service`      | 📌 List all services                                                                    |
| `systemctl list-unit-files`                | 📌 List all unit files present on the system, whether or not they are currently active. |
| `systemctl list-unit-files --type=service` | 📌 List all service unit files                                                          |
| `systemctl suspend`                        | 📌 Suspend system                                                                       |
| `systemctl hibernate`                      | 📌 Hibernate system                                                                     |
| `systemctl hybrid-sleep`                   | 📌 Hibernate system if supported, otherwise suspend system                              |
| `systemctl mask <service>`                 | 📌 Mask service (disable service and create a symlink to `/dev/null`)                   |
| `systemctl unmask <service>`               | 📌 Unmask service                                                                       |
| `systemctl list-dependencies <service>`    | 📌 List dependencies of service                                                         |
