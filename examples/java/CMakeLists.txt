# The purpose of this CMakeLists.txt is to compile all listed JAVA examples
# during build time (ensuring that ALL examples compile against their
# dependency JAVA packages).

find_package(Java REQUIRED)
include(UseJava)

# Add a JAVA example target for the provided JAVA source file which depends
# on UPM JAVA targets.
#
# Usage:
#   add_example(example_class_name upm_target_dependency_list)
#
# Parameters:
#   example_class_name: JAVA class name.  This name MUST match the JAVA
#                       example file name.
#                       <example_class_name>.java
#   upm_target_dependency_list: One or more UPM library targets.  This
#                       function assumes a javaupm_<target> also exists.
#
# Examples:
#   # Creates SensorFooExample JAVA target, depends on target: sensorfoo,
#   # and will add upm_sensorfoo.jar to the javac classpath.
#   add_example(SensorFooExample sensorfoo)
#
#   # Creates SensorFooExample JAVA target, depends on targets: sensorfoo,
#   # and interfaces and will add both upm_sensorfoo.jar and upm_interfaces.jar
#   # to the javac classpath.
#   add_example(SensorFooExample "sensorfoo;interfaces"")
#
function(add_example example_class_name dependency_list)
    set(example_file "${example_class_name}.java")

    # Build a list of all dependency jar files
    set(jar_file_list "")

    # Build a list of all dependency java target names
    set(java_targets_list "")

    # Iterate over the dependencies
    foreach(dependency ${dependency_list})
        set(java_target "javaupm_${dependency}")

        # Append to the targets list
        list(APPEND java_targets_list ${java_target})

        # If a dependency target does NOT exist, print a warning and skip
        if (NOT TARGET ${java_target})
            message(STATUS "Example ${example_file} is missing a required CMake target (${java_target}), skipping...")
            return()
        endif()

        # Get the jar for this java_target (saved as a property)
        get_target_property(jar_file ${java_target} JAR_FILE_ABSOLUTE)

        # Append to the jar list
        list(APPEND jar_file_list ${jar_file})
    endforeach()

    # Add the jar/s
    add_jar(${example_class_name} SOURCES ${example_file} INCLUDE_JARS ${jar_file_list})

    # Add a dependency from this jar to all dependency java targets
    add_dependencies(${example_class_name} ${java_targets_list})
endfunction()

