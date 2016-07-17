pkgname='cryzed-bin'
pkgver=1
pkgrel=1
arch=('any')
url='https://github.com/cryzed/bin'
license=('MIT')
depends=('python' 'python-plumbum' 'python-peewee' 'python-psutil' 'lostfiles'
         'systemd' 'networkmanager' 'python-systemd' 'python-requests'
         'python-beautifulsoup4' 'python-html5lib')
backup=('etc/vpn-whitelist-domains/domains')
source=('vpn-whitelist-domains'
        'vpn-whitelist-domains.domains'
        'vpn-whitelist-domains.networkmanager-dispatcher'
        'warm-up-dns-resolver'
        'warm-up-dns-resolver.service'
        'warm-up-dns-resolver.timer'
        'restart-plasmashell'
        'backup-system'
        'keep-process-alive'
        'systemd-octor'
        'fix-openvpn'
        'fix-openvpn@.service'
        'aur-auto-vote')
md5sums=('fd2172b03141903c33f5dc47b1c842e2'
         'd41d8cd98f00b204e9800998ecf8427e'
         '6cb4c2f54af73993d84c6a318e81d6e7'
         '28c30f22e1f202f2ed4bfb2d7e981c20'
         '2a6b37cd45fb5a2c2575f7570940f1dc'
         'cbf72293797013c3e7c1cda4dc5d7155'
         '4e4ad52e9b431121ba2453f73863a42d'
         '2d320eb1db2b9afb7e72c6f25436bf37'
         'de99f0c9afd92546b94fc2fb81c3e2b0'
         '6665c0605b72b03d00140ba35f682cc7'
         '50c8f18c04c9f1034769dbbc17e14881'
         '9733285261415b47cd8f116e328a4474'
         '9b2c600c04e74399edd83875b60ad846')

package() {
    usr_bin="$pkgdir/usr/bin"
    mkdir -p "$usr_bin"
    cp 'vpn-whitelist-domains' "$usr_bin"
    cp 'warm-up-dns-resolver' "$usr_bin"
    cp 'restart-plasmashell' "$usr_bin"
    cp 'backup-system' "$usr_bin"
    cp 'keep-process-alive' "$usr_bin"
    cp 'systemd-octor' "$usr_bin"
    cp 'fix-openvpn' "$usr_bin"
    cp 'aur-auto-vote' "$usr_bin"

    etc_vpn_whitelist_domains="$pkgdir/etc/vpn-whitelist-domains"
    mkdir -p "$etc_vpn_whitelist_domains"
    cp 'vpn-whitelist-domains.domains' "$etc_vpn_whitelist_domains/domains"

    etc_networkmanager_dispatcher="$pkgdir/etc/NetworkManager/dispatcher.d"
    mkdir -p "$etc_networkmanager_dispatcher"
    cp 'vpn-whitelist-domains.networkmanager-dispatcher' "$etc_networkmanager_dispatcher/vpn-whitelist-domains"

    etc_systemd_system="$pkgdir/etc/systemd/system"
    mkdir -p "$etc_systemd_system"
    cp 'fix-openvpn@.service' "$etc_systemd_system"

    etc_systemd_user="$pkgdir/etc/systemd/user"
    mkdir -p "$etc_systemd_user"
    cp 'warm-up-dns-resolver.service' "$etc_systemd_user"
    cp 'warm-up-dns-resolver.timer' "$etc_systemd_user"
}
