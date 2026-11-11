cmake_minimum_required(VERSION 3.16)
project(ImageLab VERSION 1.0.0 LANGUAGES CXX)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# Procura os componentes do Qt6 necessários
find_package(Qt6 REQUIRED COMPONENTS Core Widgets)

# Adiciona o executável com os arquivos modularizados
add_executable(ImageLab
    main.cpp
    mainwindow.cpp
    mainwindow.h
    funcoes.cpp
    funcoes.h
)

# Conecta as bibliotecas do Qt ao projeto
target_link_libraries(ImageLab PRIVATE Qt6::Core Qt6::Widgets)

# Caminhos de arquivo chegam em UTF-8; no Windows o stb precisa saber disso
target_compile_definitions(ImageLab PRIVATE STBI_WINDOWS_UTF8 STBIW_WINDOWS_UTF8)

# Sem janela de console no Windows
set_target_properties(ImageLab PROPERTIES WIN32_EXECUTABLE ON)

include(GNUInstallDirs)
install(TARGETS ImageLab RUNTIME DESTINATION ${CMAKE_INSTALL_BINDIR})

# Fontes em UTF-8 (comentários acentuados)
if(MSVC)
    target_compile_options(ImageLab PRIVATE /utf-8)
endif()
