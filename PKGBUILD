# Maintainer: thynkon <thynkon at protonmail dot com>
# Maintainer: Caleb Maclennan <caleb@alerque.com>

pkgname=gitui-git
pkgver=0.17.1.r3.g8729530b
pkgrel=1
pkgdesc='Blazing fast terminal-ui for git written in Rust'
url='https://github.com/extrawurst/gitui'
arch=('x86_64' 'i686')
license=('MIT')
depends=('gcc-libs' 'libgit2>=1.2.0' 'libgit2.so' 'libxcb' 'zlib')
makedepends=('git' 'cargo' 'python') # xcb crate needs python
provides=("gitui=$pkgver")
conflicts=('gitui')
source=("$pkgname::git+$url.git")
sha256sums=('SKIP')

prepare() {
  cd "${pkgname}"
  cargo fetch --locked --target "$CARCH-unknown-linux-gnu"
}

pkgver() {
  cd "${pkgname}"
  git describe --long | sed 's/^v//;s/\([^-]*-g\)/r\1/;s/-/./g'
}

build() {
  cd "${pkgname}"
  export RUSTUP_TOOLCHAIN=stable
  export CARGO_TARGET_DIR=target
  export LIBGIT2_SYS_USE_PKG_CONFIG=1
  cargo build --frozen --release
}

check() {
  cd "${pkgname}"
  export RUSTUP_TOOLCHAIN=stable
  export LIBGIT2_SYS_USE_PKG_CONFIG=1
  cargo test --frozen --release
}

package() {
  cd "$pkgname"
  install -Dm 755 "target/release/${pkgname%-git}" -t "${pkgdir}/usr/bin/${pkgname%-git}"
  install -Dm 644 {KEY_CONFIG,README,THEMES}.md -t "${pkgdir}/usr/share/doc/${pkgname}"
  install -Dm 644 LICENSE.md -t "${pkgdir}/usr/share/licenses/${pkgname%-git}"
}
