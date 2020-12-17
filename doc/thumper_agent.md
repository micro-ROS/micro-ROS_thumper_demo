## Running the micro-ROS agent over 6LoWPAN on the Thumper demo 

- Install wpan-tools on the PC.

```
sudo apt-get update -y
sudo apt-get install -y wpan-tools
```

Having the ATUSB adapter inserted into a USB port on PC, run the script [wpan_atusb.sh](../atusb/wpan_atusb_sh.md) in sudo mode to configure the `6lowpan` interface.
Then, the `lowpan0` interface is ready to be used, so the  communication with the joystick and Thumper 6LoWPAN devices can be established. 

- Download the micro-ROS agent Foxy image from  the [Docker Hub](https://hub.docker.com/), then run the agent in udp IPv6 addressing mode. 

```
docker pull microros/micro-ros-agent:foxy
docker run -it --net=host microros/micro-ros-agent:foxy udp6 --port 9999 -v6
```

The agent is ready to work with micro-ROS clients over 6lowpan.