# This package drops in the configuration and systemd unit
# files that you need to make pipewire run headless (outside
# of the context of a user session, aka "system mode")
#
# 2023-12-04 M. Dickerson <pomonamikey@gmail.com>

pkgname="pipewire-headless"
pkgver="20240902.01"
pkgrel="13"
pkgdesc="Configuration and unit files for headless pipewire"
arch=("any")
url="https://pipewire.org/"
license=("MIT")
#provides=("mongodb=$pkgver")
#conflicts=("mongodb" "mongodb-bin")
depends=("pipewire" "wireplumber>=0.5" "pipewire-pulse")
makedepends=()
source=(
  "headless.conf"
  "pipewire.service"
  "pipewire.socket"
  "wireplumber.service"
  "systemd-sysuser.conf"
  "10-disable-dbus.conf"
  "20-rtp-source.conf"
  "systemd-tmpfile.conf"
  "pipewire-pulse.service"
  "pipewire-pulse.socket"
  "pipewire-pulse.conf"
)

sha256sums=(
"6e3a25a3f3edec6c24a7c49a7f98bdb4b2d5d64c05fec773afe35940a84568a9"
"a9346afad15e29f8975e7beb85689130f5ab27d1cc9bd4ff05dc8163cf3fd30a"
"7226878c5d658d32b70b0fd1cf41706e6e25645834639862f3c5292968b20780"
"71629a9ac4566c5fed7bd1c6c69bf14c4ec790e7f004e135d33f2527282d9491"
"bac23531378f7e894a89460e5a0bad2aeb25f28440801142d1e3faa61f940492"
"28c7076af7747b27c9c6057353a6b91fb081e845e8aa2c195ff939bf2702b6bc"
"759f5ca6475b7c4d34e612afcdfa2e56fd797ab07e2aadf0f359327bd662e716"
"5653d3555b6ef7ab8266949060d0837b8abb1efb8b44da664b0cc306de3320cd"
"e6fcde6cdb45ad087688b3840ec75091ffc06fac6619f3dd2ffd00943a89dcc6"
"185bf5a11cf458ad934422059f889a8a79ba02b21e2c8b3a2a38d4cfb0caf64f"
"f280c97dd6a487cb4594debe9aabc0a2fabbcb69feb16491275d013955e1b16d"
)

#backup=("etc/mongodb.conf")

prepare() {
  /bin/true
}

build() {
  /bin/true
}

package() {
  install -Dm755 "${srcdir}/systemd-sysuser.conf" \
    "${pkgdir}/usr/lib/sysusers.d/pipewire.conf" 
  install -Dm755 "${srcdir}/systemd-tmpfile.conf" \
    "${pkgdir}/usr/lib/tmpfiles.d/pipewire.conf"
  mkdir -p ${pkgdir}/etc/wireplumber
  install -Dm644 "${srcdir}/headless.conf" \
    "${pkgdir}/etc/wireplumber"
  install -Dm755 -t "${pkgdir}/etc/pipewire/pipewire.conf.d" \
    "${srcdir}/10-disable-dbus.conf" \
    "${srcdir}/20-rtp-source.conf"
  install -Dm644 "${srcdir}/pipewire-pulse.conf" \
    "${pkgdir}/etc/pipewire/pipewire-pulse.conf.d/10-disable-dbus.conf"
  install -Dm755 -t "${pkgdir}/etc/systemd/system" \
    "${srcdir}/pipewire.service" \
    "${srcdir}/pipewire.socket" \
    "${srcdir}/wireplumber.service" \
    "${srcdir}/pipewire-pulse.service" \
    "${srcdir}/pipewire-pulse.socket"
}
