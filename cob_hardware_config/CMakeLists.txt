cmake_minimum_required(VERSION 2.8.3)
project(cob_hardware_config)

find_package(catkin REQUIRED COMPONENTS roslaunch rostest)

catkin_package()

set(robotlist
    cob3-2
    cob3-6
    cob3-9
    cob4-1
    cob4-2
    cob4-3
    cob4-4
    cob4-5
    cob4-6
    raw3-1
    raw3-2
    raw3-3
    raw3-4
    raw3-5
    raw3-6
)

### TESTING ###
if(CATKIN_ENABLE_TESTING)
    # loop through list of robots for testing
    foreach(robot ${robotlist})
        message("testing for robot: ${robot}")
        roslaunch_add_file_check(common robot:=${robot})
        roslaunch_add_file_check(common ROBOT=${robot})
        add_rostest(test/urdf_${robot}.test)
    endforeach()
endif()

### INSTALL ###
foreach(robot ${robotlist})
    install(DIRECTORY ${robot}
        DESTINATION ${CATKIN_PACKAGE_SHARE_DESTINATION}
    )
endforeach()

install(DIRECTORY common test
    DESTINATION ${CATKIN_PACKAGE_SHARE_DESTINATION}
)
