# Created by: Alex Semenyaka <alex@rinet.ru>
# $FreeBSD$

PORTNAME=	chmview
PORTVERSION=	2.0b4
PORTREVISION=	2
CATEGORIES=	converters textproc
MASTER_SITES=	https://googledrive.com/host/0BwCT-sp3iBCaeDRPYm1jTjl1Qmc/

MAINTAINER=	ak@FreeBSD.org
COMMENT=	Extractor from .chm files

LICENSE=	GPLv2+
LICENSE_FILE=	${WRKSRC}/../COPYING

LIB_DEPENDS=	libchm.so:misc/chmlib

USES=		tar:xz uidfix

WRKSRC=		${WRKDIR}/src
MAKEFILE=	${FILESDIR}/Makefile
PLIST_FILES=	bin/chmview

.include <bsd.port.mk>
