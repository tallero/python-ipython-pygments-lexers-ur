# SPDX-License-Identifier: AGPL-3.0

#    ----------------------------------------------------------------------
#    Copyright © 2024, 2025  Pellegrino Prevete
#
#    All rights reserved
#    ----------------------------------------------------------------------
#
#    This program is free software: you can redistribute it and/or modify
#    it under the terms of the GNU Affero General Public License as published by
#    the Free Software Foundation, either version 3 of the License, or
#    (at your option) any later version.
#
#    This program is distributed in the hope that it will be useful,
#    but WITHOUT ANY WARRANTY; without even the implied warranty of
#    MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
#    GNU Affero General Public License for more details.
#
#    You should have received a copy of the GNU Affero General Public License
#    along with this program.  If not, see <https://www.gnu.org/licenses/>.

# Maintainer: Truocolo <truocolo@aol.com>
# Maintainer: Truocolo <truocolo@0x6E5163fC4BFc1511Dbe06bB605cc14a3e462332b>
# Maintainer: Pellegrino Prevete (dvorak) <pellegrinoprevete@gmail.com>
# Maintainer: Pellegrino Prevete (dvorak) <dvorak@0x87003Bd6C074C713783df04f36517451fF34CBEf>
# Maintainer: Daniel M. Capella <polyzen@archlinux.org>

_py="python"
_pyver="$( \
  "${_py}" \
    -V | \
    awk \
      '{print $2}')"
_pymajver="${_pyver%.*}"
_pyminver="${_pymajver#*.}"
_pynextver="${_pymajver%.*}.$(( \
  ${_pyminver} + 1))"
_pkg="ipython-pygments-lexers"
pkgname="${_py}-${_pkg}"
pkgver=1.1.1
pkgrel=1
_pkgdesc=(
  'Defines a variety of Pygments'
  'lexers for highlighting IPython code'
)
pkgdesc="${_pkgdesc[*]}"
arch=(
  'any')
_http="https://github.com/"
_ns="ipython"
url="${_http}/${_ns}/${_pkg}"
license=(
  'BSD-3-Clause'
)
depends=(
  "${_py}>=${_pymajver}"
  "${_py}<${_pynextver}"
  "${_py}-pygments"
)
makedepends=(
  "git"
  "${_py}-build"
  "${_py}-flit-core"
  "${_py}-installer"
)
checkdepends=(
  "ipython"
  "${_py}-pytest"
)
source=(
  "git+${url}.git#tag=${pkgver}"
)
b2sums=(
  '212e91dbe6ad3d2c5df5d4982a0794515bea4b0fef358de8cf1c2bd15ad350b1e23c709a03bfdcc78b85ea5cfa9b5006842ad165b92dc8fb81d4f826ee3eff4a'
)

build() {
  cd \
    "${_name}"
  "${_py}" \
    -m \
      "build" \
    --wheel \
    --skip-dependency-check \
    --no-isolation
}

check() {
  cd \
    "${_name}"
  pytest
}

package() {
  local \
    site_packages
  site_packages="$( \
    "${_py}" \
      -c \
        "import site; print(site.getsitepackages()[0])")"
  cd \
    "${srcdir}/${_pkg}"
  ls
  install \
    -d \
    "${pkgdir}/usr/share/licenses/${pkgname}"
  ln \
    -s \
    "${site_packages}/${_pkg//-/_}-${pkgver}.dist-info/licenses/LICENSE" \
    "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE"
  "${_py}" \
    -m \
      "installer" \
      --destdir="${pkgdir}" \
      "dist/"*".whl"
}
