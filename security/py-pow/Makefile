# Created by: ijliao
# $FreeBSD$

PORTNAME=	pow
PORTVERSION=	0.7
PORTREVISION=	2
CATEGORIES=	security python
MASTER_SITES=	SF/${PORTNAME}/POW/POW-${PORTVERSION}
PKGNAMEPREFIX=	${PYTHON_PKGNAMEPREFIX}
DISTNAME=	${PORTNAME:tu}-${PORTVERSION}

MAINTAINER=	ports@FreeBSD.org
COMMENT=	Python OpenSSL Wrappers

LICENSE=	BSD3CLAUSE

USES=		python:2.7 ssl
USE_PYTHON=	distutils
PYDISTUTILS_PKGNAME=	POW

PORTDOCS=	POW.pdf

OPTIONS_DEFINE=	DOCS

.include <bsd.port.pre.mk>

.if ${SSL_DEFAULT} == base
BROKEN_FreeBSD_12=	field has incomplete type 'EVP_CIPHER_CTX' (aka 'struct evp_cipher_ctx_st')
BROKEN_FreeBSD_13=	field has incomplete type 'EVP_CIPHER_CTX' (aka 'struct evp_cipher_ctx_st')
.endif

post-patch:
	@${REINPLACE_CMD} -e 's|licence|license|' ${WRKSRC}/setup.py

do-build:
	cd ${WRKSRC} && ${PYTHON_CMD} ${PYSETUP} build_ext -D NO_RC5_32_12_16 ${PYDISTUTILS_BUILD_TARGET}

post-install:
	@${STRIP_CMD} ${STAGEDIR}${PYTHONPREFIX_SITELIBDIR}/POW/_POW.so

post-install-DOCS-on:
	@${MKDIR} ${STAGEDIR}${DOCSDIR}
.for i in ${PORTDOCS}
	${INSTALL_DATA} ${WRKSRC}/docs/${i} ${STAGEDIR}${DOCSDIR}
.endfor

.include <bsd.port.post.mk>
