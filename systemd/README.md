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

| Unit Type | Description                                                                                                                                                                                                       |
| --------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Service   | 📌 A process that runs in the background and does not require user input. <br> 📌 Can be started, stopped, restarted, reloaded, enabled, disabled, masked, and unmasked. <br> 📌 Is defined by a `.service` file. |
| Target    | 📌 A group of other units. <br> 📌 Similar to a runlevel in SysV init. <br> 📌 can be started, stopped, enabled, disabled, and masked. <br> 📌 Is defined by a `.target` file.                                    |
| Device    | 📌 A physical or virtual hardware device. <br> 📌 Can be started, stopped, enabled, disabled, and masked. <br> 📌 Defined by a `.device` file.                                                                    |
| Mount     | 📌 A file system mount point. <br> 📌 Can be started, stopped, enabled, disabled, and masked. <br> 📌 Defined by a `.mount` file.                                                                                 |
| Automount | 📌 A file system mount point that is automatically mounted when accessed. <br> 📌 Can be started, stopped, enabled, disabled, and masked. <br> 📌 Defined by a `.automount` file.                                 |
| Path      | 📌 A file or directory in a file system. <br> 📌 Can be started, stopped, enabled, disabled, and masked. <br> 📌 Defined by a `.path` file.                                                                       |
| Socket    | 📌 A communication endpoint. <br> 📌 Can be started, stopped, enabled, disabled, and masked. <br> 📌 Defined by a `.socket` file.                                                                                 |
| Snapshot  | 📌 A saved state of the systemd manager configuration. <br> 📌 Not started when the system boots. <br> 📌 Can be started, stopped, enabled, disabled, and masked. <br> 📌 Defined by a `.snapshot` file.          |

The Linux system unit configuration files are located in the following directories

1. `/etc/systemd/system `
2. `/usr/lib/systemd/system `
3. `/lib/systemd/system`

### Systemd Targets

**Runlevels** are called **Target Units** in **systemd**.

**Systemd** targets are similar to **SysV init** runlevels. They are a way to group services together. For example, the `multi-user.target` is the default target for servers and `graphical.target` is the default target for desktops.

| Target Unit           | Corresponding Runlevel      | Description                                                                                                                                                                                                                          |
| --------------------- | --------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **poweroff.target**   | analogous to runlevel **0** | 📌 Shuts down the system and powers off the machine <br> 📌 Similar to runlevel 0 in SysV init                                                                                                                                       |
| **rescue.target**     | analogous to runlevel **1** | 📌 Starts the system in rescue mode <br> 📌 The root account is automatically logged in to the system <br> 📌 Other users can't log in <br> 📌 Only the command line interface is available <br> 📌 Network services are not started |
| **multi-user.target** | analogous to runlevel **3** | 📌 Starts the system in multi-user mode <br> 📌 Users can log in to the system <br> 📌 Only the command line interface is available <br> 📌 Network services are started                                                             |
| **graphical.target**  | analogous to runlevel **5** | 📌 Starts the system in graphical mode <br> 📌 Users can log in to the system <br> 📌 Command line and graphical user interfaces are available <br> 📌 Network services are started                                                  |
| **reboot.target**     | analogous to runlevel **6** | 📌 Shuts down the system and reboots the machine                                                                                                                                                                                     |

### Default Target

The default target is the target that is started when the system boots. The default target is analogous to the runlevel that is started when the system boots.

The default target is defined by a symbolic link at `/etc/systemd/system/default.target`. The default target is a symbolic link to the target unit that should be started when the system boots.

> NOTE
>
> Systemd will search for files in the following directories in the order listed below. If a file is found in an earlier directory, the file in the later directories will be ignored.
>
> 1. `/etc/systemd/system`
> 2. `/usr/lib/systemd/system`

## Systemd Unit Files

**Systemd** uses **unit files** to describe units. Unit files are located in the `/etc/systemd/system` directory and the `/usr/lib/systemd/system` directory.

