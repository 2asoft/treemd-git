pkgname=treemd
pkgver=0.10.0
pkgrel=1
pkgdesc="A markdown navigator with tree-based structural navigation"
arch=('x86_64')
url="https://github.com/Epistates/treemd"
license=('MIT')
depends=(
  'libgcc'
  'oniguruma'
)
makedepends=('cargo')
source=("$pkgname::git+${url}")
sha256sums=('SKIP')
options=('!lto')

prepare() {
  cd "$pkgname"
  cargo fetch --locked --target "$(rustc --print host-tuple)"
}

build() {
  cd "$pkgname"
  export RUSTONIG_SYSTEM_LIBONIG=1
  cargo build --release --frozen
}

check() {
  cd "$pkgname"
  cargo test --frozen
}

package() {
  cd "$pkgname"
  install -Dm 755 "target/release/$pkgname" "$pkgdir/usr/bin/$pkgname"
  install -Dm 644 README.md -t "$pkgdir/usr/share/doc/$pkgname"
  install -Dm 644 LICENSE -t "$pkgdir/usr/share/licenses/$pkgname"
}
