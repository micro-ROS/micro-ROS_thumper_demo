## Building the Olimex STM32-E407 firmware of the Thumper demo


Use the Docker installation on PC to prepare the environment for the demo applications:
- Download the micro-ROS base Foxy image from  [the Docker Hub](https://hub.docker.com/), then run a docker container.

```
sudo docker pull microros/base:foxy
sudo docker run -it --net=host --privileged -v /dev/bus/usb:/dev/bus/usb     microros/base:foxy
```
- Create a ROS 2 workspace in the `uros_ws` folder of the docker container and build the package.

```
source /opt/ros/$ROS_DISTRO/setup.bash
git clone -b $ROS_DISTRO https://github.com/micro-ROS/micro_ros_setup.git src/micro_ros_setup
apt update && rosdep update
rosdep install --from-path src --ignore-src -y
apt-get install python3-pip
apt-get -y install python3-pip
colcon build
source install/local_setup.bas
```
- Create the Nuttx firmware on Olimex STM32-E407 with the Thumper demo applications.

```
ros2 run micro_ros_setup create_firmware_ws.sh nuttx olimex-stm32-e407
cd firmware/NuttX
git checkout -t origin/ucs_demo_f
cd ../apps
git checkout -t origin/ucs_demo_f
cd ..
```
Build and flash the firmware.
- Set the config profile variable to select the  joystick publisher or vehicle subcriber application.

```
CFG_PROFILE=uct_jspublisher_romfs
```
or

```
CFG_PROFILE=uct_jspublisher_romfs
```

- Build the application.

```
ros2 run micro_ros_setup configure_firmware.sh $CFG_PROFILE
cp firmware/NuttX/configs/olimex-stm32-e407/$CFG_PROFILE/rcS.template firmware/apps/nshlib/rcS.template
cd firmware/apps/nshlib/
../../NuttX/tools/mkromfsimg.sh -nofat ../../NuttX/
cd /uros_ws/
ros2 run micro_ros_setup build_firmware.sh
ros2 run micro_ros_setup flash_firmware.sh
```
- Connect ST-Link/V2 to  the Olimex STM32-E407 JTAG interface and flash the firmware:

```
ros2 run micro_ros_setup flash_firmware.sh
```  
