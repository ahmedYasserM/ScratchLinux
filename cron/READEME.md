

## Crontab

Crontab is a time-based job scheduler in Unix-like computer operating systems. Users that set up and maintain software environments use cron to schedule jobs (commands or shell scripts) to run periodically at fixed times, dates, or intervals. It typically automates system maintenance or administration—though its general-purpose nature makes it useful for things like connecting to the Internet and downloading email at regular intervals. The name is derived from the Greek word for time, χρόνος (chronos).


## Crontab file

The crontab file is a simple text file that contains a list of commands meant to be run at specified times. It is edited using the crontab command. The commands in the crontab file (and their run times) are checked by the cron daemon, which executes them in the system background. Each user can have their own crontab file, and though these are files in /var, they are not intended to be edited directly.


## Crontab commands

The following commands allow you to create, edit, list, and remove crontab files.

| Command | Description |
| --- | --- |
| `crontab -e` | :pushpin: Edit your crontab file, or create one if it doesn't already exist. |
| `crontab -l` | :pushpin: Display your crontab file. |
| `crontab -r` | :pushpin: Remove your crontab file. |
| `crontab -i` | :pushpin: Remove your crontab file with a prompt before removal. |
| `crontab -u` | :pushpin: Modify the crontab file of the specified user. |
| `crontab -l -u` | :pushpin: Display the crontab file of the specified user. |
| `crontab -r -u` | :pushpin: Remove the crontab file of the specified user. |
| `crontab -i -u` | :pushpin: Remove the crontab file of the specified user with a prompt before removal. |

The crontab file is parsed by cron, and is not affected by the environment of the calling shell. This is a common source of errors. If you are unsure of a command's full path, you can use the which command to get the full path of the command. For example, to get the full path of the command ls, you would run which ls.


## Crontab format

The crontab file has six fields for specifying minute, hour, day of month, month, day of week, and the command to be run at that interval. A single space is used to separate the fields. The format of a crontab file is as follows:

```shell
* * * * * command to be executed
- - - - -
| | | | |
| | | | ----- Day of week (0 - 7) (Sunday=0 or 7)
| | | ------- Month (1 - 12)
| | --------- Day of month (1 - 31)
| ----------- Hour (0 - 23)
------------- Minute (0 - 59)
```

The asterisk (*) is used to specify all possible values for a field. For example, an asterisk in the hour time field would be equivalent to every hour or an asterisk in the day of the week field would be equivalent to every day. The comma (,) is used to specify a list of values. For example, using 1,3,4 in the month field would mean January, March, and April. The dash (-) is used to specify a range of values. For example, 1-6 in the day of the week field would mean the first to the sixth day of the week. The slash (/) is used to specify a step value. For example, */5 in the hour field would mean every 5 hours.


## Crontab examples

The following are some examples of crontab entries:

```shell

# Run the command at 4am every week on Sunday

0 4 * * 0 command

# Run the command at 4am on the 1st of every month

0 4 1 * * command

# Run the command every 10 minutes

*/10 * * * * command

# Run the command every hour

0 * * * * command

# Run the command every day at 4:30am

30 4 * * * command

# Run the command every 5 minutes on weekdays

*/5 * * * 1-5 command

# Run the command every 5 minutes on weekends

*/5 * * * 0,6 command

# Run the command every 5 minutes on weekdays during working hours

*/5 9-17 * * 1-5 command

# Run the command every 5 minutes on weekdays during working hours and log the output

*/5 9-17 * * 1-5 command >> /var/log/command.log 2>&1

```

The last example shows how to redirect the output of the command to a log file. The `2>&1` at the end of the command redirects both standard output and standard error to the file. This is useful for capturing errors and debugging.


## Crontab shortcuts

```shell
@hourly command
0 * * * * command

@daily command
0 0 * * * command

@weekly command
0 0 * * 0 command

@monthly command
0 0 1 * * command

@yearly command
0 0 1 1 * command

@reboot command
```

## Crontab environment

The cron daemon runs with a limited environment, which means that certain environment variables need to be set for the cron commands to work as expected. The following environment variables are often used in crontab files:

| Variable | Description |
| --- | --- |
| `MAILTO` | :pushpin: The email address to send the output of the cron job to. |
| `PATH` | :pushpin: The search path for the cron job. |
| `HOME` | :pushpin: The home directory for the cron job. |
| `SHELL` | :pushpin: The shell to run the cron job in. |

The `MAILTO` variable is used to specify the email address to send the output of the cron job to. By default, the output of a cron job is emailed to the user that runs the job. The `MAILTO` variable can be set to another email address to send the output to a different address. For example, to send the output to the email address 
    
```shell
MAILTO="
```
    





The `PATH` variable is used to specify the search path for the cron job. By default, the search path is `/usr/bin:/bin`. The `PATH` variable can be set to a different search path to run the cron job with a different set of environment variables. For example, to set the search path to `/usr/local/bin:/usr/bin:/bin`, you would add the following line to the crontab file:

```shell
PATH="/usr/local/bin:/usr/bin:/bin"
```


The `HOME` variable is used to specify the home directory for the cron job. By default, the home directory is the user's home directory. The `HOME` variable can be set to a different home directory to run the cron job with a different home directory. For example, to set the home directory to `/var/www`, you would add the following line to the crontab file:

```shell
HOME="/var/www"
```

The `SHELL` variable is used to specify the shell to run the cron job in. By default, the shell is `/bin/sh`. The `SHELL` variable can be set to a different shell to run the cron job with a different shell. For example, to set the shell to `/bin/bash`, you would add the following line to the crontab file:

```shell
SHELL="/bin/bash"
```










