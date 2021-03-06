#   BSD LICENSE
#
#   Copyright(c) 2010-2015 Intel Corporation. All rights reserved.
#   All rights reserved.
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
#     * Neither the name of Intel Corporation nor the names of its
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

include $(RTE_SDK)/mk/rte.vars.mk

LIB = librte_eal.a

ARCH_DIR ?= $(RTE_ARCH)
VPATH += $(RTE_SDK)/lib/librte_eal/common
VPATH += $(RTE_SDK)/lib/librte_eal/common/arch/$(ARCH_DIR)

CFLAGS += -I$(SRCDIR)/include
CFLAGS += -I$(RTE_SDK)/lib/librte_eal/common
CFLAGS += -I$(RTE_SDK)/lib/librte_eal/common/include
CFLAGS += $(WERROR_FLAGS) -O3

LDLIBS += -lexecinfo
LDLIBS += -lpthread
LDLIBS += -lgcc_s

EXPORT_MAP := rte_eal_version.map

LIBABIVER := 6

# specific to bsdapp exec-env
SRCS-$(CONFIG_RTE_EXEC_ENV_BSDAPP) := eal.c
SRCS-$(CONFIG_RTE_EXEC_ENV_BSDAPP) += eal_memory.c
SRCS-$(CONFIG_RTE_EXEC_ENV_BSDAPP) += eal_hugepage_info.c
SRCS-$(CONFIG_RTE_EXEC_ENV_BSDAPP) += eal_thread.c
SRCS-$(CONFIG_RTE_EXEC_ENV_BSDAPP) += eal_pci.c
SRCS-$(CONFIG_RTE_EXEC_ENV_BSDAPP) += eal_debug.c
SRCS-$(CONFIG_RTE_EXEC_ENV_BSDAPP) += eal_lcore.c
SRCS-$(CONFIG_RTE_EXEC_ENV_BSDAPP) += eal_timer.c
SRCS-$(CONFIG_RTE_EXEC_ENV_BSDAPP) += eal_interrupts.c
SRCS-$(CONFIG_RTE_EXEC_ENV_BSDAPP) += eal_alarm.c

# from common dir
SRCS-$(CONFIG_RTE_EXEC_ENV_BSDAPP) += eal_common_lcore.c
SRCS-$(CONFIG_RTE_EXEC_ENV_BSDAPP) += eal_common_timer.c
SRCS-$(CONFIG_RTE_EXEC_ENV_BSDAPP) += eal_common_memzone.c
SRCS-$(CONFIG_RTE_EXEC_ENV_BSDAPP) += eal_common_log.c
SRCS-$(CONFIG_RTE_EXEC_ENV_BSDAPP) += eal_common_launch.c
SRCS-$(CONFIG_RTE_EXEC_ENV_BSDAPP) += eal_common_vdev.c
SRCS-$(CONFIG_RTE_EXEC_ENV_BSDAPP) += eal_common_pci.c
SRCS-$(CONFIG_RTE_EXEC_ENV_BSDAPP) += eal_common_pci_uio.c
SRCS-$(CONFIG_RTE_EXEC_ENV_BSDAPP) += eal_common_memory.c
SRCS-$(CONFIG_RTE_EXEC_ENV_BSDAPP) += eal_common_tailqs.c
SRCS-$(CONFIG_RTE_EXEC_ENV_BSDAPP) += eal_common_errno.c
SRCS-$(CONFIG_RTE_EXEC_ENV_BSDAPP) += eal_common_cpuflags.c
SRCS-$(CONFIG_RTE_EXEC_ENV_BSDAPP) += eal_common_string_fns.c
SRCS-$(CONFIG_RTE_EXEC_ENV_BSDAPP) += eal_common_hexdump.c
SRCS-$(CONFIG_RTE_EXEC_ENV_BSDAPP) += eal_common_devargs.c
SRCS-$(CONFIG_RTE_EXEC_ENV_BSDAPP) += eal_common_bus.c
SRCS-$(CONFIG_RTE_EXEC_ENV_BSDAPP) += eal_common_dev.c
SRCS-$(CONFIG_RTE_EXEC_ENV_BSDAPP) += eal_common_options.c
SRCS-$(CONFIG_RTE_EXEC_ENV_BSDAPP) += eal_common_thread.c
SRCS-$(CONFIG_RTE_EXEC_ENV_BSDAPP) += eal_common_proc.c
SRCS-$(CONFIG_RTE_EXEC_ENV_BSDAPP) += rte_malloc.c
SRCS-$(CONFIG_RTE_EXEC_ENV_BSDAPP) += malloc_elem.c
SRCS-$(CONFIG_RTE_EXEC_ENV_BSDAPP) += malloc_heap.c
SRCS-$(CONFIG_RTE_EXEC_ENV_BSDAPP) += rte_keepalive.c
SRCS-$(CONFIG_RTE_EXEC_ENV_BSDAPP) += rte_service.c

# from arch dir
SRCS-$(CONFIG_RTE_EXEC_ENV_BSDAPP) += rte_cpuflags.c
SRCS-$(CONFIG_RTE_ARCH_X86) += rte_spinlock.c
SRCS-y += rte_cycles.c

# for run-time dispatch of memcpy
SRCS-$(CONFIG_RTE_ARCH_X86) += rte_memcpy.c
SRCS-$(CONFIG_RTE_ARCH_X86) += rte_memcpy_sse.c

# if the compiler supports AVX512, add avx512 file
ifneq ($(findstring CC_SUPPORT_AVX512F,$(MACHINE_CFLAGS)),)
SRCS-$(CONFIG_RTE_ARCH_X86) += rte_memcpy_avx512f.c
CFLAGS_rte_memcpy_avx512f.o += -mavx512f
CFLAGS_rte_memcpy_avx512f.o += -DRTE_MACHINE_CPUFLAG_AVX512F
endif

# if the compiler supports AVX2, add avx2 file
ifneq ($(findstring CC_SUPPORT_AVX2,$(MACHINE_CFLAGS)),)
SRCS-$(CONFIG_RTE_ARCH_X86) += rte_memcpy_avx2.c
CFLAGS_rte_memcpy_avx2.o += -mavx2
CFLAGS_rte_memcpy_avx2.o += -DRTE_MACHINE_CPUFLAG_AVX2
endif

CFLAGS_eal_common_cpuflags.o := $(CPUFLAGS_LIST)

CFLAGS_eal.o := -D_GNU_SOURCE
#CFLAGS_eal_thread.o := -D_GNU_SOURCE
CFLAGS_eal_log.o := -D_GNU_SOURCE
CFLAGS_eal_common_log.o := -D_GNU_SOURCE

# workaround for a gcc bug with noreturn attribute
# http://gcc.gnu.org/bugzilla/show_bug.cgi?id=12603
ifeq ($(CONFIG_RTE_TOOLCHAIN_GCC),y)
CFLAGS_eal_thread.o += -Wno-return-type
CFLAGS_eal_hpet.o += -Wno-return-type
endif

INC := rte_interrupts.h

SYMLINK-$(CONFIG_RTE_EXEC_ENV_BSDAPP)-include/exec-env := \
	$(addprefix include/exec-env/,$(INC))

include $(RTE_SDK)/mk/rte.lib.mk
