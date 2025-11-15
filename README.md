# MariaDB in Android

MariaDB in Android with Termux Application 

## Requirements

- **Termux**: [Termux APK (v0.118.3)](https://github.com/termux/termux-app/releases/download/v0.118.3/termux-app_v0.118.3+github-debug_universal.apk)
- Good internet connection
- Minimum of 1GB storage space

## Installation

1. Download and install the Termux APK from the link above (open the APK on your device to install)
2. Open the Termux application
3. Update Termux packages :

```bash
pkg update -y && yes | pkg upgrade -y
```

4. Wait for the package installation to complete
5. Copy and paste this command in the terminal:

```bash
pkg install mariadb -y
mariadb-install-db
mysqld_safe &
```

The MariaDB server should now be running in the background

6. Press Enter and you should be able to connect using the command: 

```bash
mysql -u root
```

## Usage

### Connect to MariaDB
```bash
# Connect to MariaDB
mysql -u root
```

### Check if MariaDB is Running (Optional)
```bash
ps aux | grep mysqld
```

If the output shows:
```
/data/data/com.termux/files/usr/bin/sh /data/data/com.termux/files/usr/bin/mysqld_safe
```
Then MariaDB is running.

### To Stop MariaDB
```bash
pkill -9 mysqld
     #or
pkill -9 mysqld_safe
     #or
pkill -9 mariadbd
```

### Exit MariaDB
```bash
# From inside MariaDB prompt
EXIT;
# or
QUIT;
```

### Exit Termux
```bash
# Option 1: Type exit command
exit

# Option 2: Close the Termux app (swipe it away or press back button)
```

If notification permissions are allowed in Termux, you can also:
```
# Option 3: Swipe down the notification bar and tap the close button on the Termux notification
```

## Troubleshooting

### Issue: "Can't connect to local MySQL server through socket"
**Solution:** Start the MariaDB server first:
```bash
mysqld_safe &
```
Then wait a few seconds before connecting.

### Issue: "Port 3306 is already in use"
**Solution:** Stop any existing MariaDB processes:
```bash
pkill -9 mysqld
pkill -9 mysqld_safe
pkill -9 mariadbd
```
Then restart with `mysqld_safe &`

### Issue: "Permission denied" or "Access denied for user 'root'"
**Solution:** MariaDB in Termux runs without a password by default. Connect with:
```bash
mysql -u root
```

### Issue: MariaDB server won't start
**Solution:** Check if the data directory is corrupted. Reinitialize it:
```bash
rm -rf $PREFIX/var/lib/mysql
mariadb-install-db
mysqld_safe &
```

## Uninstall

To completely remove MariaDB from Termux:

```bash
# Stop MariaDB server
pkill mysqld

# Remove MariaDB package
pkg remove mariadb -y

# Remove MariaDB data directory (optional, if you want to clean up completely)
rm -rf $PREFIX/var/lib/mysql
rm -rf $PREFIX/etc/mysql
```

## Security Warning ⚠️

**Important:** By default, MariaDB in Termux is installed without a password for the root user. This means:
- Anyone with access to your device can connect to and modify your databases
- **Do NOT use this in production environments**
- This is for development/testing purposes only on personal devices

## References & Resources

- [MariaDB Official Documentation](https://mariadb.com/docs/)
- [Termux Official Wiki](https://wiki.termux.com/)
- [Termux Packages](https://packages.termux.org/)
- [MariaDB in Termux Guide](https://wiki.termux.com/wiki/Databases)

## Notes
This is my first time creating something like this. If you encounter any issues or have suggestions for improvement, please feel free to open an issue or reach out with your feedback.
