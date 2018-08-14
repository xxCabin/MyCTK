cmake_minimum_required(VERSION 3.9.1)

# ָ����������
project(WelcomeCTK)

# ָ��Ϊ��̬��
option(BUILD_SHARED_LIBS  "Build CTK Plugin" ON)

# CTK ��װ·��
set(CTK_INSTALL_PATH ${CMAKE_CURRENT_SOURCE_DIR}/../../CTK-master/CTKInstall)

# ���� CTK ��ص�ͷ�ļ�����·��
include_directories(${CTK_INSTALL_PATH}/include/ctk-0.1)
include_directories(${CMAKE_CURRENT_SOURCE_DIR}/../../CTK-master/CTK-master/Libs/PluginFramework)

# ���� CTK ��صĿ��ļ�
find_library(CORE_LIB CTKCore ${CTK_INSTALL_PATH}/lib/ctk-0.1 NO_DEFAULT_PATH)
find_library(FRAMEWORK_LIB CTKPluginFramework ${CTK_INSTALL_PATH}/lib/ctk-0.1 NO_DEFAULT_PATH)
link_libraries(${CORE_LIB} ${FRAMEWORK_LIB})

# �����Զ����� moc �ļ�
set(CMAKE_AUTOMOC ON)

# ������Ҫ�� Qt ���ļ�
find_package(Qt5Core)

# �ļ����е�����ͷ�ļ���Դ�ļ�
file(GLOB HEADER_FILES ${CMAKE_CURRENT_SOURCE_DIR}/*.h)
file(GLOB SRC_FILES ${CMAKE_CURRENT_SOURCE_DIR}/*.cpp)

# ������Դ�ļ�
set(QRC_SOURCE_FILES ${CMAKE_CURRENT_SOURCE_DIR}/Resource.qrc)
qt5_add_resources(QRC_FILES ${QRC_SOURCE_FILES})

# ���ɿ�
add_library(${PROJECT_NAME} ${HEADER_FILES} ${SRC_FILES} ${QRC_FILES})

# Ϊ target ������Ҫ���ӵĿ�
target_link_libraries(${PROJECT_NAME} Qt5::Core)