pkgname='cryzed-bin'
pkgver=1
pkgrel=1
arch=('any')
url='https://github.com/cryzed/bin'
license=('MIT')
depends=('python' 'python-plumbum' 'python-peewee' 'lostfiles' 'systemd' 'networkmanager' 'python-systemd'
         'python-requests' 'python-beautifulsoup4' 'python-html5lib' 'python-xlib' 'python-tqdm')
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
        'defaults'
        'hotstrings')
md5sums=('34b14aeeb7b83498b997f69b4c72a5e8'
         'd41d8cd98f00b204e9800998ecf8427e'
         'daee1dc2923f6c73421fee9b06072f88'
         '9c071c22393d8ba9d1c11021ae08a43c'
         '2a6b37cd45fb5a2c2575f7570940f1dc'
         'cbf72293797013c3e7c1cda4dc5d7155'
         '4e4ad52e9b431121ba2453f73863a42d'
         'f5096c603ce533fe31e5093ac7e3541d'
         'f93789f6e9ceea3c6e512f6c40ea16e7'
         '01b6c960bac9538e620d9dd08991195a'
         '609e76c7a3fd1931085188a3726be480'
         '13769a58d4ca28eb6a9c46b2b195b3ab'
         'c3e29ec92612aff3f677340a114afed3'
         '020b54a9c478c2080034c73fa64dbb14'
         '950db6dee8573be90c3603994c80d91e'
         '16d9bc42a11d26d9a51b92650e856e5d'
         '785d270baac91af36ad6611994d23579')


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
    cp 'defaults' "$usr_bin"
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