add_example(A110X_Example "a110x;interfaces")
add_example(A110X_intr_Example "a110x;interfaces")
add_example(Ad8232_Example ad8232)
add_example(ADC121C021_Example adc121c021)
add_example(Ads1015_Example "ads1x15")
add_example(Ads1115_Example ads1x15)
add_example(Adxl345_Example adxl345)
add_example(AM2315_Example "am2315;interfaces")
add_example(APA102_Example apa102)
add_example(Apds9002_Example "apds9002;interfaces")
add_example(BH1750_Example "bh1750;interfaces")
add_example(BISS0001_Example "biss0001;interfaces")
add_example(BMA250E_Example "bma250e;interfaces")
add_example(BMC150_Example "bmx055;interfaces")
add_example(BME280_Example "bmp280;interfaces")
add_example(BMG160_Example "bmg160;interfaces")
add_example(BMI055_Example "bmx055;interfaces")
add_example(BMI160_Example "bmi160;interfaces")
add_example(BMM150_Example "bmm150;interfaces")
add_example(BMP280_Example "bmp280;interfaces")
add_example(BMPX8X_Example "bmpx8x;interfaces")
add_example(BMX055_Example "bmx055;interfaces")
add_example(BNO055_Example bno055)
add_example(Button_Example "button;interfaces")
add_example(Button_intr_Example "button;interfaces")
add_example(Buzzer_Example buzzer)
add_example(CJQ4435_Example cjq4435)
add_example(Collision_Example "collision;interfaces")
add_example(CWLSXXA_Example "cwlsxxa;interfaces")
add_example(DFREC_Example "dfrec;interfaces")
add_example(DFRORP_Example "dfrorp;interfaces")
add_example(DS1307_Example ds1307)
add_example(ECEZO_Example "ecezo;interfaces")
add_example(ECS1030_Example ecs1030)
add_example(EHR_Example "ehr;interfaces")
add_example(Emg_Example "emg;interfaces")
add_example(ENC03R_Example enc03r)
add_example(ES08A_Example "servo")
add_example(FlexSensor_Example flex)
add_example(Gp2y0a_Example "gp2y0a;interfaces")
add_example(GroveLEDBar_Example my9221)
add_example(GroveMQ3_Example "gas;interfaces")
add_example(GroveMQ9_Example "gas;interfaces")
add_example(GroveQTouch_Example at42qt1070)
add_example(Gsr_Example "gsr;interfaces")
add_example(GUVAS12D_Example guvas12d)
add_example(H3LIS331DL_Example "h3lis331dl;interfaces")
add_example(HCSR04_Example "hcsr04;interfaces")
add_example(HKA5_Example hka5)
add_example(HM11_Example hm11)
add_example(Hmc5883l_Example hmc5883l)
add_example(HMTRP_Example hmtrp)
add_example(HP20x_Example "hp20x;interfaces")
add_example(HTU21D_Example "htu21d;interfaces")
add_example(Itg3200_Example "itg3200;interfaces")
add_example(Jhd1313m1_Example jhd1313m1)
add_example(Jhd1313m1_lcd_Example jhd1313m1)
add_example(Joystick12_Example joystick12)
add_example(KX122_Example kx122)
add_example(KXTJ3_Example kxtj3)
add_example(Lcm1602_i2c_Example lcm1602)
add_example(Lcm1602_parallel_Example lcm1602)
add_example(LDT0028_Example ldt0028)
add_example(LE910_Example uartat)
add_example(LED_Example led)
add_example(Light_Example "light;interfaces")
add_example(LineFinder_Example "linefinder;interfaces")
add_example(LIS2DS12_Example "lis2ds12;interfaces")
add_example(LoL_Example lol)
add_example(LSM303AGR_Example "lsm303agr;interfaces")
add_example(LSM303D_Example "lsm303d;interfaces")
add_example(LSM303DLH_Example lsm303dlh)
add_example(LSM6DS3H_Example "lsm6ds3h;interfaces")
add_example(LSM6DSL_Example "lsm6dsl;interfaces")
add_example(M24LR64E_Example m24lr64e)
add_example(MAX30100_Example max30100)
add_example(MAX31855_Example max31855)
add_example(MAX44000_Example "max44000;interfaces")
add_example(MAX5487_Example max5487)
add_example(MAXds3231m_Example maxds3231m)
add_example(MB704X_Example "mb704x;interfaces")
add_example(MCP2515_Example mcp2515)
add_example(MCP2515_TXRX_Example mcp2515)
add_example(MD_Example md)
add_example(MHZ16_Example "mhz16;interfaces")
add_example(Microphone_Example mic)
add_example(MMA7361_Example mma7361)
add_example(MMA7455_Example "mma7455;interfaces")
add_example(MMA7660_Example "mma7660;interfaces")
add_example(Moisture_Example "moisture;interfaces")
add_example(MPL3115A2_Example "mpl3115a2;interfaces")
add_example(MPR121_Example mpr121)
add_example(MPU9150_Example "mpu9150;interfaces")
add_example(MQ2_Example "gas;interfaces")
add_example(MQ4_Example "gas;interfaces")
add_example(MQ5_Example "gas;interfaces")
add_example(MQ6_Example "gas;interfaces")
add_example(MQ7_Example "gas;interfaces")
add_example(MQ8_Example "gas;interfaces")
add_example(MQ303A_Example mq303a)
add_example(MS5803_Example "ms5803;interfaces")
add_example(NMEAGPS_Example nmea_gps)
add_example(NMEAGPS_I2C_Example nmea_gps)
add_example(NRF24L01_receiver_Example nrf24l01)
add_example(NRF24L01_transmitter_Example nrf24l01)
add_example(NUNCHUCK_Example nunchuck)
add_example(O2_Example "o2;interfaces")
add_example(OTP538U_Example "otp538u;interfaces")
add_example(P9813_Example p9813)
add_example(PPD42NS_Example ppd42ns)
add_example(Pulsensor_Example pulsensor)
add_example(Relay_Example relay)
add_example(RFR359F_Example "rfr359f;interfaces")
add_example(RN2903_Example rn2903)
add_example(RN2903_P2P_RX_Example rn2903)
add_example(RN2903_P2P_TX_Example rn2903)
add_example(RotaryEncoder_Example "rotaryencoder;interfaces")
add_example(Rotary_Example "rotary;interfaces")
add_example(RPR220_Example rpr220)
add_example(RPR220_intr_Example rpr220)
add_example(SCAM_Example scam)
add_example(SensorTemplate_Example sensortemplate)
add_example(SHT1X_Example "sht1x;interfaces")
add_example(Slide_Example slide)
add_example(SM130_Example sm130)
add_example(Speaker_Example speaker)
add_example(SpeakerPWM_Example speaker)
add_example(SSD1308_oled_Example lcd)
add_example(SSD1327_oled_Example lcd)
add_example(ST7735_Example st7735)
add_example(TEAMS_Example "teams;interfaces")
add_example(Temperature_Example "temperature;interfaces")
add_example(TEX00_Example "tex00;interfaces")
add_example(Th02_Example "th02;interfaces")
add_example(TM1637_Example tm1637)
add_example(TP401_Example "gas;interfaces")
add_example(TSL2561_Example "tsl2561;interfaces")
add_example(TTP223_Example "ttp223;interfaces")
add_example(ULN200XA_Example uln200xa)
add_example(VDiv_Example "vdiv;interfaces")
add_example(VEML6070_Example veml6070)
add_example(Water_Example "water;interfaces")
add_example(WaterLevelSensor_Example waterlevel)
add_example(WFS_Example wfs)
add_example(WT5001_Example wt5001)
add_example(YG1006_Example yg1006)
add_example(ZFM20_Example zfm20)

if(SWIG_VERSION VERSION_GREATER 3.0.8)
    add_example(BME280_Interface_Example "bmp280;interfaces")
    add_example(IMS_Example "ims;interfaces")
    add_example(RHUSB_Example "rhusb;interfaces")
endif()

if (OPENZWAVE_FOUND)
    add_example(AeotecDSB09104_Example ozw)
    add_example(AeotecDW2E_Example ozw)
    add_example(AeotecSDG2_Example ozw)
    add_example(AeotecSS6_Example ozw)
    add_example(TZEMT400_Example ozw)
endif()

if (MODBUS_FOUND)
    add_example(H803X_Example h803x)
endif()

if (BACNET_FOUND)
    add_example(E50HX_Example e50hx)
    add_example(T8100_Example t8100)
    add_example(TB7300_Example tb7300)
endif()

if (JPEG_FOUND)
    add_example(VCAP_Example vcap)
endif()

if (NOT ANDROID)
    add_example(StepMotor_Example stepmotor)
endif ()
