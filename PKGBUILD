pkgdesc="ROS - tools to convert Unified Robot Description Format (URDF) to COLLADA."
url='http://www.ros.org/'

pkgname='ros-groovy-collada-urdf'
pkgver='1.9.36'
arch=('i686' 'x86_64')
pkgrel=1
license=('BSD')
makedepends=('ros-build-tools')

depends=(ros-groovy-urdf
  ros-groovy-angles
  ros-groovy-roscpp
  ros-groovy-resource-retriever
  ros-groovy-collada-parser
  assimp
  collada-dom)

build() {
  [ -f /opt/ros/groovy/setup.bash ] && source /opt/ros/groovy/setup.bash
  if [ -d ${srcdir}/collada_urdf ]; then
    cd ${srcdir}/collada_urdf
    git fetch origin --tags
    git reset --hard release/groovy/collada_urdf/${pkgver}-0
  else
    git clone -b release/groovy/collada_urdf/${pkgver}-0 git://github.com/ros-gbp/robot_model-release.git ${srcdir}/collada_urdf
  fi
  cd ${srcdir}/collada_urdf 
#&& patch -p1 < ${srcdir}/collada_urdf.patch
  [ -d ${srcdir}/build ] || mkdir ${srcdir}/build
  cd ${srcdir}/build
  /usr/share/ros-build-tools/fix-python-scripts.sh ${srcdir}/collada_urdf
  cmake ${srcdir}/collada_urdf -DCATKIN_BUILD_BINARY_PACKAGE=ON -DCMAKE_INSTALL_PREFIX=/opt/ros/groovy -DPYTHON_EXECUTABLE=/usr/bin/python2 -DPYTHON_INCLUDE_DIR=/usr/include/python2.7 -DPYTHON_LIBRARY=/usr/lib/libpython2.7.so -DSETUPTOOLS_DEB_LAYOUT=OFF
  make
}

package() {
  cd "${srcdir}/build"
  make DESTDIR="${pkgdir}/" install
}
