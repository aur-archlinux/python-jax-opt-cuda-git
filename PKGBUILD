# Maintainer: Daniel Bershatsky <bepshatsky@yandex.ru>
# Maintainer: Andrew Grigorev <andrew@ei-grad.ru>
# Maintainer: Alexandr Parkhomenko <it@52tour.ru>

pkgname=python-jax-opt-cuda-git
pkgver=0.2.9.3e290f91
pkgrel=1
pkgdesc="Differentiate, compile, and transform Numpy code."
arch=("x86_64")
url="https://github.com/google/jax/"
license=("Apache")
depends=(
    "absl-py"
    "python"
    "python-numpy"
    "python-protobuf"
    "python-six"
    "python-fastcache"
    #"python-opt-einsum"
    "cuda"
    "cudnn"
)
conflicts=("python-jax")
provides=("python-jax")
makedepends=("git" "bazel")
source=(
    "$pkgname::git+$url"
)
md5sums=(
    "SKIP"
)

pkgver() {
  cd $pkgname
  python -c "with open('jax/version.py') as fin: exec(fin.read(), globals()); print(__version__+ '.`git rev-list -n1 --abbrev-commit HEAD`')"
}

build() {
  cd $pkgname
  TF_CUDA_PATHS=/usr,/opt/cuda python build/build.py --enable_cuda --enable_march_native
}

package() {
  cd $pkgname
#  (cd build && python setup.py install --optimize=1 --root=$pkgdir)
  python setup.py install --optimize=1 --root=$pkgdir
  INSTALL_PATH="$pkgdir/usr/lib/python3.9/site-packages/"
  mkdir -p $INSTALL_PATH
  unzip dist/jaxlib-0.1.60-cp39-none-manylinux2010_x86_64.whl -d $INSTALL_PATH
}