**Systemd** unit files are written in the **INI** format. They consist of **sections** and **key-value pairs**.

### Sections

**Systemd** unit files consist of the following sections

| Section     | Description                                                                                                              |
| ----------- | ------------------------------------------------------------------------------------------------------------------------ |
| `[Unit]`    | 📌 General information about the unit <br> 📌 Contains directives that apply to the unit as a whole                      |
| `[Service]` | 📌 Information about the service <br> 📌 Contains directives that apply to the service                                   |
| `[Install]` | 📌 Information about the installation of the unit <br> 📌 Contains directives that apply to the installation of the unit |

### Directives

**Directives** are **key-value pairs** that are used to configure the unit.

**Systemd** unit files consist of the following directives

| Directive         | Description                                                                                                                                                                                                                                                                                                           |
| ----------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `Description`     | 📌 A human-readable description of the unit                                                                                                                                                                                                                                                                           |
| `Documentation`   | 📌 A list of URIs to documentation about the unit                                                                                                                                                                                                                                                                     |
| `Requires`        | 📌 A list of units that must be started before the unit is started <br> 📌 If any of the units listed in the `Requires` directive fail to start, the unit will fail to start                                                                                                                                          |
| `Wants`           | 📌 A list of units that should be started before the unit is started <br> 📌 If any of the units listed in the `Wants` directive fail to start, the unit will still start                                                                                                                                             |
| `wantedBy`        | 📌 Specifies which target unit should include or "want" the current unit                                                                                                                                                                                                                                              |
| `Conflicts`       | 📌 A list of units that must not be started when the unit is started <br> 📌 If any of the units listed in the `Conflicts` directive are started, the unit will fail to start                                                                                                                                         |
| `Before`          | 📌 A list of units that must be started before the unit is started <br> 📌 If any of the units listed in the `Before` directive fail to start, the unit will fail to start                                                                                                                                            |
| `After`           | 📌 Is used to specify the units that should be started before the current unit <br> 📌 It does not start the specified units but affects the order in which units are activated                                                                                                                                       |
| `OnFailure`       | 📌 A list of units that must be started when the unit fails to start <br> 📌 If any of the units listed in the `OnFailure` directive fail to start, the unit will still fail to start                                                                                                                                 |
| `ExecStart`       | 📌 The command to execute to start the unit <br> 📌 Can be a path to an executable file or a shell command <br> 📌 Can be specified multiple times <br> 📌 If the command is a path to an executable file, the file must be executable <br> 📌 If the command is a shell command, the command must be quoted          |
| `ExecStop`        | 📌 The command to execute to stop the unit <br> 📌 Can be a path to an executable file or a shell command <br> 📌 Can be specified multiple times <br> 📌 If the command is a path to an executable file, the file must be executable <br> 📌 If the command is a shell command, the command must be quoted           |
| `ExecReload`      | 📌 The command to execute to reload the unit <br> 📌 Can be a path to an executable file or a shell command <br> 📌 Can be specified multiple times <br> 📌 If the command is a path to an executable file, the file must be executable <br> 📌 If the command is a shell command, the command must be quoted         |
| `ExecStartPost`   | 📌 The command to execute after the unit is started <br> 📌 Can be a path to an executable file or a shell command <br> 📌 Can be specified multiple times <br> 📌 If the command is a path to an executable file, the file must be executable <br> 📌 If the command is a shell command, the command must be quoted  |
| `Restart`         | 📌 Specifies when the unit should be restarted <br> 📌 Can be set to `no`, `on-success`, `on-failure`, `on-abnormal`, `on-abort`, `on-watchdog`, or `always` <br> 📌 Defaults to `no`                                                                                                                                 |
| `TimeoutSec`      | 📌 Specifies the amount of time to wait before considering the unit to have failed to start or stop <br> 📌 Defaults to `DefaultTimeoutStartSec`                                                                                                                                                                      |
| `RemainAfterExit` | 📌 Specifies whether the unit should be considered active after the unit has finished executing <br> 📌 Can be set to `yes` or `no` <br> 📌 Defaults to `no`                                                                                                                                                          |
| `Alias`          | 📌 Systemd creates a symbolic link from the target unit names listed to this unit

