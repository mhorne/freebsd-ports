# $FreeBSD$

PORTNAME=	List-MoreUtils
PORTVERSION=	0.428
CATEGORIES=	devel perl5
MASTER_SITES=	CPAN
PKGNAMEPREFIX=	p5-

MAINTAINER=	perl@FreeBSD.org
COMMENT=	Additional list functionality not present in List::Util

LICENSE=	APACHE20

USES=		perl5
USE_PERL5=	configure

BUILD_DEPENDS=	${RUN_DEPENDS}
RUN_DEPENDS=	p5-Exporter-Tiny>0:devel/p5-Exporter-Tiny \
		p5-List-MoreUtils-XS>0:devel/p5-List-MoreUtils-XS

NO_ARCH=	yes

.include <bsd.port.mk>
