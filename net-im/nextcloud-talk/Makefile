# Created by: Bernard Spil <brnrd@freebsd.org>
# $FreeBSD$

PORTNAME=	talk
PORTVERSION=	11.0.0
CATEGORIES=	net-im www
MASTER_SITES=	https://github.com/${PKGNAMEPREFIX:S/-//}/${DISTNAME:C/-.*//}/releases/download/v${PORTVERSION}/
PKGNAMEPREFIX=	nextcloud-
PKGNAMESUFFIX=	${PHP_PKGNAMESUFFIX}
DISTNAME=	spreed-${PORTVERSION}
DIST_SUBDIR=	${PKGNAMEPREFIX:S/-//}/${DISTNAME}
WRKSRC=		${WRKDIR}/spreed

MAINTAINER=	brnrd@FreeBSD.org
COMMENT=	Online meeting app for Nextcloud

LICENSE=	AGPLv3
LICENSE_FILE=	${WRKSRC}/COPYING

RUN_DEPENDS=	nextcloud${PHP_PKGNAMESUFFIX}>=21:www/nextcloud@${PHP_FLAVOR}

USES=		php:flavors
NO_BUILD=	yes
NO_ARCH=	yes

NEXTCLOUD_USERNAME?=	${WWWOWN}
NEXTCLOUD_GROUPNAME?=	${WWWGRP}

PLIST_SUB=	NEXTCLOUD_USERNAME=${NEXTCLOUD_USERNAME} \
		NEXTCLOUD_GROUPNAME=${NEXTCLOUD_GROUPNAME}

WWWDIR=		${PREFIX}/www/nextcloud/apps-pkg/spreed

do-install:
	${MKDIR} ${STAGEDIR}${WWWDIR}
	(cd ${WRKSRC} && ${COPYTREE_SHARE} . ${STAGEDIR}${WWWDIR})

.include <bsd.port.mk>
