# Created by: Rusmir Dusko <nemysis@FreeBSD.org>
# $FreeBSD$

PORTNAME=	glfw
PORTVERSION=	3.2.1
PORTREVISION=	2
CATEGORIES=	graphics
MASTER_SITES=	SF

MAINTAINER=	koalative@gmail.com
COMMENT=	Portable framework for OpenGL development

LICENSE=	ZLIB

USES=		cmake localbase zip
USE_XORG=	x11 xcursor xinerama xrandr xxf86vm
USE_GL=		glu
USE_LDCONFIG=	yes
CMAKE_ARGS=	-DBUILD_SHARED_LIBS:BOOL=ON

PORTDOCS=	*

DOCSRCDIR1=	${WRKSRC}
DOC_FILES1=	README.md

DOCSRCDIR2=	${WRKSRC}/docs/html/search
DOCSDIR2=	${DOCSDIR}/docs/html/search
DOC_FILES2=	*

DOCSRCDIR3=	${WRKSRC}/docs/html
DOCSDIR3=	${DOCSDIR}/docs/html
DOC_FILES3=	*.html *.png *.css *.js

PORTEXAMPLES=	*

EXAMPLESSRCDIR1=	${WRKSRC}/examples
EXAMPLES_FILES1=	boing gears heightmap particles simple splitview wave

EXAMPLESSRCDIR2=	${WRKSRC}/tests
EXAMPLESDIR2=		${EXAMPLESDIR}/tests
EXAMPLES_FILES2=	clipboard cursor empty events gamma glfwinfo iconify \
			joysticks monitors msaa reopen sharing tearing threads \
			title windows

OPTIONS_DEFINE=	DOCS EXAMPLES

post-patch:
	@${REINPLACE_CMD} -e 's|lib$${LIB_SUFFIX}/pkgconfig|libdata/pkgconfig|' \
		${WRKSRC}/CMakeLists.txt

do-install-DOCS-on:
	@${MKDIR} ${STAGEDIR}${DOCSDIR}
	${INSTALL_DATA} ${DOC_FILES1:S|^|${DOCSRCDIR1}/|} ${STAGEDIR}${DOCSDIR}
	@${MKDIR} ${STAGEDIR}${DOCSDIR2}
	${INSTALL_DATA} ${DOC_FILES2:S|^|${DOCSRCDIR2}/|} ${STAGEDIR}${DOCSDIR2}
	${INSTALL_DATA} ${DOC_FILES3:S|^|${DOCSRCDIR3}/|} ${STAGEDIR}${DOCSDIR3}

do-install-EXAMPLES-on:
	@${MKDIR} ${STAGEDIR}${EXAMPLESDIR}
	${INSTALL_PROGRAM} ${EXAMPLES_FILES1:S|^|${EXAMPLESSRCDIR1}/|} \
		${STAGEDIR}${EXAMPLESDIR}
	@${MKDIR} ${STAGEDIR}${EXAMPLESDIR2}
	${INSTALL_PROGRAM} ${EXAMPLES_FILES2:S|^|${EXAMPLESSRCDIR2}/|} \
		${STAGEDIR}${EXAMPLESDIR2}

.include <bsd.port.mk>
