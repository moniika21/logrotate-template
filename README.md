# Template for logrotate

## Location

Global rules are stored in `/etc/logrotate.conf`.

Specific rules are stored in the `/etc/logrotate.d` folder.

## Some attributes

For each file, they are attributes who define how logrorate will behave.

- Log files are rotated count times before being removed or mailed

```text
rotate <count>
```

- Log files are rotated once each weekday
  - 0 means Sunday, 1 means Monday, ..., 6 means Saturday

```text
weekly <0-6>
```

- Log files are rotated once each month

```text
monthly
```

- Old versions of log files are compressed

```text
compress
```

- Do not rotate if empty

```text
notifempty
```

- Postpone compression to the next rotation cycle

```text
delaycompress
```

- If the log file is missing, go on to the next one without issuing an error message

```text
missingok
```

- The script is executed after the log file is rotated

```text
postrotate
    <script_or_command>
endscript
```

- Immediately after rotation (before the postrotate script is run) the log file is created (with the same name as the log  file just rotated)
  - `mode` specifies the mode for the log file in octal
  - `owner` specifies the user who will own the log
file.
  - `group` specifies the group the log file will belong to

```text
create <mode> <owner> <group>
```

## Docker logrotate

Each docker image creator have is own approach, you'll maybe have to logrotate yourself the generated logs.

Or like [nginx-proxy-manager](https://github.com/NginxProxyManager/nginx-proxy-manager/blob/develop/docker/rootfs/etc/logrotate.d/nginx-proxy-manager) it may be done automatically.

## My approach

This is my logrotate approach on my server:

- logrotate of all log files -> Monday

It must keep one month of archived logs for each service
