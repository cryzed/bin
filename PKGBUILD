pkgname='cryzed-bin'
pkgver=1
pkgrel=1
arch=('any')
url='https://github.com/cryzed/bin'
license=('MIT')
depends=('python-plumbum' 'python-peewee' 'python-psutil' 'lostfiles' 'systemd'
         'networkmanager')
backup=("etc/vpn-whitelist-domains/domains")
source=('vpn-whitelist-domains'
        'vpn-whitelist-domains.service'
        'vpn-whitelist-domains.domains'
        'vpn-whitelist-domains.networkmanager-dispatcher-preup'
        'warm-up-dns-resolver'
        'warm-up-dns-resolver.service'
        'warm-up-dns-resolver.timer'
        'restart-plasmashell'
        'backup-system'
        'keep-process-alive'
        'systemd-octor')
md5sums=('e8b8c986a844142d123d5f0f3474b468'
         '4b2c8dd0ca22c4a551f3c534737d56b1'
         'd41d8cd98f00b204e9800998ecf8427e'
         '7b5e625d5b9df65530e2a9ee635cf11c'
         '28c30f22e1f202f2ed4bfb2d7e981c20'
         '8f493eb0b99b1eb7e38150d2a34260fa'
         'cbf72293797013c3e7c1cda4dc5d7155'
         '4e4ad52e9b431121ba2453f73863a42d'
         '19c2fbe44de491ec04fa4c232f38a4bd'
         'de99f0c9afd92546b94fc2fb81c3e2b0'
         'ded0003fa8968ced21072b029a1bd889')

package() {
    usr_bin="$pkgdir/usr/bin"
    mkdir -p "$usr_bin"
    cp 'vpn-whitelist-domains' "$usr_bin"
    cp 'warm-up-dns-resolver' "$usr_bin"
    cp 'restart-plasmashell' "$usr_bin"
    cp 'backup-system' "$usr_bin"
    cp 'keep-process-alive' "$usr_bin"
    cp 'systemd-octor' "$usr_bin"

    etc_systemd_system="$pkgdir/etc/systemd/system"
    mkdir -p "$etc_systemd_system"
    cp 'vpn-whitelist-domains.service' "$etc_systemd_system"

    etc_vpn_whitelist_domains="$pkgdir/etc/vpn-whitelist-domains"
    mkdir -p "$etc_vpn_whitelist_domains"
    cp 'vpn-whitelist-domains.domains' "$etc_vpn_whitelist_domains/domains"

    etc_networkmanager_preup="$pkgdir/etc/NetworkManager/dispatcher.d/pre-up.d"
    mkdir -p "$etc_networkmanager_preup"
    cp 'vpn-whitelist-domains.networkmanager-dispatcher-preup' "$etc_networkmanager_preup/vpn-whitelist-domains"

    etc_systemd_user="$pkgdir/etc/systemd/user"
    mkdir -p "$etc_systemd_user"
    cp 'warm-up-dns-resolver.service' "$etc_systemd_user"
    cp 'warm-up-dns-resolver.timer' "$etc_systemd_user"
}
