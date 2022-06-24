# Accounting / Auditing
- Process accounting provides information about connect times (for logins) and command execution via a set of utilities that report aspects of collected data. It can be used for various purposes, including security.
- By default, process accounting data is stored in /var/account/pacct. When each process terminates, a record with information about the process is written to the accounting file. This file exists after system installation (empty) and is available for use when process accounting is enabled. 
- The /var/account/pacct (or alternative if specified) and /var/log/wtmp files should be monitored for space usage, as they can get very large. The pacct file is rotated once per day 31 times before being deleted. Rotated files are compressed (see /etc/logrotate.d/psacct and the logrotate(8) man page for details).

# Package
psacct
# Commands
⦁	accton - Turns process accounting on/off
⦁	Alternatively, the psacct service can be started, to turn on process accounting
⦁	ac - provides connection time statistics
⦁	lastcomm - Provides information about previously executed commands
⦁	sa - Summarizes information about previously executed commands
⦁	dump-acct - Provides human-readable output of select process accounting file data
⦁	dump-utmp - Provides human-readable output of the utmp or wtmp file

## SBS: Get last login,reboot and current logins
	who cmd read from /var/run/utmp
	last cmd read from /var/log/wtmp
## SBS: Rotate manually /var/log/wtmp
	mkdir /var/log/backup
	mv /var/log/wtmp /var/log/backup
	dump-acct /var/log/backup/wtmp

## SBS: Turn on process accounting 
	touch /var/account/pacct (by default exists; unless you wants dfferent location)
	chmod 600 /var/account/pacct 
	accton on
	login as abu and touch /tmp/file1; vi /tmp/file2; rm /tmp/file1; exit
	dump-acct /var/account/pacct
	lastcomm abu
	lastcomm --debug
	systemctl acct on
## Refer to man pages and acct.h header file:
	man 5 acct
	man 1 lastcomm
	man 2 acct
	man 2 execve
	man 8 sa
	man 1 accton
	/usr/include/linux/acct.h
	/usr/include/sys/acct.h
