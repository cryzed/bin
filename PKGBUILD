pkgname='cryzed-bin'
pkgver=1
pkgrel=1
arch=('any')
url='https://github.com/cryzed/bin'
license=('MIT')
depends=('python-plumbum' 'python-peewee' 'python-psutil' 'lostfiles')
source=('vpn-whitelist-domain'
        'warm-up-dns-resolver'
        'warm-up-dns-resolver.service'
        'warm-up-dns-resolver.timer'
        'restart-plasmashell'
        'backup-system'
        'keep-process-alive')
md5sums=('6af39b927adc5b637962b49c8a69bebe'
         '9c922befa1569b99f783e0fee1a43547'
         '8f493eb0b99b1eb7e38150d2a34260fa'
         'dda106bf7b2a7ff510f734974ebbbddb'
         '4e4ad52e9b431121ba2453f73863a42d'
         '3a6a57f8e47c07979cdf64805d5d5b19'
         '5ac369c269602134f910be3a3610e324')

package() {
    usr_bin="$pkgdir/usr/bin"
    mkdir -p "$usr_bin"
    cp 'vpn-whitelist-domain' "$usr_bin"
    cp 'warm-up-dns-resolver' "$usr_bin"
    cp 'restart-plasmashell' "$usr_bin"
    cp 'backup-system' "$usr_bin"
    cp 'keep-process-alive' "$usr_bin"

    etc_systemd_user="$pkgdir/etc/systemd/user"
    mkdir -p "$etc_systemd_user"
    cp 'warm-up-dns-resolver.service' "$etc_systemd_user"
    cp 'warm-up-dns-resolver.timer' "$etc_systemd_user"
}
