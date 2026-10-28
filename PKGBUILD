# Maintainer: devalexandre <alexandre@dev2learn.com>
# Metapackage: installs the whole Lingmo desktop (Qt 6) in one go.
pkgname=lingmo-desktop
pkgver=1.3.1
pkgrel=1
pkgdesc="Lingmo desktop environment (Qt 6): session, shell, apps, themes and login screen"
arch=('any')
url="https://github.com/ArchLingmo/lingmo-desktop"
license=('GPL-3.0-or-later')
depends=(
    # Libraries and platform integration
    'LingmoUI' 'liblingmo' 'lingmo-qt-plugins'
    # App actions shared by the apps, the Assistant, Flows and Spotlight (Lingmo Intents: ~0.8 MiB installed)
    'lingmo-intents'
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
    # Compressed swap in RAM: keeps the desktop alive when AI models or the Studio fill the
    # memory (Lingmo ships the config below)
    'zram-generator'
    # Podcast dubbing with each speaker's voice (~1 MiB; the voice engine installs on first use)
    'lingmo-podcast'
    # Live translation: subtitles, dubbed listening, translator microphone (~1 MiB installed;
    # whisper-cpp/espeak-ng already come with lingmo-assistant; models download on first use)
    'lingmo-translate'
    # Voice Studio: voices, reading aloud (the Reader's "Ouvir"), language learning and
    # dictation in any app with Meta+H (~2 MiB installed; piper-tts/espeak-ng/whisper-cpp
    # already come with the Assistant and live translation; models download on first use)
    'lingmo-voicestudio'
    # Tutor for children: ask by voice, text, photo or PDF; math checked by SymPy; parents' PIN (~1 MiB;
    # python-sympy + mpmath ~110 MiB; tesseract/whisper-cpp/espeak-ng already come with other apps)
    'lingmo-tutor'
    # Ações de arquivo: convert by dragging a file and tapping Shift/Ctrl/Alt (FileAction, MIT). The engine is
    # ~74 MiB installed (ImageMagick, PDFium, Skia bundled) + Arch's dotnet-runtime ~74 MiB; ffmpeg already comes
    # with other apps. Pandoc/LibreOffice stay optional (their slices show as "precisa de …")
    'lingmo-fileaction' 'lingmo-fileaction-engine' 'dotnet-runtime' 'ffmpeg'
)
# The [archlingmo] servers in a mirror list of their own: the repo moves to the ArchLingmo
# organisation and systems installed earlier switch to it here (lingmo-desktop.install)
backup=('etc/pacman.d/archlingmo-mirrorlist')
install=lingmo-desktop.install
optdepends=(
    'konsole: KDE terminal'
    'flameshot: screenshots (bind it to Print in Settings > Shortcuts)'
    'networkmanager: network and VPN in the status bar'
    'bluez: Bluetooth settings'
)

# Lingmo's default apps per file type (owned here, not by any single app)
package() {
    # New home first; the old address stays as a fallback while both are published
    install -Dm644 /dev/stdin "$pkgdir/etc/pacman.d/archlingmo-mirrorlist" <<'EOF'
# ArchLingmo package servers ([archlingmo] in /etc/pacman.conf includes this file)
Server = https://archlingmo.github.io/archlingmo-repo/$arch
Server = https://devalexandre.github.io/archlingmo-repo/$arch
EOF
    # zram swap for every Lingmo system: half the RAM (at most 8 GiB), zstd. An admin's
    # /etc/systemd/zram-generator.conf overrides it.
    install -Dm644 /dev/stdin "$pkgdir/usr/lib/systemd/zram-generator.conf" <<'EOF'
[zram0]
zram-size = min(ram / 2, 8192)
compression-algorithm = zstd
swap-priority = 100
EOF
    # Kernel settings for swap on zram (the ArchWiki/Pop!_OS values)
    install -Dm644 /dev/stdin "$pkgdir/usr/lib/sysctl.d/99-lingmo-zram.conf" <<'EOF'
vm.swappiness = 180
vm.watermark_boost_factor = 0
vm.watermark_scale_factor = 125
vm.page-cluster = 0
EOF
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
HOME_URL="https://archlingmo.github.io/"
BLOG_URL="https://archlingmo.github.io/#/blog/silicio"
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
# Music and podcasts: the player (Dublador de Podcasts is only offered in "Abrir com")
audio/mpeg=lingmo-videoplayer.desktop
audio/mp4=lingmo-videoplayer.desktop
audio/x-m4a=lingmo-videoplayer.desktop
audio/aac=lingmo-videoplayer.desktop
audio/ogg=lingmo-videoplayer.desktop
audio/x-vorbis+ogg=lingmo-videoplayer.desktop
audio/opus=lingmo-videoplayer.desktop
audio/flac=lingmo-videoplayer.desktop
audio/wav=lingmo-videoplayer.desktop
audio/x-wav=lingmo-videoplayer.desktop
audio/webm=lingmo-videoplayer.desktop
audio/x-matroska=lingmo-videoplayer.desktop
audio/x-ms-wma=lingmo-videoplayer.desktop
audio/x-aiff=lingmo-videoplayer.desktop
# Documents
application/pdf=lingmo-reader.desktop
application/x-pdf=lingmo-reader.desktop
EOF
}
