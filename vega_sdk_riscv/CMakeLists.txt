# This CMakeLists.txt is being kept deliberately simple for now, since
# the HAL is currently only needed to support one SoC.

zephyr_include_directories(RISCV)
zephyr_include_directories(devices/RV32M1)

# The HAL uses a CPU name to expose core-specific features.
# For details see fsl_device_registers.h and 
# $CPU_RV32M1_{ri5cy,zero_riscy,m4,cm0plus}_features.h
if(CONFIG_SOC_OPENISA_RV32M1_RI5CY)
  zephyr_compile_definitions(CPU_RV32M1_ri5cy)
elseif(CONFIG_SOC_OPENISA_RV32M1_ZERO_RISCY)
  zephyr_compile_definitions(CPU_RV32M1_zero_riscy)
elseif(CONFIG_SOC_OPENISA_RV32M1_M4)
  zephyr_compile_definitions(CPU_RV32M1_cm4)
elseif(CONFIG_SOC_OPENISA_RV32M1_M0PLUS)
  zephyr_compile_definitions(CPU_RV32M1_cm0plus)
endif()

add_subdirectory(devices/RV32M1/drivers)
add_subdirectory(middleware)

zephyr_compile_definitions(XCVR_GENFSK_ENABLED)
