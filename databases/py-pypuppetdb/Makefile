PORTNAME=	pypuppetdb
PORTVERSION=	2.5.2
CATEGORIES=	databases python
PKGNAMEPREFIX=	${PYTHON_PKGNAMEPREFIX}

MAINTAINER=	puppet@FreeBSD.org
COMMENT=	Library to work with PuppetDB's REST API
WWW=		https://github.com/voxpupuli/pypuppetdb

LICENSE=	APACHE20
LICENSE_FILE=	${WRKSRC}/LICENSE

USES=		python:3.6+
USE_GITHUB=	yes
USE_PYTHON=	autoplist distutils

NO_ARCH=	yes

CONFLICTS_INSTALL=	pypuppetdb03

GH_ACCOUNT=	voxpupuli

post-patch:
	${REINPLACE_CMD} -e '/requirements_for_tests/d' \
		${WRKSRC}/setup.py

.include <bsd.port.mk>
