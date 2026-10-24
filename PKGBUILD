# Maintainer: devalexandre <alexandre@dev2learn.com>
# Metapackage: installs the whole Lingmo desktop (Qt 6) in one go.
pkgname=lingmo-desktop
pkgver=1.3.1
pkgrel=1
pkgdesc="Lingmo desktop environment (Qt 6): session, shell, apps, themes and login screen"
arch=('any')
url="https://github.com/devalexandre/lingmo-desktop"
license=('GPL-3.0-or-later')
depends=(
    # Libraries and platform integration
    'LingmoUI' 'liblingmo' 'lingmo-qt-plugins'
    # Session, shell and window manager integration
    'lingmo-core' 'lingmo-statusbar' 'lingmo-dock' 'lingmo-launcher'
    'lingmo-filemanager' 'lingmo-settings' 'lingmo-spotlight' 'lingmo-kwin-plugins'
    # Look and feel (lingmo-systemicons: the Lingmo icon theme, which pulls WhiteSur)
    'lingmo-systemicons' 'lingmo-artwork' 'lingmo-wallpapers'
    'lingmo-cursor-themes' 'lingmo-gtk-themes'
    # Login screen and display server
    'lingmo-sddm-theme' 'sddm' 'xorg-server'
    # Global menu for GTK apps (lingmo-gmenuproxy loads it through gtk-modules)
    'appmenu-gtk-module'
    # Apps
    'lingmo-terminal' 'lingmo-texteditor' 'lingmo-calculator'
    'lingmo-screenshots' 'lingmo-screenlocker' 'lingmo-videoplayer'
    'lingmo-updater' 'lingmo-welcome' 'lingmo-store' 'lingmo-winrun'
    'lingmo-clock' 'lingmo-widgets' 'lingmo-optimizer' 'lingmo-imagewriter'
    'lingmo-automator' 'lingmo-mail' 'lingmo-assistant' 'lingmo-photos' 'lingmo-reader'
    # Virtual camera with auto framing, background blur and face unlock (pulls
    # v4l2loopback-dkms + linux-headers to build the module: ~68 MiB download)
    'lingmo-camera'
    # Video editor (pulls mlt, frei0r-plugins, vid.stab: ~15 MiB installed)
    'lingmo-studio'
    # Keyboard and mouse shared between PCs (pulls deskflow: ~5 MiB installed)
    'lingmo-continuity'
    # Phone and devices (pulls kdeconnect: ~27 MiB installed, ~6.5 MiB download)
    'lingmo-share'
)
optdepends=(
    'konsole: KDE terminal'
    'flameshot: screenshots (bind it to Print in Settings > Shortcuts)'
    'networkmanager: network and VPN in the status bar'
    'bluez: Bluetooth settings'
)

# Lingmo's default apps per file type (owned here, not by any single app)
package() {
    install -Dm644 /dev/stdin "$pkgdir/etc/lingmo-release" <<'EOF'
NAME="ArchLingmo"
VERSION="2026.11"
PRETTY_NAME="ArchLingmo Silício"
VERSION_CODENAME=silicon
CODENAME_PRETTY="Silício"
CODENAME_PT="Silício"
CODENAME_EN="Silicon"
ELEMENT_SYMBOL=Si
ELEMENT_NUMBER=14
HOME_URL="https://devalexandre.github.io/archlingmo/"
BLOG_URL="https://devalexandre.github.io/archlingmo/#/blog/silicio"
EOF
    install -Dm644 /dev/stdin "$pkgdir/usr/share/applications/lingmo-mimeapps.list" <<'EOF'
# Default applications for Lingmo sessions (XDG_CURRENT_DESKTOP=Lingmo),
# read by xdg-open, GIO and KService after ~/.config/mimeapps.list:
# the user's own choices always win.
[Default Applications]
# Programs and installers from outside the Arch repositories: isolated boxes
application/x-ms-dos-executable=lingmo-winrun.desktop
application/x-msdownload=lingmo-winrun.desktop
application/x-dosexec=lingmo-winrun.desktop
application/vnd.microsoft.portable-executable=lingmo-winrun.desktop
application/x-ms-ne-executable=lingmo-winrun.desktop
application/x-msi=lingmo-winrun.desktop
application/x-ms-shortcut=lingmo-winrun.desktop
application/vnd.debian.binary-package=lingmo-winrun.desktop
application/x-rpm=lingmo-winrun.desktop
application/vnd.appimage=lingmo-winrun.desktop
application/x-iso9660-appimage=lingmo-winrun.desktop
application/vnd.android.package-archive=lingmo-winrun.desktop
# Pictures
image/jpeg=lingmo-photos.desktop
image/pjpeg=lingmo-photos.desktop
image/png=lingmo-photos.desktop
image/apng=lingmo-photos.desktop
image/webp=lingmo-photos.desktop
image/gif=lingmo-photos.desktop
image/bmp=lingmo-photos.desktop
image/x-bmp=lingmo-photos.desktop
image/x-ms-bmp=lingmo-photos.desktop
image/tiff=lingmo-photos.desktop
image/avif=lingmo-photos.desktop
image/heic=lingmo-photos.desktop
image/heif=lingmo-photos.desktop
image/jxl=lingmo-photos.desktop
image/svg+xml=lingmo-photos.desktop
image/svg+xml-compressed=lingmo-photos.desktop
image/x-tga=lingmo-photos.desktop
image/x-portable-pixmap=lingmo-photos.desktop
image/qoi=lingmo-photos.desktop
# Documents
application/pdf=lingmo-reader.desktop
application/x-pdf=lingmo-reader.desktop
EOF
}
