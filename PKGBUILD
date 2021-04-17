pkgname=slock
pkgver=20210418.52f4116
pkgrel=1
pkgdesc='Simple X display locker'
url='http://tools.suckless.org/slock'
arch=('i686' 'x86_64' 'armv7h')
license=('MIT')
makedepends=('git')
depends=('libxrandr')
source=('git://github.com/ArthurGoodman/slock.git')
sha256sums=('SKIP')

provides=("$pkgname")
conflicts=("$pkgname")

pkgver() {
  cd "$srcdir/$pkgname"
  git log -1 --format='%cd.%h' --date=short | tr -d -
}

prepare() {
  cd "$srcdir/$pkgname"
  sed "s/nobody/$(whoami)/g" -i lock.sh
}

build() {
  cd "$srcdir/$pkgname"
  make X11INC=/usr/include/X11 X11LIB=/usr/lib/X11
}

package() {
  cd "$srcdir/$pkgname"
  make PREFIX=/usr DESTDIR="${pkgdir}" install
  install -Dm644 LICENSE "${pkgdir}/usr/share/licenses/$pkgname/LICENSE"
  install -Dm755 lock.sh "${pkgdir}/usr/lib/elogind/system-sleep/lock.sh"
}
