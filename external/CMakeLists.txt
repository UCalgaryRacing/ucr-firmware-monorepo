cmake_minimum_required(VERSION 3.22)


# Ideally we would create the library targets here, but each application has different HAL configuration
# options which are passed back to the HAL drivers through a header, so the library must be built separately
# for each application. Thus, the libraries are created in each application's CMakeLists.txt instead.