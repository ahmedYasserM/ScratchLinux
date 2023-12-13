# Systemd

## Commands cheat sheet

| Command                                 | Usage                                                              |
| --------------------------------------- | ------------------------------------------------------------------ |
| `systemctl status <service>`            | show status of service                                             |
| `systemctl start <service>`             | start service                                                      |
| `systemctl stop <service>`              | stop service                                                       |
| `systemctl restart <service>`           | restart service                                                    |
| `systemctl enable <service>`            | enable service to start on boot                                    |
| `systemctl disable <service>`           | disable service to start on boot                                   |
| `systemctl is-enabled <service>`        | check if service is enabled                                        |
| `systemctl is-active <service>`         | check if service is active                                         |
| `systemctl daemon-reload`               | reload systemd manager configuration                               |
| `systemctl list-units --type=service`   | list all services                                                  |
| `systemctl poweroff`                    | shutdown system                                                    |
| `systemctl reboot`                      | reboot system                                                      |
| `systemctl suspend`                     | suspend system                                                     |
| `systemctl hibernate`                   | hibernate system                                                   |
| `systemctl hybrid-sleep`                | hibernate system if supported, otherwise suspend system            |
| `systemctl mask <service>`              | mask service (disable service and create a symlink to `/dev/null`) |
| `systemctl unmask <service>`            | unmask service                                                     |
| `systemctl list-dependencies <service>` | list dependencies of service                                       |
