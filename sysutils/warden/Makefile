# Created by: Kris Moore <kmoore@FreeBSD.org>
# $FreeBSD$

PORTNAME=	warden
PORTVERSION=	1438351389
CATEGORIES=	sysutils

MAINTAINER=	kmoore@FreeBSD.org
COMMENT=	Warden jail management system utility

LICENSE=	BSD3CLAUSE

RUN_DEPENDS=	${LOCALBASE}/share/pcbsd/scripts/functions.sh:sysutils/pcbsd-libsh \
		debootstrap:sysutils/debootstrap \
		jailme:sysutils/jailme

WRKSRC_SUBDIR=	src-sh/warden
USES=		pkgconfig
NO_BUILD=	yes
NO_ARCH=	yes
MAKE_ARGS=	PREFIX=${STAGEDIR}${PREFIX}

USE_GITHUB=	yes
GH_ACCOUNT=	pcbsd
GH_PROJECT=	pcbsd
GH_TAGNAME=	2c5a0c

.include <bsd.port.mk>
