# bin
This repository contains a collection of scripts and related files that I am using on my Arch Linux installation. There
might be better ways to do some of the things I wrote these scripts for, or even already existing solutions I simply
didn't know about; if you think you know of either one please let me know.


## keep-process-alive
Unfortunately KRunner seems pretty unstable for me and crashes sometimes without any discernible reason. Manually
restarting it is a pain, so I came up with this.

```
Usage:
    keep-process-alive [SWITCHES] name

Meta-switches
    -h, --help                                 Prints this help message and quits
    --help-all                                 Print help messages of all subcommands and quit
    -v, --version                              Prints the program's version and quits

Switches
    --argument, -a VALUE:str                   Pass argument to process when (re)started; may be given multiple times
    --check-zombie-interval, -i VALUE:int      Seconds between checking if the process has become a zombie; the default is 3
```

If a process with the same name already exists it will be monitored and the arguments that the existing instance were
run with, will be used to restart the process when needed, otherwise the path to the executable will be determined using
`which` and started with any passed arguments.

If the process should become a zombie, it will be terminated using the `TERM` signal and restarted. If the process
terminates for whatever reason it will be restarted.


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


## warm-up-dns-resolver
I am using Unbound with DNSSEC enabled. The resolving of an uncached domain takes quite a bit of time because of that,
and most domains have a low TTL or even a TTL of 0 set which disables caching in Unbound completely. Naturally this is
a bit annoying, so I wrote this script.

```
Usage:
    warm-up-dns-resolver [SWITCHES]

Meta-switches
    -h, --help                  Prints this help message and quits
    --help-all                  Print help messages of all subcommands and quit
    -v, --version               Prints the program's version and quits

Switches
    --days, -n VALUE:int        Use domains of history up to n days before the last made entry; the default is 7
    --domain, -d VALUE:str      Domain to resolve; may be given multiple times
    --file, -f VALUE:str        Path to file containing domains to be resolved; may be given multiple times
    --use-firefox               Use domains in Mozilla Firefox's history
```

It can also scrape domains directly from Mozilla Firefox's history. The matching systemd *.service and *.timer files
execute this command: `warm-up-dns-resolver --file ~/.warm-up-dns-resolver-domains --use-firefox`. This allows me to
place high-priority domains into a file in my home directory and also always quickly resolve domains that I visited in
the last 7 days using Firefox. Additionally I adapted my `unbound.conf` a bit:

```
server:
  use-syslog: yes
  username: "unbound"
  directory: "/etc/unbound"
  trust-anchor-file: trusted-key.key
  root-hints: "/etc/unbound/root.hints"

  cache-min-ttl: 3600
  prefetch: yes
  prefetch-key: yes
```

`cache-min-ttl: 3600` forces caching of resolved domains to at least one hour. Due to enabling `prefetch`, Unbound will
start resolving cached domains as soon as their remaining TTL falls below 10% -- that's why I configured the systemd
timer unit to run every 6 minutes. In theory this should keep every specified domain cached in Unbound.


## systemd-octor
```
usage: systemd-octor [-h] [--output OUTPUT] [--compare COMPARE COMPARE]

optional arguments:
  -h, --help            show this help message and exit
  --output OUTPUT, -o OUTPUT
                        Change destination of output file
  --compare COMPARE COMPARE, -c COMPARE COMPARE
                        Compare first output to second output
```

This is used to compare the systemd service configuration between two systems. Useful for example in case some important
units were disabled on system A and the exact changes made were forgotten. An easy way to fix the configuration then is
to create a fresh Arch Linux installation (system B) in a `systemd-nspawn` container, or as a full virtual machine, and
running this script to get a sane systemd service configuration which can then be compared using:
`systemd-octor --compare A.json B.json`.


## fix-openvpn
```# systemctl enable fix-openvpn@<syslog-identifier>```
```usage: fix-openvpn [-h] syslog-identifier [gateway]

positional arguments:
  syslog-identifier  The syslog identifier of the journal to monitor
  gateway            Specify the gateway. If not set, the script will attempt
                     to determine the default gateway

optional arguments:
  -h, --help         show this help message and exit
```

Monitors the OpenVPN systemd log and automatically adds routes through the default gateway for remote link IPs that are
attempted to be connected to. This is needed when the resolved IP address for a specified VPN domain changes, preventing
automatic reconnects to the VPN server, because the traffic is routed through a broken connection.

Note: It seems that OpenVPN already attempts to do that on its own, but somehow fails. It might be using the old IP
address after re-establishing the tunnel.

## [aur-auto-vote](https://www.reddit.com/r/archlinux/comments/4ryh6t/aur_autovote/)
I really wanted to show my appreciation for the AUR packages that I am using, but am entirely too lazy to keep the list
of voted-for packages up-to-date manually.

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

When voting already voted-for packages will be automatically skipped. Local PKGBUILDs I usually prefix with my nick,
i.e. `cryzed-` so I pass in `--ignore 'cryzed-.*'`. If you feel that your voted-for packages are completely outdated,
consider using `--unvote-all` to remove all votes beforehand. It might be a good idea to specify a `--delay` > 0 to
prevent hammering the server.

## backup-system
* `# systemctl start backup-system` (to start the script via systemd. A systemd `EnvironmentFile` with a `DIRECTORY` key
is needed at `/etc/backup-system.conf`)
* `# backup-system [DESTINATION]` (to start the script manually, destination is optional)
* `# systemctl enable backup-system.timer` (to enable the timer for daily backups)

This is a script that backups the most important parts of my Arch Linux installation, should it ever break in an
unrecoverable fashion. It uses:

* [`lostfiles`](https://aur.archlinux.org/packages/lostfiles/) to get a list of files in the system which are not part
of any package, i.e. files I most likely created and added to the system without using a custom PKGBUILD.
* `pacman -Qii | awk '/^MODIFIED/ {print $2}'` to get a list of modified backup files, i.e. modified configuration files
of installed packages
* `pacman -Q --explicit` to save the list of all explicitly installed packages
* all systemd overrides located in `/etc/systemd/system` or `/etc/systemd/user`
* `systemd-octor` (see above) to save the systemd service configuration
* all `/home` directories
* `/root`

and uses `tar` to compress all those files into an archive with the current date.

Note that I have symlinked all XDG directories, i.e. "Documents", "Downloads", "Music" etc. to a different HDD to
prevent unnecessary writes on my system SSD -- so when backing up the `/home` directories, tar will only backup the
dotfiles and not automatically follow the symlinks. The resulting backup file is usually around ~10-12 GB in size.
