# snap-sync

## About

This bash script sends incremental snapshots to another drive for backing up
data. Plug in and mount any btrfs-formatted device you want your system to be
backed up to (like a USB drive).  When you run the script you will be prompted
to select a mounted btrfs device.

The script iterates through all snapper configurations. For each configuration
it creates a new local snapshot. If you have never synced to the specified
device you will be prompted to enter a directory on the device where the backup
snapshots will go. Additionally you are shown the location of the backed up
snapshot. If you have performed a backup to this device before, only the changes
since the last backup have to be sent.

## Requirements

snapper is required.

## Example output

    # snap-sync

    Selected a mounted BTRFS device to backup to.
    1) 43cedfb6-8775-43be-8abc-ee63bb92e10e (/)
    2) 43cedfb6-8775-43be-8abc-ee63bb92e10e (/.snapshots)
    3) 43cedfb6-8775-43be-8abc-ee63bb92e10e (/home)
    4) 7360922b-c916-4d9f-a670-67fe0b91143c (/run/media/wes/backup)
    0) Exit
    Enter a number: 4
    You selected the disk with UUID 7360922b-c916-4d9f-a670-67fe0b91143c.
    At 'home' configuration
    Backup location: /run/media/wes/backup/acer-c720/home/1097/
    Continue (y/n)? y
    At subvol /home/.snapshots/1097/snapshot
    At 'root' configuration
    Backup location: /run/media/wes/backup/acer-c720/root/2288/
    Continue (y/n)? y
    At subvol //.snapshots/2288/snapshot
    Done!

The related snapshots from this on the local machine are for `home`:

    single | 1097 |       | Sat 01 Oct 2016 07:48:40 AM CDT | root |          | latest incremental backup | backupdir=acer-c720, uuid=7360922b-c916-4d9f-a670-67fe0b91143c

and for `root`:

    single | 2288 |       | Sat 01 Oct 2016 07:50:56 AM CDT | root |          | latest incremental backup | backupdir=acer-c720, uuid=7360922b-c916-4d9f-a670-67fe0b91143c

As you can see the userdata column for snapper is used to keep track of these
snapshots for the next time the script is run so that only the changes will need
to be sent.
