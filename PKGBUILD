# Contributor: Miguel Aguilar <zodiac_es@yahoo.es

pkgname=fbht-git
pkgver=r40.33248f0
pkgrel=4
pkgdesc="A Facebook Hacking Tool"
arch=('any')
url='https://github.com/chinoogawa/fbht'
license=('custom')
depends=('python2' 'python2-mechanize' 'python2-networkx' 'python2-matplotlib' 
         'python2-numpy' 'python2-simplejson' 'python2-pygraphviz')
makedepends=('git')
provides=('fbht')
conflicts=('fbht')
source=("git+https://github.com/chinoogawa/fbht.git")
md5sums=('SKIP')

pkgver() {
  cd "$srcdir/fbht"
  printf "r%s.%s" "$(git rev-list --count HEAD)" "$(git rev-parse --short HEAD)"
}


prepare(){
  grep -iRl 'python' "$srcdir/fbht" | xargs sed -i 's|#!.*/usr/bin/python|#!/usr/bin/python2|;s|#!.*/usr/bin/env python$|#!/usr/bin/env python2|'
}

package() {
  cd "$srcdir/fbht"

  # Make base directories.
  install -dm755 "$pkgdir/usr/share/fbht"
  install -dm755 "$pkgdir/usr/bin"

  # Licenes and docs
  install -dm755 "$pkgdir/usr/share/fbht/dumps"
  install -dm755 "$pkgdir/usr/share/fbht/logs"
  install -Dm644 "License" "$pkgdir/usr/share/fbht/"
  install -D -m644 License "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE"
  install -Dm644 "README.md" "$pkgdir/usr/share/fbht/"
  cp -a --no-preserve=ownership dumps/* "$pkgdir/usr/share/fbht/dumps/"
  cp -a --no-preserve=ownership logs/* "$pkgdir/usr/share/fbht/logs/"

  #Bin
  install -m755 {MyParser,community,database,handlers,main,mainFunc,mainLib}.py "$pkgdir/usr/share/fbht/"
  install -m644 "fb_db.db" "$pkgdir/usr/share/fbht/"
 
cat > "$pkgdir/usr/bin/fbht" << EOF
#!/bin/sh
cd /usr/share/fbht
python2 main.py "\$@"
EOF

chmod +x "$pkgdir/usr/bin/fbht"

}
