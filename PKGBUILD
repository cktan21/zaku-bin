pkgname=zaku-bin
pkgver=26.0
pkgrel=1

pkgdesc="Fast, open-source API client with fangs"
arch=('x86_64' 'aarch64')
url="https://zaku.dev"
license=('AGPL-3.0-or-later')

depends=(
    'glibc'
    'gcc-libs'
    'libglvnd'
    'wayland'
    'xdg-utils'
)

provides=('zaku')
conflicts=('zaku')

options=('!strip')

source_x86_64=(
    "Zaku-${pkgver}-linux-x86_64.tar.gz::https://api.zaku.dev/releases/stable/${pkgver}/linux-x86_64/download"
)

source_aarch64=(
    "Zaku-${pkgver}-linux-aarch64.tar.gz::https://api.zaku.dev/releases/stable/${pkgver}/linux-aarch64/download"
)

sha256sums_x86_64=(
    '4386fac7cd7cfe891b77940ba67c392e687835c9103a722b255d710c26e55e67'
)

sha256sums_aarch64=(
    '2ddd7c6a71cfc55a51eb37c68156e2607a8cadaab0a06c1d1cf599c55b6e6291'
)

package() {
    # Zaku ships its own runtime libraries and expects:
    #
    #   libexec/zaku
    #   lib/*.so
    #
    # The binary has an RPATH of $ORIGIN/../lib.

    install -dm755 "$pkgdir/usr/lib/zaku"

    cp -a \
        "$srcdir/zaku.app/lib" \
        "$srcdir/zaku.app/libexec" \
        "$pkgdir/usr/lib/zaku/"

    # CLI/application executable
    install -dm755 "$pkgdir/usr/bin"
    ln -s /usr/lib/zaku/libexec/zaku \
        "$pkgdir/usr/bin/zaku"

    # Desktop entry
    install -Dm644 \
        "$srcdir/zaku.app/share/applications/dev.zaku.Zaku.desktop" \
        "$pkgdir/usr/share/applications/dev.zaku.Zaku.desktop"

    # Icons
    install -Dm644 \
        "$srcdir/zaku.app/share/icons/hicolor/512x512/apps/zaku.png" \
        "$pkgdir/usr/share/icons/hicolor/512x512/apps/zaku.png"

    install -Dm644 \
        "$srcdir/zaku.app/share/icons/hicolor/1024x1024/apps/zaku.png" \
        "$pkgdir/usr/share/icons/hicolor/1024x1024/apps/zaku.png"
}