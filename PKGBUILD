#@IgnoreInspection BashAddShebang
pkgname=local-bin
pkgver=1
pkgrel=1
arch=(any)
url=https://github.com/cryzed/bin
license=(MIT)
depends=(python python-plumbum python-peewee lostfiles systemd networkmanager python-systemd
         python-requests python-beautifulsoup4 python-html5lib python-xlib python-tqdm youtube-dl)
backup=(etc/vpn-whitelist.addresses
        etc/backup-system.conf)
source=(vpn-whitelist
        vpn-whitelist.addresses
        vpn-whitelist.networkmanager-dispatcher
        warm-up-dns-resolver
        warm-up-dns-resolver.service
        warm-up-dns-resolver.timer
        restart-plasmashell
        backup-system
        backup-system.service
        backup-system.timer
        backup-system.conf
        systemd-octor
        fix-openvpn
        fix-openvpn@.service
        aur-auto-vote
        defaults
        hotstrings
        provides)
md5sums=('ee9da778244926085cf8694361028bd7'
         'd41d8cd98f00b204e9800998ecf8427e'
         'daee1dc2923f6c73421fee9b06072f88'
         'cd68102111c8551b8c0cb762bae88874'
         '2a6b37cd45fb5a2c2575f7570940f1dc'
         'cbf72293797013c3e7c1cda4dc5d7155'
         '56e35e81dc59e38eb8dadef358ed67db'
         '3f4aac2fe51a3ecb6d55a30c495038a7'
         'c5b4cb38118499d636bc4121a30ed0a3'
         '01b6c960bac9538e620d9dd08991195a'
         '0abe9cdcf110be3945454765579f01f8'
         '13769a58d4ca28eb6a9c46b2b195b3ab'
         '0a12bff48d9b16a7d00f92196bd52bb1'
         '020b54a9c478c2080034c73fa64dbb14'
         '11fbb58590d1f804050ce7a0548d869a'
         '1413890025bab242a314279a6f013c3f'
         '71e6c5aa7fdfe0b27e49f418eff416e4'
         'b77a3e0feeff8681845bf53eaf450b0e')


package() {
    # /usr/bin
    usr_bin="$pkgdir/usr/bin"
    install -D --mode 755 vpn-whitelist --target-directory "$usr_bin"
    install -D --mode 755 warm-up-dns-resolver --target-directory "$usr_bin"
    install -D --mode 755 restart-plasmashell --target-directory "$usr_bin"
    install -D --mode 755 backup-system --target-directory "$usr_bin"
    install -D --mode 755 systemd-octor --target-directory "$usr_bin"
    install -D --mode 755 fix-openvpn --target-directory "$usr_bin"
    install -D --mode 755 aur-auto-vote --target-directory "$usr_bin"
    install -D --mode 755 defaults --target-directory "$usr_bin"
    install -D --mode 755 hotstrings --target-directory "$usr_bin"
    install -D --mode 755 provides --target-directory "$usr_bin"

    # /etc
    etc="$pkgdir/etc"
    install -D --mode 644 vpn-whitelist.addresses --target-directory "$etc"
    install -D --mode 644 backup-system.conf --target-directory "$etc"

    # /etc/NetworkManager/dispatcher.d
    install -D --mode 755 vpn-whitelist.networkmanager-dispatcher "$etc/NetworkManager/dispatcher.d/vpn-whitelist"

    # /etc/systemd/user
    etc_systemd_user="$etc/systemd/user"
    install -D --mode 644 warm-up-dns-resolver.service --target-directory "$etc_systemd_user"
    install -D --mode 644 warm-up-dns-resolver.timer --target-directory "$etc_systemd_user"

    # /etc/systemd/system
    etc_systemd_system="$etc/systemd/system"
    install -D --mode 644 fix-openvpn@.service --target-directory "$etc_systemd_system"
    install -D --mode 644 backup-system.service --target-directory "$etc_systemd_system"
    install -D --mode 644 backup-system.timer --target-directory "$etc_systemd_system"
}
