cmake_minimum_required(VERSION 2.8.3)
project(fake_localization)

find_package(catkin REQUIRED
        COMPONENTS
            angles
            roscpp
            rosconsole
            nav_msgs
            geometry_msgs
            tf
            message_filters
        )


find_package(Boost REQUIRED COMPONENTS signals)

catkin_package(
    CATKIN_DEPENDS
        roscpp
        rospy
)

add_executable(fake_localization fake_localization.cpp)
target_link_libraries(fake_localization
    ${catkin_LIBRARIES}
    ${Boost_LIBRARIES}
    )

add_dependencies(fake_localization nav_msgs_gencpp)
add_dependencies(fake_localization geometry_msgs_gencpp)

install(
    PROGRAMS
       static_odom_broadcaster.py
    DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION}
)

install(
    TARGETS
        fake_localization
    DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION}
)
