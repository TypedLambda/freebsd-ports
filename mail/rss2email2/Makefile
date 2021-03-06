# Created by: Andrew Pantyukhin <infofarmer@FreeBSD.org>
# $FreeBSD$

PORTNAME=	rss2email
PORTVERSION=	2.71
PORTREVISION=	1
CATEGORIES=	mail python
MASTER_SITES=	http://www.allthingsrss.com/rss2email/
PKGNAMEPREFIX=	${PYTHON_PKGNAMEPREFIX}

MAINTAINER=	srg@guglielmo.us
COMMENT=	Emails posts from subscribed RSS/Atom newsfeeds

LICENSE=	GPLv2 GPLv3
LICENSE_COMB=	dual

RUN_DEPENDS=	${PYTHON_PKGNAMEPREFIX}feedparser>=5.0.1:textproc/py-feedparser \
		${PYTHON_PKGNAMEPREFIX}html2text>=3.0.1:textproc/py-html2text

USES=		python:2 shebangfix
SHEBANG_FILES=	rss2email.py
NO_ARCH=	yes
NO_BUILD=	yes

CONFLICTS_INSTALL=	py*-rss2email-3.*

PLIST_FILES=	bin/r2e \
		%%DATADIR%%/rss2email.py
PORTEXAMPLES=	config.py.example

OPTIONS_DEFINE=	EXAMPLES

post-patch:
	@${REINPLACE_CMD} -e 's|@PYTHONCMD@|${PYTHON_CMD}|;s|@DATADIR@|${DATADIR}|'\
		${WRKSRC}/r2e
	@${REINPLACE_CMD} -e "s|\([^[:alnum:]]\)c.type\([^[:alnum:]]\)|\1c.get('type','')\2|"\
		${WRKSRC}/rss2email.py

do-install:
	@${MKDIR} ${STAGEDIR}${DATADIR} ${STAGEDIR}${EXAMPLESDIR}
	${INSTALL_SCRIPT} ${WRKSRC}/rss2email.py ${STAGEDIR}${DATADIR}
	${INSTALL_SCRIPT} ${WRKSRC}/r2e ${STAGEDIR}${PREFIX}/bin
	${INSTALL_DATA} ${WRKSRC}/config.py.example ${STAGEDIR}${EXAMPLESDIR}

.include <bsd.port.pre.mk>

.if ${OSVERSION} < 1100077
# chmod -R bug.
post-extract:
	@${CHMOD} 0755 ${WRKSRC}
.endif

.include <bsd.port.post.mk>
