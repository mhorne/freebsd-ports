# $FreeBSD$

PORTNAME=	electron
DISTVERSIONPREFIX=	v
DISTVERSION=	${ELECTRON_VER:S/-beta./.b/}
CATEGORIES=	devel java
MASTER_SITES=	https://commondatastorage.googleapis.com/chromium-browser-official/:chromium_official \
		https://commondatastorage.googleapis.com/chromium-nodejs/:chromium_node \
		https://commondatastorage.googleapis.com/chromium-fonts/:chromium_testfonts
PKGNAMESUFFIX=	${ELECTRON_VER_MAJOR}
DISTFILES=	chromium-${CHROMIUM_OFFICIAL_VER}${EXTRACT_SUFX}:chromium_official \
		${CHROMIUM_NODE_MODULES_HASH}:chromium_node \
		${CHROMIUM_TEST_FONTS_HASH}:chromium_testfonts \
		electron-yarn-cache-${ELECTRON_VER}${EXTRACT_SUFX}:prefetch
DIST_SUBDIR=	${PORTNAME}

MAINTAINER=	tagattie@FreeBSD.org
COMMENT=	Build cross-platform desktop apps with JavaScript, HTML, and CSS

LICENSE=	MIT
LICENSE_FILE=	${WRKSRC}/electron/LICENSE

FETCH_DEPENDS=		yarn-node12>0:www/yarn-node12
EXTRACT_DEPENDS=	yarn-node12>0:www/yarn-node12
PATCH_DEPENDS=		git:devel/git
BUILD_DEPENDS=		${LOCALBASE}/bin/ar:devel/binutils \
			gperf:devel/gperf \
			yasm:devel/yasm \
			${LOCALBASE}/include/linux/videodev2.h:multimedia/v4l_compat \
			node12>0:www/node12 \
			npm-node12>0:www/npm-node12
LIB_DEPENDS=		libatk-bridge-2.0.so:accessibility/at-spi2-atk \
			libatspi.so:accessibility/at-spi2-core \
			libsnappy.so:archivers/snappy \
			libFLAC.so:audio/flac \
			libopus.so:audio/opus \
			libdbus-1.so:devel/dbus \
			libnotify.so:devel/libnotify \
			libpci.so:devel/libpci \
			libnspr4.so:devel/nspr \
			libre2.so:devel/re2 \
			libdrm.so:graphics/libdrm \
			libpng.so:graphics/png \
			libwebp.so:graphics/webp \
			libavcodec.so:multimedia/ffmpeg \
			libopenh264.so:multimedia/openh264 \
			libfreetype.so:print/freetype2 \
			libharfbuzz.so:print/harfbuzz \
			libsecret-1.so:security/libsecret \
			libnss3.so:security/nss \
			libexpat.so:textproc/expat2 \
			libxkbcommon.so:x11/libxkbcommon \
			libfontconfig.so:x11-fonts/fontconfig
RUN_DEPENDS=		xdg-open:devel/xdg-utils
TEST_DEPENDS=		git:devel/git \
			${PYTHON_PKGNAMEPREFIX}python-dbusmock>0:devel/py-python-dbusmock@${PY_FLAVOR} \
			npm-node12>0:www/npm-node12

USES=		bison dos2unix gettext-tools gl gnome jpeg localbase:ldflags \
		ninja pkgconfig python:2.7,build,test shebangfix tar:xz xorg
DOS2UNIX_FILES=	third_party/skia/third_party/vulkanmemoryallocator/include/vk_mem_alloc.h
USE_GITHUB=	yes
GH_TAGNAME=	${DISTVERSIONPREFIX}${ELECTRON_VER}
GH_TUPLE=	nodejs:node:v${NODE_VER}:node \
		nodejs:nan:${NAN_VER}:nan
USE_GL=		gl glesv2
USE_GNOME=	atk cairo gdkpixbuf2 gtk30 libxml2 libxslt pango
USE_JAVA=	yes
JAVA_VERSION=	1.8
JAVA_BUILD=	yes
USE_LDCONFIG=	${DATADIR}
USE_XORG=	x11 xcb xcomposite xcursor xdamage xext xfixes xi xrandr \
		xrender xscrnsaver xtst

