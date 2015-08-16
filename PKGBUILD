# Maintainer: Arch Haskell Team <arch-haskell@haskell.org>
_hkgname=logic-TPTP
pkgname=haskell-logic-tptp
pkgver=0.2.0.4
pkgrel=3
pkgdesc="Import, export etc. for TPTP, a syntax for first-order logic"
url="http://hackage.haskell.org/package/${_hkgname}"
license=('GPL')
arch=('i686' 'x86_64')
makedepends=()
depends=('ghc' 'haskell-quickcheck=2.1.1.1' 'haskell-ansi-wl-pprint' 'haskell-array=0.3.0.1' 'haskell-containers=0.3.0.0' 'haskell-haskell98=1.0.1.1' 'haskell-mtl' 'haskell-syb=0.1.0.2' 'haskell-utf8-prelude')
options=('strip')
source=(http://hackage.haskell.org/packages/archive/${_hkgname}/${pkgver}/${_hkgname}-${pkgver}.tar.gz)
install=${pkgname}.install
build() {
    cd ${srcdir}/${_hkgname}-${pkgver}
    runhaskell Setup configure -O --enable-split-objs --enable-shared \
       --prefix=/usr --docdir=/usr/share/doc/${pkgname} --libsubdir=\$compiler/site-local/\$pkgid
    runhaskell Setup build
    runhaskell Setup haddock
    runhaskell Setup register   --gen-script
    runhaskell Setup unregister --gen-script
    sed -i -r -e "s|ghc-pkg.*unregister[^ ]* |&'--force' |" unregister.sh
}
package() {
    cd ${srcdir}/${_hkgname}-${pkgver}
    install -D -m744 register.sh   ${pkgdir}/usr/share/haskell/${pkgname}/register.sh
    install    -m744 unregister.sh ${pkgdir}/usr/share/haskell/${pkgname}/unregister.sh
    install -d -m755 ${pkgdir}/usr/share/doc/ghc/html/libraries
    ln -s /usr/share/doc/${pkgname}/html ${pkgdir}/usr/share/doc/ghc/html/libraries/${_hkgname}
    runhaskell Setup copy --destdir=${pkgdir}
}
md5sums=('80c5d2f0b88760229ddac430191aa93d')
