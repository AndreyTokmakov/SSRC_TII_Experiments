cmake_minimum_required(VERSION 3.21)
project(SSRC_TII_Experiments)

set(CMAKE_CXX_STANDARD 26)

# 5.15 - My home Ubuntu-20.04
if (CMAKE_SYSTEM_VERSION MATCHES "5.15")
    set(THIRD_PARTY_DIR /home/andtokm/DiskS/ProjectsUbuntu/third_party)
    set(EXTRA_LIBS tbb)
else()
    set(THIRD_PARTY_DIR /home/andtokm/Projects/third_party)
endif()

# add_subdirectory(Utilities)

# LibSerial headers:
include_directories(${THIRD_PARTY_DIR}/libserial/src)
include_directories(${THIRD_PARTY_DIR}/libserial/src/libserial)
link_directories(${THIRD_PARTY_DIR}/libserial/build/lib)

# LibPCAP
# include_directories(${THIRD_PARTY_DIR}/libpcap)
# link_directories(${THIRD_PARTY_DIR}/libpcap/build)

# include all components
add_executable(${PROJECT_NAME} MACOSX_BUNDLE
        main.cpp
        Networking/Headers/ARPHeader.h
        Networking/Headers/EthernetHeader.h
        Networking/Headers/IPv4Header.h
        Networking/Headers/TCPHeader.h
        Networking/Headers/UDPHeader.h
        Networking/Headers/ICMPHeader.h
        Networking/Utils/Utilities.cpp
        Networking/Utils/Utilities.h
        Serial/LinuxSerial.cpp
        Serial/LinuxSerial.h
        Networking/Networking.cpp
        Networking/Networking.h
        Serial/SerialPort.h
        Serial/Exception.h
        Serial/SerialPort.cpp
        LibSerial/LibSerial.cpp
        LibSerial/LibSerial.h
        LibPcap/LibPcapExperiments.cpp
        LibPcap/LibPcapExperiments.h
        LibPcap/config.h
        WiFi/WiFiScanner.cpp
        WiFi/WiFiScanner.h
        ContikiDCube/ContikiDCube.cpp
        ContikiDCube/ContikiDCube.h
)

TARGET_LINK_LIBRARIES(${PROJECT_NAME}
        -ldl
        libserial.a
        libpcap.a
)