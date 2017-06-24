pkgname='local-bin'
pkgver=1
pkgrel=1
arch=('any')
url='https://github.com/cryzed/bin'
license=('MIT')
depends=('python' 'networkmanager' 'python-requests' 'python-beautifulsoup4'
         'python-html5lib' 'python-xlib' 'python-tqdm' 'borg')
backup=('etc/vpn-whitelist.addresses'
        'etc/backup-system.conf')
source=('vpn-whitelist'
        'vpn-whitelist.addresses'
        'vpn-whitelist.networkmanager-dispatcher'
        'restart-plasmashell'
        'backup-system.service'
        'backup-system.timer'
        'backup-system.conf'
        'aur-auto-vote'
        'defaults'
        'hotstrings')
md5sums=('ee9da778244926085cf8694361028bd7'
         'd41d8cd98f00b204e9800998ecf8427e'
         'daee1dc2923f6c73421fee9b06072f88'
         '56e35e81dc59e38eb8dadef358ed67db'
         'fcbb5f10bbd8395f101fd023e9c0a2e4'
         '01b6c960bac9538e620d9dd08991195a'
         'eb1bde0663e0a4fb89e36a54b4ca63c3'
         '11fbb58590d1f804050ce7a0548d869a'
         '1413890025bab242a314279a6f013c3f'
         '71e6c5aa7fdfe0b27e49f418eff416e4')


package() {
    # /usr/bin
    usr_bin="$pkgdir/usr/bin"
    install -D --mode 755 'vpn-whitelist' --target-directory "$usr_bin"
    install -D --mode 755 'restart-plasmashell' --target-directory "$usr_bin"
    install -D --mode 755 'aur-auto-vote' --target-directory "$usr_bin"
    install -D --mode 755 'defaults' --target-directory "$usr_bin"
    install -D --mode 755 'hotstrings' --target-directory "$usr_bin"

    # /etc
    etc="$pkgdir/etc"
    install -D --mode 644 'vpn-whitelist.addresses' --target-directory "$etc"
    install -D --mode 600 'backup-system.conf' --target-directory "$etc"

    # /etc/NetworkManager/dispatcher.d
    install -D --mode 755 'vpn-whitelist.networkmanager-dispatcher' "$etc/NetworkManager/dispatcher.d/vpn-whitelist"

    # /etc/systemd/system
    etc_systemd_system="$etc/systemd/system"
    install -D --mode 644 'backup-system.service' --target-directory "$etc_systemd_system"
    install -D --mode 644 'backup-system.timer' --target-directory "$etc_systemd_system"
}
