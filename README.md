# Template for logrotate

## Location

Global rules are stored in `/etc/logrotate.conf`.

Specific rules are stored in the `/etc/logrotate.d` folder.

## Some attributes

For each file, they are attributes who define how logrorate will behave.

- Log files are rotated once each weekday or each month
  - 0 means Sunday, 1 means Monday, ..., 6 means Saturday

```text
weekly <0-6>
```

- Log files can be also rotated once each month

```text
monthly
```

- Log files are rotated count times before being removed or mailed

```text
rotate <count>
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

## My approach

This is my logrotate approach on my server:

- logrotate of all log files -> Monday

It must keep one month of archived logs for each service