SHEBANG_FILES=	buildtools/freebsd/clang-format

MAKE_ARGS=			-C out/${BUILDTYPE}
MAKE_ENV+=			C_INCLUDE_PATH=${LOCALBASE}/include \
				CPLUS_INCLUDE_PATH=${LOCALBASE}/include
ALL_TARGET=			electron third_party/electron_node:headers
POST_BUILD_TARGETS=		licenses version
POST_BUILD_DIST_TARGETS=	electron_dist_zip electron_chromedriver_zip \
				electron_mksnapshot_zip

DATADIR=	${PREFIX}/share/${PORTNAME}${PKGNAMESUFFIX}
BINARY_ALIAS=	python=${PYTHON_CMD}

NO_WRKSUBDIR=	yes
WRKSRC_SUBDIR=	src

PLIST_SUB=	ELECTRON_VER=${ELECTRON_VER} \
		ELECTRON_VER_MAJOR=${ELECTRON_VER_MAJOR}

OPTIONS_DEFINE=		CUPS DEBUG DIST DRIVER KERBEROS
OPTIONS_DEFAULT=	CUPS DRIVER KERBEROS ALSA
OPTIONS_GROUP=		AUDIO
OPTIONS_GROUP_AUDIO=	ALSA PULSEAUDIO
OPTIONS_SUB=		yes

DIST_DESC=	Build distribution zip files
DRIVER_DESC=	Install chromedriver

ALSA_LIB_DEPENDS=	libasound.so:audio/alsa-lib
ALSA_RUN_DEPENDS=	${LOCALBASE}/lib/alsa-lib/libasound_module_pcm_oss.so:audio/alsa-plugins
ALSA_VARS=		GN_ARGS+=use_alsa=true
ALSA_VARS_OFF=		GN_ARGS+=use_alsa=false
CUPS_LIB_DEPENDS=	libcups.so:print/cups
CUPS_VARS=		GN_ARGS+=use_cups=true
CUPS_VARS_OFF=		GN_ARGS+=use_cups=false
DEBUG_VARS=		BUILDTYPE=Testing
DEBUG_VARS_OFF=		BUILDTYPE=Release
DIST_IMPLIES=		DRIVER
DRIVER_ALL_TARGET=	chromedriver
KERBEROS_VARS=		GN_ARGS+=use_kerberos=true
KERBEROS_VARS_OFF=	GN_ARGS+=use_kerberos=false
PULSEAUDIO_LIB_DEPENDS=	libpulse.so:audio/pulseaudio
PULSEAUDIO_VARS=	GN_ARGS+=use_pulseaudio=true
PULSEAUDIO_VARS_OFF=	GN_ARGS+=use_pulseaudio=false

# Official chromium version containing "gn" which is known to work
CHROMIUM_OFFICIAL_VER=		87.0.4280.141
# See ${WRKSRC}/electron/DEPS for CHROMIUM_VER
CHROMIUM_VER=			87.0.4280.141
# See ${WRKSRC}/third_party/node/node_modules.tar.gz.sha1 for CHROMIUM_NODE_MODULES_HASH
CHROMIUM_NODE_MODULES_HASH=	a9603a3dc03fa41af9cc5c8ac28d23d1f98dfe3c
# See ${WRKSRC}/third_party/test_fonts/test_fonts.tar.gz.sha1 for CHROMIUM_TEST_FONTS_HASH
CHROMIUM_TEST_FONTS_HASH=	cd96fc55dc243f6c6f4cb63ad117cad6cd48dceb
# See ${WRKSRC}/electron/DEPS for NODE_VER
NODE_VER=			12.18.3
# See ${WRKSRC}/electron/DEPS for NAN_VER
NAN_VER=			2c4ee8a32a299eada3cd6e468bbd0a473bfea96d

YARN_TIMESTAMP=	1613819499

