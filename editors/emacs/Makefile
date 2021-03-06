# Created by: MANTANI Nobutaka <nobutaka@nobutaka.com>
# $FreeBSD$

PORTNAME=	emacs
PORTVERSION=	${EMACS_VER}
PORTREVISION=	4
PORTEPOCH=	3
CATEGORIES=	editors ipv6
MASTER_SITES=	GNU

MAINTAINER=	emacs@FreeBSD.org
COMMENT=	GNU editing macros

LICENSE=	GPLv3+
LICENSE_FILE=	${WRKSRC}/COPYING

BROKEN_aarch64=	Fails to link: missing sbrk
CONFLICTS_INSTALL=	emacs-devel emacs-devel_nox

USE_HARDENING=	pie:off relro:off

FLAVORS=		full canna nox
full_CONFLICTS_INSTALL=	emacs-canna emacs-nox
canna_CONFLICTS_INSTALL=	emacs emacs-nox
canna_PKGNAMESUFFIX=	-canna
canna_DESCR=		${.CURDIR}/pkg-descr-canna
canna_LIB_DEPENDS=	libcanna.so:japanese/canna-lib
nox_CONFLICTS_INSTALL=	emacs emacs-canna
nox_PKGNAMESUFFIX=	-nox

USES=		cpe gmake localbase:ldflags makeinfo ncurses pkgconfig tar:xz
CPE_VENDOR=	gnu

GNU_CONFIGURE=	yes
CONFIGURE_ARGS=	--localstatedir=/var \
		--with-gameuser=games:games
CONFIGURE_ENV=	ac_cv_header_sys_sysinfo_h=no \
		ac_cv_prog_liblockfile=no
INFO=		ada-mode auth autotype bovine calc ccmode cl dbus dired-x \
		ebrowse ede ediff edt efaq eieio eintr elisp emacs emacs-gnutls \
		emacs-mime epa erc ert eshell eudc eww flymake forms gnus \
		htmlfontify idlwave ido info mairix-el message mh-e newsticker \
		nxml-mode octave-mode org pcl-cvs pgg rcirc reftex remember \
		sasl sc semantic ses sieve smtpmail speedbar srecode todo-mode \
		tramp url vhdl-mode vip viper widget wisent woman
INFO_PATH=	${DATADIR_REL}/info
PLIST_SUB=	EMACS_VER=${EMACS_VER} GNU_HOST=${CONFIGURE_TARGET}
SUB_FILES=	sources.el
SUB_LIST=	ARCHLIBDIR=${PREFIX}/libexec/emacs/${EMACS_VER}/${CONFIGURE_TARGET} \
		EMACS_VER=${EMACS_VER} # sources.el

OPTIONS_DEFINE=	ACL DBUS GCONF GNUTLS GSETTINGS LLDB M17N MAILUTILS MODULES OTF \
		SCROLLBARS SOURCES XFT XIM XML XWIDGETS
OPTIONS_DEFAULT=	ACL DBUS GCONF GIF GNUTLS GSETTINGS GTK3 JPEG KQUEUE \
		M17N MAGICK MODULES OSS OTF PNG SCROLLBARS SOURCES SVG \
		TIFF XFT XIM XML XPM
OPTIONS_SUB=	YES
OPTIONS_GROUP=	GRAPHICS
OPTIONS_GROUP_GRAPHICS=	CAIRO GIF JPEG MAGICK PNG SVG TIFF XPM
OPTIONS_RADIO=	FILENOTIFY SOUND X11TOOLKIT
OPTIONS_RADIO_FILENOTIFY=	GFILE KQUEUE
OPTIONS_RADIO_SOUND=	ALSA OSS
OPTIONS_RADIO_X11TOOLKIT=	GTK2 GTK3 MOTIF XAW XAW3D

