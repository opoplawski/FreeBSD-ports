# $FreeBSD$

PORTNAME=	grafana
PORTVERSION=	4.3.2
PORTREVISION=	1
DISTVERSIONPREFIX=	v
CATEGORIES=	www
MASTER_SITES+=	https://s3-us-west-2.amazonaws.com/grafana-releases/release/:public
PKGNAMESUFFIX=	${PORTVERSION:C/([0-9]).*/\1/1}
DISTFILES=	grafana-${PORTVERSION}.linux-x64${EXTRACT_SUFX}:public
EXTRACT_ONLY=	${DISTNAME}${EXTRACT_SUFX}

MAINTAINER=	swills@FreeBSD.org
COMMENT=	Dashboard and graph editor for Graphite, InfluxDB & OpenTSDB

LICENSE=	APACHE20

BUILD_DEPENDS=	${LOCALBASE}/bin/go:lang/go

ONLY_FOR_ARCHS=	i386 amd64

USE_RC_SUBR=	grafana

USES=	compiler

USE_GITHUB=	yes
GH_SUBDIR=	src/github.com/${PORTNAME}/${PORTNAME}
TAG=		349f3eb

GRAFANA_USER?=	grafana
GRAFANA_GROUP?=	grafana

USERS=		${GRAFANA_USER}
GROUPS=		${GRAFANA_GROUP}

GRAFANAHOMEDIR=		${PREFIX}/share/grafana/
GRAFANADATADIR=		/var/db/${PORTNAME}/
GRAFANALOGDIR=		/var/log/${PORTNAME}/
GRAFANAPIDDIR=		/var/run/${PORTNAME}/
GRAFANAPLUGINDIR=	/var/db/${PORTNAME}/plugins
GRAFANADASHBOARDDIR=	/var/db/${PORTNAME}/dashboards

SUB_FILES=	grafana grafana.conf
SUB_LIST+=	GRAFANA_USER=${GRAFANA_USER} \
		GRAFANA_GROUP=${GRAFANA_GROUP} \
		GRAFANADATADIR=${GRAFANADATADIR} \
		GRAFANALOGDIR=${GRAFANALOGDIR} \
		GRAFANAPIDDIR=${GRAFANAPIDDIR} \
		GRAFANAHOMEDIR=${GRAFANAHOMEDIR} \
		GRAFANAPLUGINDIR=${GRAFANAPLUGINDIR} \
		GRAFANADASHBOARDDIR=${GRAFANADASHBOARDDIR}

PLIST_SUB+=	GRAFANAHOMEDIR=${GRAFANAHOMEDIR}

post-extract:
	@${RM} -r ${WRKSRC}/src/github.com/grafana/grafana/public
	@(cd ${WRKDIR} && ${EXTRACT_CMD} ${EXTRACT_BEFORE_ARGS} ${DISTDIR}/grafana-${PORTVERSION}.linux-x64${EXTRACT_SUFX} ${EXTRACT_AFTER_ARGS} grafana-${PORTVERSION}/public)

do-build:
	@cd ${WRKSRC}/src/github.com/${PORTNAME}/${PORTNAME} ; ${SETENV} ${BUILD_ENV} GOPATH=${WRKSRC} go build -ldflags "-w -X main.version=${PORTVERSION} -X main.commit=${TAG}" -o ./bin/grafana-server ./pkg/cmd/grafana-server
	@cd ${WRKSRC}/src/github.com/${PORTNAME}/${PORTNAME} ; ${SETENV} ${BUILD_ENV} GOPATH=${WRKSRC} go build -ldflags "-w -X main.version=${PORTVERSION} -X main.commit=${TAG}" -o ./bin/grafana-cli ./pkg/cmd/grafana-cli

do-install:
	${INSTALL_PROGRAM} ${WRKSRC}/src/github.com/grafana/grafana/bin/grafana-server \
		${STAGEDIR}${PREFIX}/bin/grafana-server
	${INSTALL_PROGRAM} ${WRKSRC}/src/github.com/grafana/grafana/bin/grafana-cli \
		${STAGEDIR}${PREFIX}/bin/grafana-cli
	cd ${WRKSRC}/src/github.com/grafana/grafana && \
		${COPYTREE_SHARE} public ${STAGEDIR}${PREFIX}/share/grafana
	${MKDIR} ${STAGEDIR}${GRAFANAPIDDIR}
	${MKDIR} ${STAGEDIR}${GRAFANALOGDIR}
	${MKDIR} ${STAGEDIR}${GRAFANAHOMEDIR}
	${MKDIR} ${STAGEDIR}${GRAFANADATADIR}
	${MKDIR} ${STAGEDIR}${GRAFANAPLUGINDIR}
	${MKDIR} ${STAGEDIR}${GRAFANADASHBOARDDIR}
	${MKDIR} ${STAGEDIR}${GRAFANAHOMEDIR}/conf
	${MKDIR} ${STAGEDIR}${GRAFANAHOMEDIR}/data
	${MKDIR} ${STAGEDIR}${GRAFANAHOMEDIR}/data/log
	${INSTALL_DATA} ${WRKSRC}/src/github.com/grafana/grafana/conf/defaults.ini \
		${STAGEDIR}${GRAFANAHOMEDIR}/conf/defaults.ini
	${INSTALL_DATA} ${WRKDIR}/grafana.conf ${STAGEDIR}${PREFIX}/etc/grafana.conf.sample

.include <bsd.port.pre.mk>

.if ${COMPILER_TYPE} == clang
BUILD_ENV=	CC=clang
.endif

.include <bsd.port.post.mk>
