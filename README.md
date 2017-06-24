# bin
This repository contains a collection of scripts and related files that I am using on my Arch Linux installation. There
might be better ways to do some of the things I wrote these scripts for, or even already existing solutions I simply
didn't know about; if you think you know of either one please let me know.


## [aur-auto-vote](https://www.reddit.com/r/archlinux/comments/4ryh6t/aur_autovote/)
I really wanted to show my appreciation for the AUR packages that I am using, but am entirely too lazy to keep the list
of voted-for packages up-to-date manually.

```
$ aur-auto-vote --help
usage: aur-auto-vote [-h] [--ignore IGNORE] [--unvote-all] [--delay DELAY]
                     username

positional arguments:
  username

optional arguments:
  -h, --help            show this help message and exit
  --ignore IGNORE, -i IGNORE
                        Regex for packages that should not be voted. Can be
                        passed multiple times.
  --unvote-all, -u      Unvote all voted-for packages, all other arguments are
                        ignored.
  --delay DELAY, -d DELAY
                        Delay between voting actions (seconds).
```

When voting already voted-for packages will be automatically skipped. Local PKGBUILDs I usually prefix with my nick,
i.e. `cryzed-` so I pass in `--ignore 'cryzed-.*'`. If you feel that your voted-for packages are completely outdated,
consider using `--unvote-all` to remove all votes beforehand. It might be a good idea to specify a `--delay` > 0 to
prevent hammering the server.


## defaults
```
$ ./defaults --help
usage: defaults [-h] [--editor PATH] [--stdout] path

Inspect the original version of files belonging to installed packages.

If the editor is not specified using --editor, the environment variables EDIT
and VISUAL will be used; alternatively --stdout can be used to pipe the original
file's contents directly to stdout.

Files are searched for in packages located in the "CacheDir" directories specified
in /etc/pacman.conf (default: /var/cache/pacman/pkg/) and in the "PKGDEST"
directory specified in /etc/makepkg.conf, if defined. Defaults will only work
with foreign packages, if the "PKGDEST" directory is specified.

If the package can't be found in either, defaults attempt to download the latest
version of the package from the available pacman mirrors, however this only
works with native packages.

positional arguments:
  path

optional arguments:
  -h, --help     show this help message and exit
  --editor PATH
  --stdout
```

This is useful for me when editing backup (configuration)-files which are part of installed packages. Often they are
filled with comments and various examples configurations, however after figuring out my configuration I rarely want to
keep all these around.

Removing them to keep the file as clean as possible however, might be an issue when further modifications are needed at
some later point in time -- all the reference examples are now missing, forcing you to either read the man page (even
for trivial changes) or manually hunt down the package in your cache or online and checking out the original file.

This script aims to save you these steps: simply run it with a path to a file, and the local, as well as the original
file, should both be opened in the specified editor.


## hotstrings
```
$ hotstrings --help
usage: hotstrings [-h] [path]

positional arguments:
  path        Path to JSON file containing hotstring definitions

optional arguments:
  -h, --help  show this help message and exit
```

This script is a much lighter version of AutoKey, specifically the
[AutoKey-py3](https://aur.archlinux.org/packages/autokey-py3/) fork. Since there was a recent update to the official
[python-xlib](https://github.com/python-xlib/python-xlib) which breaks compatibility with the fork, and the fork also
doesn't seem to be actively maintained anymore, I wanted to preemptively find another solution before AutoKey-py3
eventually stops working entirely on my system.

This pretty much implements only the functionality I actually use: replacing hotstrings and running commands; basically
you type text and it is either replaced by the given replacement string or a specified command is run (optionally
replacing the hotstring with its stdout output). Dependencies are Python 3 and the the official python-xlib or
[LiuLang's fork](https://github.com/LiuLang/python3-xlib) which is used by AutoKey-py3.

An example configuration file might look like this:
```
$ cat ~/.config/hotstrings.json 
{
    "first": ["replace", "replacement 1"],
    "second": ["replace", "replacement 2"],
    "third": ["run", "sh", "-c", "touch ~/Desktop/hello_world.txt"],
    "fourth": ["run-replace", "date"],

    // doesn't strip whitespace at the beginning and end of the output
    "five": ["run-replace-raw", "date"]
}
```


## restart-plasmashell
Sometimes the KDE Plasma shell starts displaying my wallpaper strangely (i.e. not at all) towards the bottom of my
screen. When that happens I simply run this script to quickly restart the shell.


## vpn-whitelist-domain
I am using NetworkManager and the NetworkManager-OpenVPN plugin. When connecting to my VPN provider, NetworkManager
creates a virtual tunnel-device through which all traffic is routed by setting the route metric lower than the metric
of my default gateway.

Some sites and services unfortunately have simply blocked or banned my VPN's IP address, so for some domains it is
useful to bypass the VPN tunnel entirely. That is what this script does: it finds the first default gateway that isn't a
tunnel device, resolves the passed domain to all possible IPs and then adds explicit routes for each of them through the
discovered gateway.

```
Usage:
    vpn-whitelist-domain [SWITCHES] domain

Meta-switches
    -h, --help         Prints this help message and quits
    --help-all         Print help messages of all subcommands and quit
    -v, --version      Prints the program's version and quits

Switches
    -r, --remove       Remove domain from whitelist
```


## backup-system
These are some small systemd service skeletons that use borg and environment variables in `/etc/backup-system.conf` to
allow daily system backups. To customize the service run `# systemctl edit backup-system` and modify the
`[Service]`-section accordingly.
