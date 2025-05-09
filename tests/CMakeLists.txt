ExternalProject_Add(ceeaus
  SOURCE_DIR ${meta_BINARY_DIR}/../../data/ceeaus
  DOWNLOAD_DIR ${meta_BINARY_DIR}/downloads
  URL https://web.archive.org/web/20220616030242if_/https://meta-toolkit.org/data/2016-01-26/ceeaus.tar.gz 
  URL_HASH "SHA256=83616fe13563786a1a6701f40ee0dc044bf32d1273e0ad53ca72582a90bed9ef"
  CONFIGURE_COMMAND ""
  BUILD_COMMAND ""
  INSTALL_COMMAND "")

ExternalProject_Add(breast-cancer
  SOURCE_DIR ${meta_BINARY_DIR}/../../data/breast-cancer
  DOWNLOAD_DIR ${meta_BINARY_DIR}/../downloads
  URL http://162.218.114.106/data/breast-cancer.tar.gz
  URL_HASH "SHA256=28a87b30d651c9b14ebf4e125c9f532233d7970b7bb19e4b1cb8c4f4ccd0d125"
  CONFIGURE_COMMAND ""
  BUILD_COMMAND ""
  INSTALL_COMMAND "")

ExternalProject_Add(housing
  SOURCE_DIR ${meta_BINARY_DIR}/../../data/housing
  DOWNLOAD_DIR ${meta_BINARY_DIR}/../downloads
  URL http://162.218.114.106/data/housing.tar.gz
  URL_HASH "SHA256=555aee6a3cc4fdae089eb91c60c682ef6136d15c33aa8d554cd1b47cb43a64d4"
  CONFIGURE_COMMAND ""
  BUILD_COMMAND ""
  INSTALL_COMMAND "")

ExternalProject_Add(cranfield
  SOURCE_DIR ${meta_BINARY_DIR}/../../data/cranfield
  DOWNLOAD_DIR ${meta_BINARY_DIR}/../downloads
  URL http://162.218.114.106/data/cranfield.tar.gz
  URL_HASH "SHA256=507b6f4f133bc1a65d140780cbd7060a3ca159410b772e5eb1e2c12b215d72b4"
  CONFIGURE_COMMAND ""
  BUILD_COMMAND ""
  INSTALL_COMMAND "")

# Ignore sign warnings when expanding bandit's macros.
file(GLOB BANDIT_SOURCE_FILES *.cpp)
set_property(SOURCE ${BANDIT_SOURCE_FILES} APPEND PROPERTY COMPILE_FLAGS
    " -Wno-sign-conversion -Wno-conversion")
add_executable(unit-test ${BANDIT_SOURCE_FILES})
add_dependencies(unit-test ceeaus breast-cancer)
target_include_directories(unit-test PUBLIC ${meta_SOURCE_DIR}/../deps/bandit/)
target_link_libraries(unit-test meta-index
                                meta-classify
                                meta-regression
                                meta-stats
                                meta-parser
                                meta-features
                                meta-language-model
                                meta-succinct
                                meta-topics)