GN_ARGS+=		clang_use_chrome_plugins=false \
			enable_hangout_services_extension=true \
			enable_nacl=false \
			enable_one_click_signin=true \
			enable_remoting=false \
			fieldtrial_testing_like_official_build=true \
			is_clang=true \
			toolkit_views=true \
			treat_warnings_as_errors=false \
			use_allocator="none" \
			use_allocator_shim=false \
			use_aura=true \
			use_custom_libcxx=false \
			use_gnome_keyring=false \
			use_lld=true \
			use_sysroot=false \
			use_system_freetype=true \
			use_system_harfbuzz=true \
			use_system_libjpeg=true \
			extra_cxxflags="${CXXFLAGS}" \
			extra_ldflags="${LDFLAGS}"
GN_BOOTSTRAP_FLAGS=	--no-clean --no-rebuild --skip-generate-buildfiles

.include "Makefile.version"
.include <bsd.port.pre.mk>

.if ${ARCH} == "amd64"
PLIST_SUB+=	AMD64=""
.else
PLIST_SUB+=	AMD64="@comment "
.endif

.if ${ARCH} == "i386"
PLIST_SUB+=	I386=""
.else
PLIST_SUB+=	I386="@comment "
.endif

pre-fetch:
	@${MKDIR} ${DISTDIR}/${DIST_SUBDIR}
	if [ ! -f ${DISTDIR}/${DIST_SUBDIR}/electron-yarn-cache-${ELECTRON_VER}${EXTRACT_SUFX} ]; \
		then ${MKDIR} ${WRKDIR}; \
		${ECHO_CMD} 'yarn-offline-mirror "./yarn-offline-cache"' >> \
			${WRKDIR}/.yarnrc; \
		${CP} ${FILESDIR}/package.json ${FILESDIR}/yarn.lock ${WRKDIR}; \
		cd ${WRKDIR} && ${SETENV} HOME=${WRKDIR} XDG_CACHE_HOME=${WRKDIR}/.cache \
			yarn --frozen-lockfile --ignore-scripts; \
		${MTREE_CMD} -cbnSp yarn-offline-cache | ${MTREE_CMD} -C | ${SED} \
			-e 's:time=[0-9.]*:time=${YARN_TIMESTAMP}.000000000:' \
			-e 's:\([gu]id\)=[0-9]*:\1=0:g' \
			-e 's:flags=.*:flags=none:' \
			-e 's:^\.:./yarn-offline-cache:' > yarn-offline-cache.mtree; \
		${TAR} cJf ${DISTDIR}/${DIST_SUBDIR}/electron-yarn-cache-${ELECTRON_VER}${EXTRACT_SUFX} \
			@yarn-offline-cache.mtree; \
		${RM} -r ${WRKDIR}; \
	fi

post-extract:
# Move extracted sources to appropriate locations
	${MV} ${WRKDIR}/${PORTNAME}-${ELECTRON_VER}/chromium-${CHROMIUM_VER} ${WRKSRC}
	${MV} ${WRKDIR}/${PORTNAME}-${ELECTRON_VER}/${PORTNAME}-${ELECTRON_VER} ${WRKSRC}/electron
	${MV} ${WRKDIR}/${PORTNAME}-${ELECTRON_VER}/${GH_PROJECT_nan}-${NAN_VER} \
		${WRKSRC}/third_party/nan
	${MV} ${WRKDIR}/${PORTNAME}-${ELECTRON_VER}/${GH_PROJECT_node}-${NODE_VER} \
		${WRKSRC}/third_party/electron_node
	# ${MV} ${WRKDIR}/${PORTNAME}-${ELECTRON_VER}/node_modules ${WRKSRC}/third_party/node
	${MV} ${WRKDIR}/${PORTNAME}-${ELECTRON_VER}/test_fonts ${WRKSRC}/third_party/test_fonts
# Take in clang-format from official chromium distribution
	${MKDIR} ${WRKSRC}/buildtools/freebsd
	# ${MV} ${WRKDIR}/${PORTNAME}-${ELECTRON_VER}/chromium-${CHROMIUM_OFFICIAL_VER}/buildtools/linux64/clang-format \
	# 	${WRKSRC}/buildtools/freebsd
	${CP} ${WRKSRC}/buildtools/linux64/clang-format ${WRKSRC}/buildtools/freebsd
