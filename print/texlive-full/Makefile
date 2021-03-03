# $FreeBSD$

PORTNAME=	texlive
DISTVERSION=	20200327
CATEGORIES=	print
PKGNAMESUFFIX=	-full

MAINTAINER=	hrs@FreeBSD.org
COMMENT=	TeX Live, Full Version

USES=		metaport
USE_TEX=	full texhash

OPTIONS_DEFINE=	DOCS SOURCE

DOCS_USE=	TEX=docs
SOURCE_DESC=	Install source files
SOURCE_USE=	TEX=source

.include <bsd.port.mk>
