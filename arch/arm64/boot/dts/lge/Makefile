ifeq ($(CONFIG_MACH_MSM8937_LGPS29),y)
DTS_TARGET := msm8937-lgps29
endif

ifeq ($(CONFIG_MACH_MSM8937_PH2_GLOBAL_COM),y)
DTS_TARGET := msm8937-ph2_global_com
endif

ifeq ($(CONFIG_MACH_MSM8937_PH2_CMO_CN),y)
DTS_TARGET := msm8937-ph2_cmo_cn
endif

ifeq ($(CONFIG_MACH_MSM8937_PH2N_TMO_US),y)
DTS_TARGET := msm8937-ph2n_tmo_us
endif

ifeq ($(CONFIG_MACH_MSM8937_PH2N_MPCS_US),y)
DTS_TARGET := msm8937-ph2n_mpcs_us
endif

ifeq ($(CONFIG_MACH_MSM8937_PH2N_GLOBAL_CA),y)
DTS_TARGET := msm8937-ph2n_global_ca
endif

ALL_DTS := $(notdir $(wildcard echo $(srctree)/$(src)/$(DTS_TARGET)/*.dts))
dtb-y += $(patsubst %.dts,%.dtb,$(ALL_DTS))

DTB_NAMES := $(subst $\",,$(CONFIG_BUILD_ARM_APPENDED_DTB_IMAGE_NAMES))
ifneq ($(DTB_NAMES),)
DTB_LIST := $(addsuffix .dtb,$(DTB_NAMES))
else
DTB_LIST := $(dtb-y)
endif

ifeq ($(CONFIG_ARM64),y)
always  := $(addprefix ../,$(DTB_LIST))

$(obj)/../%.dtb: $(src)/$(DTS_TARGET)/%.dts FORCE
	$(call if_changed_dep,dtc)
else
targets += dtbs
targets += $(addprefix ../, $(DTB_LIST))

$(obj)/../%.dtb: $(src)/$(DTS_TARGET)/%.dts FORCE
        $(call if_changed_dep,dtc)

dtbs: $(addprefix $(obj)/$(DTS_TARGET)/,$(DTB_LIST))
endif

clean-files := *.dtb
