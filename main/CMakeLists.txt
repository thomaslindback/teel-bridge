#
#    Copyright (c) 2021 Project CHIP Authors
#    All rights reserved.
#
#    Licensed under the Apache License, Version 2.0 (the "License");
#    you may not use this file except in compliance with the License.
#    You may obtain a copy of the License at
#
#        http://www.apache.org/licenses/LICENSE-2.0
#
#    Unless required by applicable law or agreed to in writing, software
#    distributed under the License is distributed on an "AS IS" BASIS,
#    WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
#    See the License for the specific language governing permissions and
#    limitations under the License.

get_filename_component(CHIP_ROOT $ENV{IDF_PATH}/../connectedhomeip-1.2.0.1 REALPATH)

idf_component_register(PRIV_INCLUDE_DIRS
                      "${CMAKE_CURRENT_LIST_DIR}/include"
                      "${CHIP_ROOT}/examples/providers"
                      SRC_DIRS
                      "${CMAKE_CURRENT_LIST_DIR}"
                      "${CHIP_ROOT}/zzz_generated/app-common/app-common/zap-generated/attributes"
                      "${CHIP_ROOT}/zzz_generated/app-common/app-common/zap-generated"
                      "${CHIP_ROOT}/src/app/server"
                      "${CHIP_ROOT}/src/app/util"
                      "${CHIP_ROOT}/src/app/reporting"
                      "${CHIP_ROOT}/src/app/clusters/access-control-server"
                      "${CHIP_ROOT}/src/app/clusters/administrator-commissioning-server"
                      "${CHIP_ROOT}/src/app/clusters/basic-information"
                      "${CHIP_ROOT}/src/app/clusters/bridged-device-basic-information-server"
                      "${CHIP_ROOT}/src/app/clusters/level-control"
                      "${CHIP_ROOT}/src/app/clusters/identify-server"
                      "${CHIP_ROOT}/src/app/clusters/diagnostic-logs-server"
                      "${CHIP_ROOT}/src/app/clusters/ethernet-network-diagnostics-server"
                      "${CHIP_ROOT}/src/app/clusters/localization-configuration-server"
                      "${CHIP_ROOT}/src/app/clusters/time-format-localization-server"
                      "${CHIP_ROOT}/src/app/clusters/fixed-label-server"
                      "${CHIP_ROOT}/src/app/clusters/user-label-server"
                      "${CHIP_ROOT}/src/app/clusters/thread-network-diagnostics-server"
                      "${CHIP_ROOT}/src/app/clusters/wifi-network-diagnostics-server"
                      "${CHIP_ROOT}/src/app/clusters/software-diagnostics-server"
                      "${CHIP_ROOT}/src/app/clusters/switch-server"
                      "${CHIP_ROOT}/src/app/clusters/general-diagnostics-server"
                      "${CHIP_ROOT}/src/app/clusters/group-key-mgmt-server"
                      "${CHIP_ROOT}/src/app/clusters/descriptor"
                      "${CHIP_ROOT}/src/app/clusters/network-commissioning"
                      "${CHIP_ROOT}/src/app/clusters/on-off-server"
                      "${CHIP_ROOT}/src/app/clusters/operational-credentials-server"
                      "${CHIP_ROOT}/src/app/clusters/general-commissioning-server"
                      "${CHIP_ROOT}/examples/platform/esp32/common"
                      "${CHIP_ROOT}/examples/providers"
                      PRIV_REQUIRES chip QRCode bt nvs_flash)

include("${CHIP_ROOT}/build/chip/esp32/esp32_codegen.cmake")

#chip_app_component_codegen("${CHIP_ROOT}/examples/bridge-app/bridge-common/bridge-app.matter")
#chip_app_component_zapgen("${CHIP_ROOT}/examples/bridge-app/bridge-common/bridge-app.zap")
chip_app_component_codegen("${CMAKE_SOURCE_DIR}/model/bridge-app.matter")
chip_app_component_zapgen("${CMAKE_SOURCE_DIR}/model/bridge-app.zap")

set_property(TARGET ${COMPONENT_LIB} PROPERTY CXX_STANDARD 17)
target_compile_options(${COMPONENT_LIB} PRIVATE "-DCHIP_HAVE_CONFIG_H")
target_compile_options(${COMPONENT_LIB} PUBLIC
           "-DCHIP_ADDRESS_RESOLVE_IMPL_INCLUDE_HEADER=<lib/address_resolve/AddressResolve_DefaultImpl.h>"
)
