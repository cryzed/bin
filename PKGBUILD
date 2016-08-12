pkgname='cryzed-bin'
pkgver=1
pkgrel=1
arch=('any')
url='https://github.com/cryzed/bin'
license=('MIT')
depends=('python' 'python-plumbum' 'python-peewee' 'lostfiles' 'systemd'
         'networkmanager' 'python-systemd' 'python-requests'
         'python-beautifulsoup4' 'python-html5lib' 'python-xlib')
backup=('etc/vpn-whitelist.addresses'
        'etc/backup-system.conf')
source=('vpn-whitelist'
        'vpn-whitelist.'{'addresses','networkmanager-dispatcher'}
        'warm-up-dns-resolver'
        'warm-up-dns-resolver.'{'service','timer'}
        'restart-plasmashell'
        'backup-system'
        'backup-system.'{'service','timer','conf'}
        'systemd-octor'
        'fix-openvpn'
        'fix-openvpn@.service'
        'aur-auto-vote'
        'what-did-i-do'
        'hotstrings')
md5sums=('eb0aab81b02a28e3e308f8de39be1f93'
         'd41d8cd98f00b204e9800998ecf8427e'
         'd1f2a15d7153d8d1586058914b52f2e8'
         '76087fa6e8c900fd164abe4dbc981892'
         '2a6b37cd45fb5a2c2575f7570940f1dc'
         'cbf72293797013c3e7c1cda4dc5d7155'
         '4e4ad52e9b431121ba2453f73863a42d'
         'f03a77e8efd80b00cf8672775f783e08'
         'f93789f6e9ceea3c6e512f6c40ea16e7'
         '01b6c960bac9538e620d9dd08991195a'
         '609e76c7a3fd1931085188a3726be480'
         '30ff20a49ef656a27e2a312feaa9c881'
         'e399c5c0721e2a48acc4168f6749af04'
         '020b54a9c478c2080034c73fa64dbb14'
         '9b2c600c04e74399edd83875b60ad846'
         '8940c60d9ae513956c129315f2e01aff'
         '299d8e4181ef952849cb0cc3bda2744d')


package() {
    # /usr/bin
    usr_bin="$pkgdir/usr/bin"
    mkdir -p "$usr_bin"
    cp 'vpn-whitelist' "$usr_bin"
    cp 'warm-up-dns-resolver' "$usr_bin"
    cp 'restart-plasmashell' "$usr_bin"
    cp 'backup-system' "$usr_bin"
    cp 'systemd-octor' "$usr_bin"
    cp 'fix-openvpn' "$usr_bin"
    cp 'aur-auto-vote' "$usr_bin"
    cp 'what-did-i-do' "$usr_bin"
    cp 'hotstrings' "$usr_bin"

    # /etc
    etc="$pkgdir/etc"
    mkdir -p "$etc"
    cp 'backup-system.conf' "$etc"
    cp 'vpn-whitelist.addresses' "$etc"

    # /etc/NetworkManager/dispatcher.d
    etc_networkmanager_dispatcher="$pkgdir/etc/NetworkManager/dispatcher.d"
    mkdir -p "$etc_networkmanager_dispatcher"
    cp 'vpn-whitelist.networkmanager-dispatcher' "$etc_networkmanager_dispatcher/vpn-whitelist"

    # /etc/systemd/user
    etc_systemd_user="$pkgdir/etc/systemd/user"
    mkdir -p "$etc_systemd_user"
    cp 'warm-up-dns-resolver.'{'service','timer'} "$etc_systemd_user"

    # /etc/systemd/system
    etc_systemd_system="$pkgdir/etc/systemd/system"
    mkdir -p "$etc_systemd_system"
    cp 'fix-openvpn@.service' "$etc_systemd_system"
    cp 'backup-system.'{'service','timer'} "$etc_systemd_system"
}
