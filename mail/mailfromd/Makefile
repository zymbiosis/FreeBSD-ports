PORTNAME=	mailfromd
PORTVERSION=	8.13
CATEGORIES=	mail
MASTER_SITES=	http://download.gnu.org.ua/pub/release/${PORTNAME}/ \
		http://download.gnu.org.ua/pub/alpha/${PORTNAME}/

MAINTAINER=	zeus@gnu.org.ua
COMMENT=	Mail filtering daemon for Sendmail, Postfix, and MeTA1
WWW=		https://puszcza.gnu.org.ua/software/mailfromd/

LICENSE=	GPLv3+

LIB_DEPENDS=	libmailutils.so:mail/mailutils \
		libadns.so:dns/adns \
		libgmp.so:math/gmp \
		libgnutls.so:security/gnutls \
		libnettle.so:security/nettle

USES=		gmake localbase readline tar:xz
GNU_CONFIGURE=	yes
CONFIGURE_ARGS=	--enable-syslog-async
CONFIGURE_ENV=	DEFAULT_STATE_DIR="${DATABASEDIR}" \
		DEFAULT_SOCKET="unix:${MFD_RUN_DIR}/${PORTNAME}.sock" \
		DEFAULT_USER=mailnull
USE_RC_SUBR=	calloutd ${PORTNAME}
TEST_TARGET=	check

DATABASEDIR?=	/var/db/${PORTNAME}
MFD_RUN_DIR?=	/var/run/${PORTNAME}

PLIST_SUB+=	DATABASEDIR=${DATABASEDIR} \
		MFD_RUN_DIR=${MFD_RUN_DIR} \
		VERSION=${PORTVERSION}
SUB_LIST+=	MFD_RUN_DIR=${MFD_RUN_DIR}

INFO=		${PORTNAME}
PORTDOCS=	AUTHORS ChangeLog NEWS README THANKS TODO

OPTIONS_DEFINE=		DOCS DSPAM NLS
OPTIONS_DEFAULT=	GDBM
OPTIONS_MULTI=		DB
OPTIONS_MULTI_DB=	BDB GDBM
OPTIONS_SUB=		yes

BDB_DESC=		Berkeley DB v4.8 support (last working one)
DB_DESC=		Database configuration

DSPAM_DESC=		DSPAM spam filter library support
DSPAM_LIB_DEPENDS=	libdspam.so:mail/dspam
DSPAM_USES=		pkgconfig
DSPAM_CONFIGURE_WITH=	dspam

NLS_USES=		gettext
NLS_CONFIGURE_ENABLE=	nls

BDB_USES=		bdb
BDB_CONFIGURE_WITH=	berkeley-db
BDB_CPPFLAGS=		-I${BDB_INCLUDE_DIR}
BDB_LDFLAGS=		-L${BDB_LIB_DIR}

GDBM_LIB_DEPENDS=	libgdbm.so:databases/gdbm
GDBM_CONFIGURE_WITH=	gdbm

.if defined(WITH_DEBUG)
CONFIGURE_ARGS+=	--enable-debug
.endif

post-install:
	@${MKDIR} ${STAGEDIR}${DATABASEDIR} ${STAGEDIR}${MFD_RUN_DIR}

post-install-DOCS-on:
	@${MKDIR} ${STAGEDIR}${DOCSDIR}
	${INSTALL_DATA} ${PORTDOCS:S|^|${WRKSRC}/|} ${STAGEDIR}${DOCSDIR}

.include <bsd.port.mk>
