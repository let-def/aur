# Maintainer: Caleb Maclennan <caleb@alerque.com>

pkgname=nodejs-addon-api
_npmname=${pkgname/js}
pkgver=2.0.0
pkgrel=1
pkgdesc='Node.js API (N-API)'
arch=('any')
url="https://github.com/nodejs/$_npmname"
license=('MIT')
depends=('nodejs')
makedepends=('npm' 'jq' 'moreutils')
source=("https://registry.npmjs.org/$_npmname/-/$_npmname-$pkgver.tgz")
sha256sums=('1a84bbf44b12660d2a241ee30338de6fd8be41992efa4bc8ceef42c763ce6088')
noextract=("${source[@]##*/}")

package() {
    npm install -g --user root --cache "$srcdir/npm-cache" --no-audit --no-fund --prefix "$pkgdir/usr" "${source[@]##*/}"
    find "$pkgdir"/usr -type d -exec chmod 755 {} +
    find "$pkgdir" -type f -name package.json \
        -execdir sh -c "jq '. |= with_entries(select(.key | test(\"_.+\") | not))' {} | sponge {}" \;
    chown -R root:root "$pkgdir"
}