# Take in gn source files from official chromium distribution
	# ${RM} -r ${WRKSRC}/tools/gn
	# ${MV} ${WRKDIR}/${PORTNAME}-${ELECTRON_VER}/chromium-${CHROMIUM_OFFICIAL_VER}/tools/gn \
	# 	${WRKSRC}/tools/gn
# Remove unnecessary files
	${RM} -r ${WRKSRC}/third_party/jdk/current
	${RM} -r ${WRKSRC}/third_party/jdk/extras
# Install node modules for electron
	${MV} ${WRKDIR}/${PORTNAME}-${ELECTRON_VER}/yarn-offline-cache ${WRKDIR}
	${ECHO_CMD} 'yarn-offline-mirror "../../../yarn-offline-cache"' >> ${WRKSRC}/electron/.yarnrc
	cd ${WRKSRC}/electron && \
		${SETENV} HOME=${WRKDIR} XDG_CACHE_HOME=${WRKDIR}/.cache yarn --frozen-lockfile --offline

pre-patch:
	${SH} ${FILESDIR}/apply-electron-patches.sh ${WRKSRC}
	# ${FIND} ${WRKSRC} -type f -name '*.orig' -print -delete
	# ${FIND} ${WRKSRC} -type f -name '*~' -print -delete

pre-configure:
# We used to remove bundled libraries to be sure that chromium uses
# system libraries and not shipped ones.
# cd ${WRKSRC} && ${PYTHON_CMD} \
#./build/linux/unbundle/remove_bundled_libraries.py [list of preserved]
	cd ${WRKSRC} && ${SETENV} ${CONFIGURE_ENV} ${PYTHON_CMD} \
		./build/linux/unbundle/replace_gn_files.py --system-libraries \
		ffmpeg flac fontconfig freetype harfbuzz-ng libdrm libpng \
		libusb libwebp libxml libxslt openh264 opus snappy || ${FALSE}

do-configure:
# GN generator bootstrapping and generating ninja files
	cd ${WRKSRC} && ${SETENV} ${CONFIGURE_ENV} CC=${CC} CXX=${CXX} LD=${CXX} \
		READELF=${READELF} AR=${AR} NM=${NM} ${PYTHON_CMD} \
		./tools/gn/bootstrap/bootstrap.py ${GN_BOOTSTRAP_FLAGS}
	cd ${WRKSRC} && ${SETENV} ${CONFIGURE_ENV} ./out/Release/gn gen out/${BUILDTYPE} \
		--args='import("//electron/build/args/${BUILDTYPE:tl}.gn") ${GN_ARGS}'
# Setup nodejs dependency
	${MKDIR} ${WRKSRC}/third_party/node/freebsd/node-freebsd-x64/bin
	${LN} -sf ${LOCALBASE}/bin/node ${WRKSRC}/third_party/node/freebsd/node-freebsd-x64/bin/node
# Setup java dependency
	${MKDIR} ${WRKDIR}/bin
	${LN} -sf ${LOCALBASE}/openjdk8/bin/java ${WRKDIR}/bin/java

post-build:
	cd ${WRKSRC} && ${SETENV} ${MAKE_ENV} \
		${MAKE_CMD} ${MAKE_ARGS} ${POST_BUILD_TARGETS}

post-build-DIST-on:
	cd ${WRKSRC} && ${SETENV} ${MAKE_ENV} \
		${MAKE_CMD} ${MAKE_ARGS} ${POST_BUILD_DIST_TARGETS}
	cd ${WRKSRC}/out/${BUILDTYPE} && \
		${CP} chromedriver.zip chromedriver-v${ELECTRON_VER}-freebsd-${ARCH:S/amd64/x64/:S/i386/ia32/}.zip && \
		${CP} dist.zip electron-v${ELECTRON_VER}-freebsd-${ARCH:S/amd64/x64/:S/i386/ia32/}.zip && \
		${CP} mksnapshot.zip mksnapshot-v${ELECTRON_VER}-freebsd-${ARCH:S/amd64/x64/:S/i386/ia32/}.zip && \
		${SHA256} -r *-v${ELECTRON_VER}-freebsd-*.zip | ${SED} -e 's/ / */' > SHASUMS256.txt

do-install:
	${MKDIR} ${STAGEDIR}${DATADIR}
.for f in electron mksnapshot v8_context_snapshot_generator
	${INSTALL_PROGRAM} ${WRKSRC}/out/${BUILDTYPE}/${f} ${STAGEDIR}${DATADIR}
.endfor
.for f in libEGL.so libGLESv2.so libvk_swiftshader.so libvulkan.so
	${INSTALL_LIB} ${WRKSRC}/out/${BUILDTYPE}/${f} ${STAGEDIR}${DATADIR}
.endfor
	${MKDIR} ${STAGEDIR}${DATADIR}/swiftshader
.for f in libEGL.so libGLESv2.so
	${INSTALL_LIB} ${WRKSRC}/out/${BUILDTYPE}/swiftshader/${f} ${STAGEDIR}${DATADIR}/swiftshader
.endfor
.for f in LICENSE LICENSES.chromium.html icudtl.dat snapshot_blob.bin v8_context_snapshot.bin version vk_swiftshader_icd.json
	${INSTALL_DATA} ${WRKSRC}/out/${BUILDTYPE}/${f} ${STAGEDIR}${DATADIR}
.endfor
.for f in chrome_100_percent.pak chrome_200_percent.pak resources.pak
	${INSTALL_DATA} ${WRKSRC}/out/${BUILDTYPE}/${f} ${STAGEDIR}${DATADIR}
.endfor
	${MKDIR} ${STAGEDIR}${DATADIR}/locales
	${INSTALL_DATA} ${WRKSRC}/out/${BUILDTYPE}/locales/*.pak ${STAGEDIR}${DATADIR}/locales
	${MKDIR} ${STAGEDIR}${DATADIR}/resources
.for f in default_app.asar
	${INSTALL_DATA} ${WRKSRC}/out/${BUILDTYPE}/resources/${f} ${STAGEDIR}${DATADIR}/resources
.endfor
	cd ${WRKSRC}/out/${BUILDTYPE}/gen && ${COPYTREE_SHARE} node_headers ${STAGEDIR}${DATADIR}
	cd ${WRKSRC}/out/${BUILDTYPE} && ${COPYTREE_SHARE} gen/electron/buildflags ${STAGEDIR}${DATADIR}
	cd ${WRKSRC}/out/${BUILDTYPE} && ${COPYTREE_SHARE} gen/v8/embedded.S ${STAGEDIR}${DATADIR}
	${RLN} ${STAGEDIR}${DATADIR}/electron ${STAGEDIR}${PREFIX}/bin/electron${PKGNAMESUFFIX}

post-install-DIST-on:
	${MKDIR} ${STAGEDIR}${DATADIR}/releases
	${INSTALL_DATA} ${WRKSRC}/out/${BUILDTYPE}/SHASUMS256.txt ${STAGEDIR}${DATADIR}/releases
	${INSTALL_DATA} ${WRKSRC}/out/${BUILDTYPE}/*-v${ELECTRON_VER}-freebsd-*.zip ${STAGEDIR}${DATADIR}/releases

post-install-DRIVER-on:
	${INSTALL_PROGRAM} ${WRKSRC}/out/${BUILDTYPE}/chromedriver ${STAGEDIR}${DATADIR}

do-test:
# Note 1: "npm install" will run before actual tests are executed
# Note 2: Xvfb or something similar is necessary for headless testing
	cd ${WRKSRC}/electron && \
		${SETENV} ${TEST_ENV} ELECTRON_OUT_DIR=${BUILDTYPE} LOCAL_GIT_DIRECTORY=${LOCALBASE} \
		npm run test -- --ci

.include <bsd.port.post.mk>
