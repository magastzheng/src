#	$NetBSD: Makefile,v 1.6 2016/08/19 16:33:23 christos Exp $

.include <bsd.own.mk>

DRIVER=		xf86-video-ati-kms
DRIVER_NAME=	radeon_drv

LIBDPLIBS+=	drm_radeon ${.CURDIR}/../../../lib/libdrm_radeon

.if ${XORG_SERVER_SUBDIR} == "xorg-server.old"
CPPFLAGS+=	-DUSE_XAA
.else
CPPFLAGS+= \
		-DHAS_DIRTYTRACKING2 \
		-DHAVE_XORG_LIST \
		-DHAVE_XF86_CURSOR_RESET_CURSOR \
		-DHAVE_DRI3_H \
		-DHAVE_MISYNCSHM_H \
		-DHAVE_PRESENT_H \
		-DHAVE_XF86_CURSOR_RESET_CURSOR
.endif

SRCS.EXA=	radeon_exa.c r600_exa.c r6xx_accel.c \
		r600_textured_videofuncs.c r600_shader.c radeon_exa_shared.c \
		evergreen_exa.c evergreen_accel.c evergreen_shader.c \
		evergreen_textured_videofuncs.c cayman_accel.c cayman_shader.c
SRCS.KMS=	radeon_dri2.c radeon_dri3.c radeon_drm_queue.c radeon_kms.c \
		radeon_present.c radeon_sync.c radeon_vbo.c radeon_bo_helper.c \
		drmmode_display.c

.if ${HAVE_XORG_GLAMOR} != "no"
SRCS.GLAMOR=	radeon_glamor.c radeon_glamor_wrappers.c
CPPFLAGS+= \
		-DHAVE_GLAMOR_H \
		-DUSE_GLAMOR
.else
SRCS.GLAMOR=
.endif

SRCS=		radeon_accel.c radeon_video.c \
		radeon_misc.c radeon_probe.c \
		radeon_textured_video.c radeon_xvmc.c \
		$(SRCS.EXA) \
		$(SRCS.KMS) \
		$(SRCS.GLAMOR)

MAN=		radeon.4
MANSUBDIR=	/x86

CPPFLAGS+=	-DHAVE_CONFIG_H
CPPFLAGS+=	-I${DESTDIR}${X11INCDIR}/X11 \
		-I${DESTDIR}${X11INCDIR}/X11/dri \
		-I${DESTDIR}${X11INCDIR}/libdrm \
		-I${DESTDIR}${X11INCDIR}/pixman-1 \
		-I${X11SRCDIR.${DRIVER}}/../include

# XXX
COPTS+=	-Wno-error

.include "../Makefile.xf86-driver"
