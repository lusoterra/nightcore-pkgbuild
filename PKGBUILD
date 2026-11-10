# Maintainer: Lev <lev@lusosterone.net>

pkgname=nightcore
_pkgname=nightcore
pkgver=2026.10.21
pkgrel=1
# Full upstream version as written in pyproject.toml (pkgver itself may not
# contain a hyphen, so the -4 lives here and in pkgrel).
_pkgver=2026.10.21-1
_tag=v${_pkgver}
pkgdesc="Bit-perfect nightcore/speed/pitch audio tool (ffmpeg, sox, rubberband)"
arch=('any')
url="https://github.com/lusoterra/nightcore.py"
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
    'ffmpeg-full: FDK-AAC support'
    'bash-completion: bash completion'
    'zsh: zsh completion'
    'fish: fish completion'
)
makedepends=('python-build' 'python-installer' 'python-setuptools')
conflicts=("$_pkgname-git")
source=("${_pkgname}-${_pkgver}.tar.gz::${url}/releases/download/${_tag}/${_pkgname}-${_pkgver}.tar.gz"
        "${_pkgname}-${_pkgver}.tar.gz.sig::${url}/releases/download/${_tag}/${_pkgname}-${_pkgver}.tar.gz.sig")

sha256sums=('3373606ebb1f0ae72eb48810bac64b1c677c662ac5db6381253b48a8fa87608e'
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
    install -Dm644 completions/nightcore.fish "$pkgdir/usr/share/fish/vendor_completions.d/nightcore.fish"
    install -Dm644 nightcore.1 "$pkgdir/usr/share/man/man1/nightcore.1"
    install -Dm644 LICENSE "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
}
