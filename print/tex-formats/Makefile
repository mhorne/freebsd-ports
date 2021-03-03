# $FreeBSD$

PORTNAME=	formats
PORTVERSION=	202020406
CATEGORIES=	print
MASTER_SITES=	#empty
PKGNAMEPREFIX=	tex-
DISTFILES=	#empty
EXTRACT_ONLY=	#empty

MAINTAINER=	hrs@FreeBSD.org
COMMENT=	Formats for basic TeX engines and the 'latex' command

NO_ARCH=	yes
NO_BUILD=	yes
NO_INSTALL=	yes

USE_TEX=	web2c basic texmf fmtutil texhash
TEXHASHDIRS=	${TEXMFVARDIR}
TEX_FORMATS=	amstex context cslatex csplain eplain latex-bin \
		metafont mex mptopdf pdftex tex

.include <bsd.port.mk>
