pkgname='cryzed-bin'
pkgver=1
pkgrel=1
arch=('any')
url='https://github.com/cryzed/bin'
license=('MIT')
depends=('python-plumbum' 'python-peewee' 'python-psutil' 'lostfiles' 'systemd'
         'networkmanager' 'python-systemd')
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
        'fix-networkmanager-openvpn'
        'fix-networkmanager-openvpn.service')
md5sums=('8a3b2486266d94a5338ed936eba0d7d9'
         'd41d8cd98f00b204e9800998ecf8427e'
         'f499dcf2bb99dc6d1d937f1b8a9dc7f6'
         '28c30f22e1f202f2ed4bfb2d7e981c20'
         '0b5f1e4424ee905d1c6365a2f04a6ed5'
         'cbf72293797013c3e7c1cda4dc5d7155'
         '4e4ad52e9b431121ba2453f73863a42d'
         '19c2fbe44de491ec04fa4c232f38a4bd'
         'de99f0c9afd92546b94fc2fb81c3e2b0'
         '6665c0605b72b03d00140ba35f682cc7'
         '96be73f93b335a3e6583d33b9c7e158d'
         'fc0f6cd2d87c091653ce45d8153d9c6b')

package() {
    usr_bin="$pkgdir/usr/bin"
    mkdir -p "$usr_bin"
    cp 'vpn-whitelist-domains' "$usr_bin"
    cp 'warm-up-dns-resolver' "$usr_bin"
    cp 'restart-plasmashell' "$usr_bin"
    cp 'backup-system' "$usr_bin"
    cp 'keep-process-alive' "$usr_bin"
    cp 'systemd-octor' "$usr_bin"
    cp 'fix-networkmanager-openvpn' "$usr_bin"

    etc_vpn_whitelist_domains="$pkgdir/etc/vpn-whitelist-domains"
    mkdir -p "$etc_vpn_whitelist_domains"
    cp 'vpn-whitelist-domains.domains' "$etc_vpn_whitelist_domains/domains"

    etc_networkmanager_dispatcher="$pkgdir/etc/NetworkManager/dispatcher.d"
    mkdir -p "$etc_networkmanager_dispatcher"
    cp 'vpn-whitelist-domains.networkmanager-dispatcher' "$etc_networkmanager_dispatcher/vpn-whitelist-domains"

    etc_systemd_system="$pkgdir/etc/systemd/system"
    mkdir -p "$etc_systemd_system"
    cp 'fix-networkmanager-openvpn.service' "$etc_systemd_system"

    etc_systemd_user="$pkgdir/etc/systemd/user"
    mkdir -p "$etc_systemd_user"
    cp 'warm-up-dns-resolver.service' "$etc_systemd_user"
    cp 'warm-up-dns-resolver.timer' "$etc_systemd_user"
}