ACL_DESC=	Access control list support
CAIRO_DESC=	Experimental Cairo library support     (implies PNG, XFT)
FILENOTIFY_DESC=	File notification support
GFILE_DESC=	File notification via gfile
GRAPHICS_DESC=	Graphics support
GSETTINGS_DESC=	GSettings API for application settings
KQUEUE_DESC=	File notification via kqueue
LLDB_DESC=	LLDB support for GUD
#LTO_DESC=	Enable link-time optimization
MAGICK_DESC=	ImageMagick image processing support
MAILUTILS_DESC=	Mail framework via GNU Mailutils
M17N_DESC=	M17N for text-shaping                  (implies XFT)
MODULES_DESC=	Dynamic modules support
OTF_DESC=	Opentype fonts                         (implies XFT)
SCROLLBARS_DESC=	Toolkit scroll-bars
SOURCES_DESC=	Install sources
SVG_DESC=	Scalable vector graphics support       (implies PNG)
X11TOOLKIT_DESC=	X11 toolkit
XAW3D_DESC=	Athena3D widgets
XAW_DESC=	Athena widgets
XIM_DESC=	X Input Method
XWIDGETS_DESC=	GTK widgets in Emacs buffers           (requires GTK3)

ACL_CONFIGURE_ENABLE=	acl
ALSA_CONFIGURE_ON=	--with-sound=alsa
ALSA_LIB_DEPENDS=	libasound.so:audio/alsa-lib
CAIRO_USE=		GNOME=cairo
CAIRO_CONFIGURE_WITH=	cairo
CAIRO_IMPLIES=		PNG XFT
DBUS_LIB_DEPENDS=	libdbus-1.so:devel/dbus
DBUS_CONFIGURE_WITH=	dbus
GCONF_USE=		GNOME=gconf2
GCONF_CONFIGURE_WITH=	gconf
GFILE_CONFIGURE_ON=	--with-file-notification=gfile
GIF_LIB_DEPENDS=	libgif.so:graphics/giflib
GIF_CONFIGURE_WITH=	gif
GNUTLS_LIB_DEPENDS=	libgnutls.so:security/gnutls
GNUTLS_CONFIGURE_WITH=	gnutls
GSETTINGS_USE=		GNOME=glib20
GSETTINGS_CONFIGURE_WITH=	gsettings
GSETTINGS_IMPLIES=	DBUS
GTK2_USE=		GNOME=cairo,gtk20
GTK2_USES=		gettext-runtime
GTK2_CONFIGURE_ON=	--with-x-toolkit=gtk2
GTK2_LIB_DEPENDS=	libfreetype.so:print/freetype2 \
			libfontconfig.so:x11-fonts/fontconfig
GTK3_USE=		GNOME=cairo,gtk30
GTK3_USES=		gettext-runtime
GTK3_CONFIGURE_ON=	--with-x-toolkit=gtk3
JPEG_USES=		jpeg
JPEG_CONFIGURE_WITH=	jpeg
KQUEUE_CONFIGURE_ON=	--with-file-notification=kqueue
LLDB_EXTRA_PATCHES=	${PATCHDIR}/extrapatch-lldb-gud.el
#LTO_CONFIGURE_ON=	--enable-link-time-optimization
M17N_LIB_DEPENDS=	libm17n.so:devel/m17n-lib
M17N_CONFIGURE_WITH=	m17n-flt
MAGICK_LIB_DEPENDS=	libMagickCore-6.so:graphics/ImageMagick
MAGICK_CONFIGURE_WITH=	imagemagick
MAILUTILS_CONFIGURE_WITH=	mailutils
MAILUTILS_LIB_DEPENDS=	libmailutils.so:mail/mailutils
MODULES_CONFIGURE_WITH=	modules
MOTIF_USES=		motif
MOTIF_CONFIGURE_ON=	--with-x-toolkit=motif
MOTIF_LIB_DEPENDS=	libXp.so:x11/libXp
OSS_CONFIGURE_ON=	--with-sound=oss
OTF_LIB_DEPENDS=	libotf.so:print/libotf
OTF_CONFIGURE_WITH=	libotf
PNG_LIB_DEPENDS=	libpng.so:graphics/png
PNG_CONFIGURE_WITH=	png
SCROLLBARS_CONFIGURE_WITH=	toolkit-scroll-bars
SVG_USE=		GNOME=cairo,librsvg2
SVG_CONFIGURE_WITH=	rsvg
SVG_IMPLIES=		PNG
SVG_USES=		gettext-runtime
TIFF_LIB_DEPENDS=	libtiff.so:graphics/tiff
TIFF_CONFIGURE_WITH=	tiff
XAW_USE=		XORG=xaw
XAW_CONFIGURE_ON=	--with-x-toolkit=athena --without-xaw3d
XAW3D_LIB_DEPENDS=	libXaw3d.so:x11-toolkits/Xaw3d
XAW3D_CONFIGURE_ON=	--with-x-toolkit=athena
XFT_USE=		XORG=xft,xrender
XFT_CONFIGURE_WITH=	xft
XFT_LIB_DEPENDS=	libfontconfig.so:x11-fonts/fontconfig \
			libfreetype.so:print/freetype2