for detaild information you can check [systemd.unit manpage](https://www.freedesktop.org/software/systemd/man/latest/systemd.unit.html#AllowIsolate=)

### Example

```ini
[Unit]
Description=Apache Web Server

[Service]
ExecStart=/usr/sbin/httpd
ExecReload=/usr/sbin/httpd -k graceful
ExecStop=/usr/sbin/httpd -k graceful-stop
Type=notify
NotifyAccess=all
Restart=on-failure
RestartSec=5s

[Install]
WantedBy=multi-user.target
```

---

---

## Commands cheat sheet

| Command                          | Usage                                                                 |
| -------------------------------- | --------------------------------------------------------------------- |
| `systemctl status <service>`     | 📌 Show status of service                                             |
| `systemctl start <service>`      | 📌 Start service                                                      |
| `systemctl stop <service>`       | 📌 Stop service                                                       |
| `systemctl restart <service>`    | 📌 Restart service                                                    |
| `systemctl enable <service>`     | 📌 Enable service to start on boot                                    |
| `systemctl disable <service>`    | 📌 Disable service to start on boot                                   |
| `systemctl is-enabled <service>` | 📌 Check if service is enabled                                        |
| `systemctl is-active <service>`  | 📌 Check if service is active                                         |
| `systemctl hybrid-sleep`         | 📌 Hibernate system if supported, otherwise suspend system            |
| `systemctl mask <service>`       | 📌 Mask service (disable service and create a symlink to `/dev/null`) |
| `systemctl unmask <service>`     | 📌 Unmask service                                                     |
| `systemctl list-dependenc ies <service>`   | 📌 List dependencies of service                                                         |
|`systemctl list-units --type=service`     | 📌 List all services                                                                    |
|`systemctl list-unit-files`               | 📌 List all unit files present on the system, whether or not they are currently active. <br> 📌 Unit status can be either **static**, **enabled** or **disabled** <br> 📌 **enabled** - means that the unit is currently enabled <br> 📌 **disabled** - means that the unit is currently disabled <br> 📌 **static** - refers to **statically enabled** and means that the unit is enabled by default and can not be disabled, even by **root** |
|`systemctl list-unit-files --type=service`| 📌 List all service unit files                                                          |
|`systemctl poweroff`                      | 📌 Shutdown system                                                                      |
|`systemctl reboot`                        | 📌 Reboot system                                                                        |
|`systemctl daemon-reload`                 | 📌 Reload systemd manager configuration                                                 |
|`systemctl list-units`                    | 📌 List all currently active units                                                      |
|`systemctl suspend`                       | 📌 Suspend system                                                                       |
|`systemctl hibernate`                     | 📌 Hibernate system                                                                     |
|`systemctl get-default`                   | 📌 Get default target (runlevel)                                                        |
|`systemctl set-default <target>`          | 📌 Set default target (runlevel)                                                        |
|`runlevel`                                | 📌 Get current runlevel                                                                 |
|`systemctl isolate <target>`                | 📌 Change to specified target (runlevel)                                                |
|`systemctl show <unit> `| 📌 Show properties of unit                                                              |
|`systemctl show --property <property> <unit>` | 📌 Show value of property of unit                                                       |
|`systemctl cat <unit>`                    | 📌 Show unit file                                                                       |
|`systemctl edit <unit>`                   | 📌 Edit unit file                                                                       |
|`systemctl kill <unit>`                   | 📌 Send **default SIGTERM** signal to unit                                              |
|`systemctl kill -s <signal> <unit>` | 📌 Send signal to unit |
