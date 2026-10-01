# Maintainer: Lev <lev@lusosterone.net>

pkgname=nightcore
_pkgname=nightcore
pkgver=2026.10.01
pkgrel=4
# Full upstream version as written in pyproject.toml (pkgver itself may not
# contain a hyphen, so the -4 lives here and in pkgrel).
_pkgver=2026.10.01-4
_tag=v${_pkgver}
pkgdesc="Bit-perfect nightcore/speed/pitch audio tool (ffmpeg, sox, rubberband)"
arch=('any')
url="https://git.lusosterone.net/lev/nightcore"
license=('MIT')
depends=(
    'python'
    'ffmpeg'
    'sox'
    'rubberband'
    'flac'
    'opus-tools'
    'vorbis-tools'
)
optdepends=(
    'lame: MP3 fallback when ffmpeg lacks libmp3lame'
    'qaac-wine: High-quality AAC/ALAC encoding (CoreAudio via Wine)'
    'bash-completion: bash completion'
    'zsh: zsh completion'
)
makedepends=('python-build' 'python-installer' 'python-setuptools')
conflicts=("$_pkgname-git")
source=("${_pkgname}-${_pkgver}.tar.gz::${url}/releases/download/${_tag}/${_pkgname}-${_pkgver}.tar.gz"
        "${_pkgname}-${_pkgver}.tar.gz.sig::${url}/releases/download/${_tag}/${_pkgname}-${_pkgver}.tar.gz.sig")

sha256sums=('676cebc230172276fa5cdb9303b23ad89e2e22343ef4d02d30e6a34a17bd2e7b'
            'SKIP')
validpgpkeys=('13EA3CFB9ABC093823509BD668C62637ED987692')

build() {
    cd "$_pkgname-$_pkgver"
    python -m build --wheel --no-isolation
}

package() {
    cd "$_pkgname-$_pkgver"
    python -m installer --destdir="$pkgdir" dist/*.whl
    install -Dm644 completions/nightcore.bash "$pkgdir/usr/share/bash-completion/completions/nightcore"
    install -Dm644 completions/_nightcore "$pkgdir/usr/share/zsh/site-functions/_nightcore"
    install -Dm644 nightcore.1 "$pkgdir/usr/share/man/man1/nightcore.1"
    install -Dm644 LICENSE "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
}
