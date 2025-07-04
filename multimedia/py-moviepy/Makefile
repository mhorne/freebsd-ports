# $FreeBSD$

PORTNAME=	moviepy
PORTVERSION=	1.0.3
CATEGORIES=	multimedia python
MASTER_SITES=	CHEESESHOP
PKGNAMEPREFIX=	${PYTHON_PKGNAMEPREFIX}

MAINTAINER=	sunpoet@FreeBSD.org
COMMENT=	Video editing with Python

LICENSE=	MIT
LICENSE_FILE=	${WRKSRC}/LICENCE.txt

RUN_DEPENDS=	ffmpeg:multimedia/ffmpeg \
		convert:graphics/ImageMagick${IMAGEMAGICK_DEFAULT} \
		${PYTHON_PKGNAMEPREFIX}decorator>=4.0.2<5.0:devel/py-decorator@${PY_FLAVOR} \
		${PYTHON_PKGNAMEPREFIX}imageio>=2.5<3.0:graphics/py-imageio@${PY_FLAVOR} \
		${PYTHON_PKGNAMEPREFIX}imageio-ffmpeg>=0.2.0:graphics/py-imageio-ffmpeg@${PY_FLAVOR} \
		${PYNUMPY} \
		${PYTHON_PKGNAMEPREFIX}proglog<=1.0.0:devel/py-proglog@${PY_FLAVOR} \
		${PYTHON_PKGNAMEPREFIX}requests>=2.8.1<3.0:www/py-requests@${PY_FLAVOR} \
		${PYTHON_PKGNAMEPREFIX}tqdm>=4.11.2<5.0:misc/py-tqdm@${PY_FLAVOR} \

USES=		python:3.4+
USE_PYTHON=	autoplist concurrent distutils

NO_ARCH=	yes

.include <bsd.port.mk>
