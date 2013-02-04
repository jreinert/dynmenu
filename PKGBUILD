# Maintainer: Joakim Reinert <mail@jreinert.com>
pkgname=dynmenu-git
pkgver=0.1
pkgrel=1
pkgdesc=""
arch=(any)
url="http://github.com/supasnashbuhl/dynmenu"
license=('GPL')
depends=('ruby' 'dmenu') # Full dependency information is available in the yaml specification
makedepends=('git' 'rubygems')
md5sums=()
optdepends=('subtle: subtle internal commands'
            'dmenu-xft: xft font support')
_gitroot="git://github.com/supasnashbuhl/dynmenu.git"
_gitname="dynmenu"

build() {
    cd "$srcdir"
    msg "Connecting to GIT server...."

    if [[ -d "$_gitname" ]]; then
      cd "$_gitname" && git pull origin
      msg "The local files are updated."
    else
      git clone "$_gitroot" "$_gitname"
    fi

    msg "GIT checkout done or server timeout"
    msg "Starting build"

    rm -rf "$srcdir/$_gitname-build"
    git clone "$srcdir/$_gitname" "$srcdir/$_gitname-build"
    cd "$srcdir/$_gitname-build"
    gem build $_gitname.gemspec
}

package() {
  cd "$srcdir/$_gitname-build"
  # _gemdir is defined inside package() because if ruby[gems] is not installed on
  # the system, makepkg will exit with an error when sourcing the PKGBUILD.
  local _gemdir="$(ruby -rubygems -e'puts Gem.default_dir')"

  gem install --no-user-install --ignore-dependencies -i "$pkgdir$_gemdir" -n "$pkgdir/usr/bin" \
    "$_gitname-$pkgver.gem"
}

# vim:set ts=2 sw=2 et:
