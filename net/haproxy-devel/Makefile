# Created by: Hugo Saro <hugo@barafranca.com>
# $FreeBSD$

PORTNAME=	haproxy
DISTVERSION=	2.4-dev10
CATEGORIES=	net www
MASTER_SITES=	http://www.haproxy.org/download/2.4/src/devel/
PKGNAMESUFFIX=	-devel
DISTFILES=	${PORTNAME}-${DISTVERSION}${EXTRACT_SUFX}

MAINTAINER=	demon@FreeBSD.org
COMMENT=	Reliable, high performance TCP/HTTP load balancer

LICENSE=	GPLv2 LGPL21
LICENSE_COMB=	multi

CONFLICTS_INSTALL=	haproxy-[0-9]* haproxy17-[0-9]* haproxy18-[0-9]* haproxy19-[0-9]* haproxy20-[0-9]* haproxy21-[0-9]*

USES=		compiler:c++11-lang cpe gmake
USE_RC_SUBR=	haproxy

MAKE_ARGS=	TARGET=freebsd DEFINE=-DFREEBSD_PORTS USE_GETADDRINFO=1 \
		USE_ZLIB=1 USE_CPU_AFFINITY=1 USE_ACCEPT4=1 \
		CC="${CC}" DEBUG_CFLAGS="" CPU_CFLAGS="${CFLAGS}"

OPTIONS_DEFINE=		DOCS EXAMPLES LUA OPENSSL DEVICEATLAS PROMEX
OPTIONS_RADIO=		PCRE
OPTIONS_RADIO_PCRE=	DPCRE SPCRE
DPCRE_DESC=		Link dynamically
SPCRE_DESC=		Link statically
DEVICEATLAS_DESC=	DeviceAtlas Device Detection support
PROMEX_DESC=		Enable Prometheus exporter
OPTIONS_DEFAULT=	SPCRE OPENSSL

DPCRE_LIB_DEPENDS=	libpcre.so:devel/pcre
DPCRE_MAKE_ARGS=	USE_PCRE=1 USE_PCRE_JIT=1
SPCRE_LIB_DEPENDS=	libpcre.so:devel/pcre
SPCRE_MAKE_ARGS=	USE_PCRE=1 USE_STATIC_PCRE=1 USE_PCRE_JIT=1
DEVICEATLAS_LIB_DEPENDS=	libda.so:net/deviceatlas-enterprise-c
DEVICEATLAS_MAKE_ARGS=		USE_DEVICEATLAS=1 DEVICEATLAS_LIB=${LOCALBASE}/lib DEVICEATLAS_INC=${LOCALBASE}/include
PROMEX_MAKE_ARGS=	EXTRA_OBJS="contrib/prometheus-exporter/service-prometheus.o"
OPENSSL_USES=		ssl
OPENSSL_MAKE_ARGS=	USE_OPENSSL=1 SSL_LIB=${OPENSSLLIB} SSL_INC=${OPENSSLINC}
LUA_USES=		lua:53
LUA_MAKE_ARGS=		USE_LUA=1 LUA_INC=${LUA_INCDIR} LUA_LIB=${LUA_LIBDIR} LUA_LIB_NAME=lua-${LUA_VER}

.include <bsd.port.pre.mk>

.if ${ARCH} == "amd64" || ${ARCH} == "i386"
MAKE_ARGS+=	USE_REGPARM=1
.endif

post-build:
	cd ${WRKSRC}/contrib/halog && ${MAKE_CMD} ${MAKE_ENV}

do-install:
	${INSTALL_PROGRAM} ${WRKSRC}/haproxy ${STAGEDIR}${PREFIX}/sbin/
	${INSTALL_PROGRAM} ${WRKSRC}/contrib/halog/halog ${STAGEDIR}${PREFIX}/sbin/
	${INSTALL_MAN} ${WRKSRC}/doc/haproxy.1 ${STAGEDIR}${MAN1PREFIX}/man/man1
	${MKDIR} ${STAGEDIR}${DOCSDIR}
	(cd ${WRKSRC}/doc/ && ${COPYTREE_SHARE} \* ${STAGEDIR}${DOCSDIR})
	${MKDIR} ${STAGEDIR}${EXAMPLESDIR}
	(cd ${WRKSRC}/examples/ && ${COPYTREE_SHARE} \* ${STAGEDIR}${EXAMPLESDIR})

.include <bsd.port.post.mk>
