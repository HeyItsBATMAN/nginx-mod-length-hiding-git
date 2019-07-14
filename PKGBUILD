pkgname=nginx-mod-length-hiding
pkgver=1.0
pkgrel=1

_modname="length-hiding-filter-module"
_nginxver=1.16.0

pkgdesc='nginx filter module to append random generated string to the end of HTML response '
arch=('i686' 'x86_64')
depends=('nginx')
url="https://github.com/nulab/nginx-length-hiding-filter-module"
license=('MIT')

source=(https://nginx.org/download/nginx-$_nginxver.tar.gz{,.asc}
        git+https://github.com/nulab/nginx-length-hiding-filter-module.git)
validpgpkeys=(B0F4253373F8F6F510D42178520A9993A1C052F8)
md5sums=('SKIP'
         'SKIP'
         'SKIP')

build() {
  cd "$srcdir"/nginx-$_nginxver
  ./configure --with-compat --add-dynamic-module=../nginx-$_modname
  make modules
}

package() {
  install -Dm644 "$srcdir/"nginx-$_modname/LICENSE \
                 "$pkgdir"/usr/share/licenses/$pkgname/LICENSE

  cd "$srcdir"/nginx-$_nginxver/objs
  for mod in *.so; do
    install -Dm755 $mod "$pkgdir"/usr/lib/nginx/modules/$mod
  done
}

