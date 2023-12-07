# This package drops in the configuration and systemd unit
# files that you need to make pipewire run headless (outside
# of the context of a user session, aka "system mode")
#
# 2023-12-04 M. Dickerson <pomonamikey@gmail.com>

pkgname="pipewire-headless"
pkgver="20231204.01"
pkgrel="12"
pkgdesc="Configuration and unit files for headless pipewire"
arch=("any")
url="https://pipewire.org/"
license=("MIT")
#provides=("mongodb=$pkgver")
#conflicts=("mongodb" "mongodb-bin")
depends=("pipewire" "wireplumber" "pipewire-pulse")
makedepends=()
source=(
  "headless.conf"
  "pipewire.service"
  "pipewire.socket"
  "wireplumber.service"
  "000-functions.lua"
  "020-default-access.lua"
  "030-alsa-monitor.lua"
  "030-libcamera-monitor.lua"
  "030-v4l2-monitor.lua"
  "040-device-defaults.lua"
  "040-stream-defaults.lua"
  "050-alsa-config.lua"
  "050-default-access-config.lua"
  "050-libcamera-config.lua"
  "050-v4l2-config.lua"
  "090-enable-all.lua"
  "110-default-policy.lua"
  "150-endpoints-config.lua"
  "190-enable-all.lua"
  "230-bluez-midi-monitor.lua"
  "230-bluez-monitor.lua"
  "250-bluez-config.lua"
  "250-bluez-midi-config.lua"
  "290-enable-all.lua"
  "systemd-sysuser.conf"
  "10-disable-dbus.conf"
  "20-rtp-source.conf"
  "systemd-tmpfile.conf"
  "pipewire-pulse.service"
  "pipewire-pulse.socket"
  "pipewire-pulse.conf"
)

sha256sums=(
"7301cff314c1ad54aff12e2c335d89b9b0408f5a558d182f825776a077bb6b1b"
"a9346afad15e29f8975e7beb85689130f5ab27d1cc9bd4ff05dc8163cf3fd30a"
"7226878c5d658d32b70b0fd1cf41706e6e25645834639862f3c5292968b20780"
"71629a9ac4566c5fed7bd1c6c69bf14c4ec790e7f004e135d33f2527282d9491"
"887403a1443ae33c22b7c6a1d9fc35e7104576c4f592cb7040b45f9ac998bf48"
"526a23059c0f218e6067f0d0ba94073ebbaeb9095981d992ddb2cabd2654ce90"
"5bd8793ebdd98aaddd86613a5cdb7c0c66ee9a6f0c708899f29e213922f1fa3e"
"a89665bd9cb22d013a601f176c2e6095eceadc9f88e0363927534ce1c732cbbf"
"aeda7eb6cecd43843154c4a59dd6b8d2d7764d8c6fdea6261b18fcd83bfa7846"
"e3d197a0d60323a855475a51bfda1b708c4004e622653f7526c7f5b4e15cf8d2"
"16956deb4cffa09f6d1fad1cffca9af32871dfb2f9d22c5ed157cbaf64bfc24a"
"aa6f4bb9e0eb344ed1f0899c19419f87ac0ea210460a333548c8d36c63fc4b93"
"4aa0e7032d595581b1352b276c19b15f119fbe42ab9845aa85e9f0bc0120341c"
"5f3d70f43b7341ccbbd99ce85ee834061babd91fbfdc1f2cfdca24584a93042b"
"01cba116c52c5819c96d0383bcf034de1088ec1da71a395b72ad028f56fa534b"
"86888e9d3fcc952c41e778ab4edae4a0eb1f9f51b62ae0772befa9f0fdef611d"
"e2ed20b7791671f5e516f7195dc68e706230ce99ad375751e8a3ad20693b07e4"
"f06d5c83042aca119a973f6962300adc27cdecbfe1483715899484f220f01437"
"8cfbbeca2965606607eaff573bdf5cf6a98006ff4b2ad4559d387184407750db"
"c02b30c28f7f22363f4d28934ee9b3a087dd4746030897b4fccf824f1a1c163e"
"7707bc53cdb081d026f5b08a67d0b12de5359302150e1910e875f62329afa2e0"
"d1cc910d9a370e6b070278d6aa15df6225a630b8bca7c3d3d44e43f51d9cee5c"
"6e24071ea010805570c12a0da76b9a58ae0ce68feedef76056d0920b801c0e0c"
"64171c18c3b483fc705e832b79a2d6f080053eec02b89bbe664680a224ff14db"
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
  mkdir -p "${pkgdir}/etc/wireplumber/headless.lua.d"
  install -Dm755 "${srcdir}/headless.conf" \
    "${pkgdir}/etc/wireplumber"
  install -Dm755 ${srcdir}/*.lua \
    "${pkgdir}/etc/wireplumber/headless.lua.d"
  install -Dm755 -t "${pkgdir}/etc/pipewire/pipewire.conf.d" \
    "${srcdir}/10-disable-dbus.conf" \
    "${srcdir}/20-rtp-source.conf"
  install -Dm755 "${srcdir}/pipewire-pulse.conf" \
    "${pkgdir}/etc/pipewire/pipewire-pulse.conf.d/10-disable-dbus.conf"
  install -Dm755 -t "${pkgdir}/etc/systemd/system" \
    "${srcdir}/pipewire.service" \
    "${srcdir}/pipewire.socket" \
    "${srcdir}/wireplumber.service" \
    "${srcdir}/pipewire-pulse.service" \
    "${srcdir}/pipewire-pulse.socket"
}
