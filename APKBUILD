# Maintainer: Omar Roth <omarroth@protonmail.com>
pkgname="lsquic"
pkgver="2.6.3"
pkgrel=0
pkgdesc="LiteSpeed QUIC and HTTP/3 Library"
url="https://github.com/litespeedtech/lsquic"
arch="all"
license="MIT"
depends="boringssl-dev zlib-dev libevent-dev"
makedepends="cmake git go perl bsd-compat-headers"
install=""
#subpackages="$pkgname-doc $pkgname-dev"
source="https://github.com/litespeedtech/lsquic/archive/master.tar.gz
	lsquic_types.patch"
builddir="$srcdir/$pkgname-master"

prepare() {
	cd "$builddir"
	git clone https://github.com/litespeedtech/ls-qpack src/liblsquic/ls-qpack
	patch -p1 < "$srcdir/lsquic_types.patch"
	cmake -DCMAKE_BUILD_TYPE=Release -DBORINGSSL_INCLUDE=/usr/include/openssl -DEVENT_LIB=/usr/lib/libevent.so -DBORINGSSL_LIB_crypto=/usr/lib/libcrypto.a -DBORINGSSL_LIB_ssl=/usr/lib/libssl.a .
}

build() {
	cd "$builddir"
	make lsquic
}

check() {
	:
}

package() {
	cd "$builddir"
	install -Dm644 LICENSE "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
	install -Dm644 LICENSE.chrome "$pkgdir/usr/share/licenses/$pkgname/LICENSE.chrome"

	strip src/liblsquic/liblsquic.a
	install -d "$pkgdir/usr/lib"
	install -Dm755 src/liblsquic/liblsquic.a "$pkgdir/usr/lib/liblsquic.a"
}
sha512sums="6341c8d54dff69054927216a76a737e39639b180a3b7e67f7c73efa043432a6bd71bb466c22681f607998e76460bc7f33eb55f2fbd0735ee8de4c9ac036d69cc  master.tar.gz
45113c60781531cf06683c82458417ca7bc7d0602b608268792e8d2620595942c4fbd0dea4813e8f9458468dfb91eed535ea098217aa0a2b22de53e6c01f5233  lsquic_types.patch"
