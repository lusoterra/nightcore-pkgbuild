# Maintainer: Lev <lev@lusosterone.net>

pkgname=nightcore
_pkgname=nightcore
pkgver=2026.10.10
pkgrel=1
# Full upstream version as written in pyproject.toml (pkgver itself may not
# contain a hyphen, so the -4 lives here and in pkgrel).
_pkgver=2026.10.10-1
_tag=v${_pkgver}
pkgdesc="Bit-perfect nightcore/speed/pitch audio tool (ffmpeg, sox, rubberband)"
arch=('any')
url="https://git.lusosterone.net/lev/nightcore"
license=('MIT')
depends=(
    'python'
    'python-mutagen'
    'ffmpeg'
    'sox'
    'rubberband'
    'flac'
    'opus-tools'
    'vorbis-tools'
)
optdepends=(
    'lame: preferred MP3 encoder (ffmpeg libmp3lame fallback)'
    'qaac-wine: High-quality AAC/ALAC encoding (CoreAudio via Wine)'
    'bash-completion: bash completion'
    'zsh: zsh completion'
)
makedepends=('python-build' 'python-installer' 'python-setuptools')
conflicts=("$_pkgname-git")
source=("${_pkgname}-${_pkgver}.tar.gz::${url}/releases/download/${_tag}/${_pkgname}-${_pkgver}.tar.gz"
        "${_pkgname}-${_pkgver}.tar.gz.sig::${url}/releases/download/${_tag}/${_pkgname}-${_pkgver}.tar.gz.sig")

sha256sums=('d39a508c8c096dab013fdc099c102b3476ea071afec786d75d1b61da699b32b3'
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
