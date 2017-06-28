pkgname='local-bin'
pkgver=1
pkgrel=1
arch=('any')
url='https://github.com/cryzed/bin'
license=('MIT')
depends=('python' 'networkmanager' 'python-requests' 'python-beautifulsoup4'
         'python-html5lib' 'python-xlib' 'python-tqdm' 'borg' 'smartmontools'
         'python-plumbum' 'unbound')
backup=('etc/vpn-whitelist.addresses'
        'etc/backup.conf')
source=('vpn-whitelist'
        'vpn-whitelist.addresses'
        'vpn-whitelist.networkmanager-dispatcher'
        'restart-plasmashell'
        'backup.service'
        'backup.timer'
        'backup.conf'
        'aur-auto-vote'
        'defaults'
        'hotstrings'
        'smartd-create-super-users-desktop-file'
        'smartd-wall'
        'update-unbound-root-hints.timer'
        'update-unbound-root-hints.service')
md5sums=('ee9da778244926085cf8694361028bd7'
         'd41d8cd98f00b204e9800998ecf8427e'
         '821993dc77ce23f25e0de9162a447664'
         '56e35e81dc59e38eb8dadef358ed67db'
         'dcf24df9e444aa1115155348a299ab15'
         '0fdcfc45ceec87c3115f7cf4f2d0d0d3'
         'eb1bde0663e0a4fb89e36a54b4ca63c3'
         '11fbb58590d1f804050ce7a0548d869a'
         '1413890025bab242a314279a6f013c3f'
         '71e6c5aa7fdfe0b27e49f418eff416e4'
         '9d88f20f56b8f8fda279737b2839cb04'
         'cedc139256ef95bffe303eff9f284ac8'
         '7c7a594f8d1a31b3708226fbf8c0fea1'
         '44727f221685187f0db5333e80264cee')


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
    install -D --mode 600 'backup.conf' --target-directory "$etc"

    # /etc/NetworkManager/dispatcher.d
    install -D --mode 755 'vpn-whitelist.networkmanager-dispatcher' "$etc/NetworkManager/dispatcher.d/vpn-whitelist"

    # /etc/systemd/system
    etc_systemd_system="$etc/systemd/system"
    install -D --mode 644 'backup.service' --target-directory "$etc_systemd_system"
    install -D --mode 644 'backup.timer' --target-directory "$etc_systemd_system"
    install -D --mode 644 'update-unbound-root-hints.service' --target-directory "$etc_systemd_system"
    install -D --mode 644 'update-unbound-root-hints.timer' --target-directory "$etc_systemd_system"

    # /usr/share/smartmontools/smartd_warning.d/
    smartd_warning_d="$pkgdir/usr/share/smartmontools/smartd_warning.d"
    install -D --mode 755 'smartd-create-super-users-desktop-file' "$smartd_warning_d/create-super-users-desktop-file"
    install -D --mode 755 'smartd-wall' "$smartd_warning_d/wall"
}
