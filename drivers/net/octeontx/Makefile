#   BSD LICENSE
#
#   Copyright(c) 2017 Cavium Inc. All rights reserved.
#
#   Redistribution and use in source and binary forms, with or without
#   modification, are permitted provided that the following conditions
#   are met:
#
#     * Redistributions of source code must retain the above copyright
#       notice, this list of conditions and the following disclaimer.
#     * Redistributions in binary form must reproduce the above copyright
#       notice, this list of conditions and the following disclaimer in
#       the documentation and/or other materials provided with the
#       distribution.
#     * Neither the name of Cavium Networks nor the names of its
#       contributors may be used to endorse or promote products derived
#       from this software without specific prior written permission.
#
#   THIS SOFTWARE IS PROVIDED BY THE COPYRIGHT HOLDERS AND CONTRIBUTORS
#   "AS IS" AND ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT
#   LIMITED TO, THE IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR
#   A PARTICULAR PURPOSE ARE DISCLAIMED. IN NO EVENT SHALL THE COPYRIGHT
#   OWNER OR CONTRIBUTORS BE LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL,
#   SPECIAL, EXEMPLARY, OR CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT
#   LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES; LOSS OF USE,
#   DATA, OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND ON ANY
#   THEORY OF LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT
#   (INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE
#   OF THIS SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.
#
include $(RTE_SDK)/mk/rte.vars.mk

#
# library name
#
LIB = librte_pmd_octeontx.a

CFLAGS += $(WERROR_FLAGS)
CFLAGS += -I$(RTE_SDK)/drivers/mempool/octeontx/

EXPORT_MAP := rte_pmd_octeontx_version.map

LIBABIVER := 1

OBJS_BASE_DRIVER=$(patsubst %.c,%.o,$(notdir $(wildcard $(SRCDIR)/base/*.c)))
$(foreach obj, $(OBJS_BASE_DRIVER), $(eval CFLAGS_$(obj)+=$(CFLAGS_BASE_DRIVER)))

VPATH += $(SRCDIR)/base

#
# all source are stored in SRCS-y
#
SRCS-$(CONFIG_RTE_LIBRTE_OCTEONTX_PMD) += octeontx_rxtx.c
SRCS-$(CONFIG_RTE_LIBRTE_OCTEONTX_PMD) += octeontx_pkovf.c
SRCS-$(CONFIG_RTE_LIBRTE_OCTEONTX_PMD) += octeontx_pkivf.c
SRCS-$(CONFIG_RTE_LIBRTE_OCTEONTX_PMD) += octeontx_bgx.c
SRCS-$(CONFIG_RTE_LIBRTE_OCTEONTX_PMD) += octeontx_ethdev.c

ifeq ($(CONFIG_RTE_TOOLCHAIN_GCC),y)
CFLAGS_octeontx_rxtx.o += -fno-prefetch-loop-arrays
endif
CFLAGS_octeontx_rxtx.o += -O3 -Ofast

LDLIBS += -lrte_eventdev
LDLIBS += -lrte_pmd_octeontx_ssovf

include $(RTE_SDK)/mk/rte.lib.mk
