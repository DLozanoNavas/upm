set (libname "th02")
set (libdescription "Temperature and Humidity Sensor Pro")
set (module_src ${libname}.cxx)
set (module_hpp ${libname}.hpp)
set (module_iface iHumidity.hpp iTemperature.hpp)
upm_module_init(mraa)
