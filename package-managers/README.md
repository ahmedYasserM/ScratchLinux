## Package Managers

## Pacman

## Configuration Files

| File                       | Description                         |
| -------------------------- | ----------------------------------- |
| `/etc/pacman.conf`         | :pushpin: Pacman configuration file |
| `/etc/pacman.d/mirrorlist` | :pushpin: Pacman mirrorlist         |

### Pacman Cheatsheet

| Command                 | Description                                                                         |
| ----------------------- | ----------------------------------------------------------------------------------- |
| `pacman -S <package>`   | :pushpin: Install a package                                                         |
| `pacman -Sw <package>`  | :pushpin: Download a package without installing it                                  |
| `pacman -Sy`            | :pushpin: Update the package database                                               |
| `pacman -Syy`           | :pushpin: Force update the package database `even if you updated it recently`       |
| `pacman -Su`            | :pushpin: Update the system                                                         |
| `pacman -Syu`           | :pushpin: Update the package database and the system                                |
| `pacman -Q`             | :pushpin: List all installed packages `even if those you didn't install explicitly` |
| `pacman -Qe`            | :pushpin: List all `explicitly` installed packages                                  |
| `pacman -Qq`            | :pushpin: List all installed packages `only package names`             |
| `pacman -Qn` | :pushpin: List all installed packages from the `official repositories` |
| `pacman -Qm` | :pushpin: List all installed packages from the `AUR` |
| `pacman -Qs`            | :pushpin: List all installed packages with a description                            |
| `pacman -Ql`            | :pushpin: List all files installed by a package                                     |
| `pacman -Qd`            | :pushpin: List all dependencies of a package                                        |
| `pacman -Qdt`           | :pushpin: List all `orphaned` packages                                                |
| `pacman -F <file>`      | :pushpin: Search for a file in all packages                                         |
| `pacman -Ss <keyword>`  | :pushpin: Search for a package  that contains a specific keyword in the remote repositories |
| `pacman -R <package>`   | :pushpin: Remove a package                                                          |
| `pacman -Rs <package>`  | :pushpin: Remove a package and its dependencies                                     |
| `pacman -Rns <package>` | :pushpin: Remove a package and its dependencies and **system** configuration files  |
| `pacman -Sc`            | :pushpin: Remove old package versions from the cache                                |