XIM_CONFIGURE_WITH=	xim
XML_USE=		GNOME=libxml2
XML_CONFIGURE_WITH=	xml2
XPM_USE=		XORG=xpm
XPM_CONFIGURE_WITH=	xpm
XWIDGETS_USE=		XORG=xcomposite
XWIDGETS_CONFIGURE_WITH=	xwidgets
XWIDGETS_LIB_DEPENDS=	libwebkitgtk-3.0.so:www/webkit-gtk3
XWIDGETS_IMPLIES=	GTK3

.if ${FLAVOR:U} == canna
CONFIGURE_ARGS+=	--with-canna
PATCH_DIST_STRIP=	-p1
PATCH_SITES=		http://www.gentei.org/~yuuji/software/emacs25canna/ \
			http://distfiles.pirateparty.in/ashish/ \
			LOCAL/ashish
PATCHFILES=		emacs25.2canna-20170507.diff.gz
PLIST_FILES+=		${DATADIR}/${EMACS_VER}/lisp/canna.el.gz \
			${DATADIR}/${EMACS_VER}/lisp/canna.elc \
			${DATADIR}/${EMACS_VER}/lisp/isearch-ext.el.gz \
			${DATADIR}/${EMACS_VER}/lisp/isearch-ext.elc
SOURCES_PLIST_FILES=	${DATADIR}/${EMACS_VER}/src/canna.c
.endif
.if ${FLAVOR:U} == nox
CONFIGURE_ARGS+=	--with-sound=no --without-cairo --without-dbus \
			--without-gconf --without-gif --without-gsettings \
			--with-x-toolkit=no --without-jpeg --without-m17n-flt \
			--without-imagemagick --without-libotf --without-png \
			--without-toolkit-scroll-bars --without-rsvg \
			--without-tiff --without-x --without-xim --without-xpm \
			--without-xwidgets
OPTIONS_EXCLUDE=	ALSA CAIRO DBUS GCONF GIF GSETTINGS GTK2 GTK3 JPEG \
			M17N MAGICK MOTIF OSS OTF PNG SCROLLBARS SVG TIFF XAW \
			XAW3D XFT XIM XPM XWIDGETS
.else
CONFIGURE_ARGS+=	--with-x
INSTALLS_ICONS=		yes
USE_XORG=		ice sm x11 xcb xext xfixes xinerama xmu xrandr xt
USES+=			desktop-file-utils
.endif

EMACS_VER=	25.3

.include <bsd.port.options.mk>

# has graphics/ImageMagick been compiled with OPENMP?
.if ${PORT_OPTIONS:MMAGICK} && ${:!${GREP} -sc " \-fopenmp " ${LOCALBASE}/libdata/pkgconfig/ImageMagick.pc || true!} == "1"
USES+=	compiler:openmp
.endif

# With a desktop entry stage-qa will give a warning about requiring
# desktop-file-utils and portlint -C will give a warning about INSTALL_ICONS,
# but don't pull in those dependencies with the nox flavor.
.if ${FLAVOR} == nox
post-patch:
	@${REINPLACE_CMD} -e 's/^Terminal=.*$$/Terminal=true/' ${WRKSRC}/etc/emacs.desktop
.endif

post-install-SOURCES-on:
	@${MKDIR} ${STAGEDIR}${DATADIR}/${EMACS_VER}/src
	${INSTALL_DATA} ${WRKSRC}/src/*.[ch] ${STAGEDIR}${DATADIR}/${EMACS_VER}/src
	${INSTALL_DATA} ${WRKDIR}/sources.el ${STAGEDIR}${DATADIR}/${EMACS_VER}/site-lisp/site-start.el

.include <bsd.port.mk>
