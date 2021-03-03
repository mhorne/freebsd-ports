# $FreeBSD$

PORTNAME=	List-MoreUtils-XS
PORTVERSION=	0.428
CATEGORIES=	devel perl5
MASTER_SITES=	CPAN
PKGNAMEPREFIX=	p5-

MAINTAINER=	perl@FreeBSD.org
COMMENT=	Faster Thrift binary protocol encoding and decoding

LICENSE=	APACHE20

USES=		perl5
USE_PERL5=	configure

post-install:
	${STRIP_CMD} ${STAGEDIR}${PREFIX}/${SITE_ARCH_REL}/auto/List/MoreUtils/XS/XS.so

.include <bsd.port.mk>
