# L4T ROS Container Image

This is the fork from [aptpod/l4t-ros](https://github.com/aptpod/l4t-ros) that extends to Ubuntu 24.04 and ROS2 Jazzy.

The L4T ROS container image is a ROS (Robot Operating System) container image compatible with NVIDIA GPUs. It is based on an Ubuntu image and leverages the NVIDIA Container Runtime to enable NVIDIA GPU support while incorporating a ROS distribution.

## Requirements

The following tools are required to create this image:

- Docker  

## Creating the L4T Base Image

1. Use any version of the Ubuntu image as a base.  
2. Install the necessary tools required for the NVIDIA Container Runtime.  

Run the following commands to create the image:

```bash
sudo make UBUNTU_DISTRIB=noble L4T_BASE_REGISTRY=l4t-base L4T_CUDA_REGISTRY=l4t-cuda image
make UBUNTU_DISTRIB=noble L4T_BASE_REGISTRY=l4t-base push
```

| Variable         | Values                           |
|-----------------|--------------------------------|
| UBUNTU_DISTRIB  | noble, jammy, focal, bionic (default: noble) |

## Creating the L4T ROS Container Image

1. Install the ROS distribution on the L4T base image.  
2. Create a ROS container compatible with NVIDIA GPUs.  

Follow these steps:
- Navigate to the directory of the desired ROS distribution.  
- Run the following command:

```bash
make image
```

| ROS Distro     | Directory      |
|---------------|--------------|
| ROS2 Jazzy    | ros/jazzy    |
| ROS2 Humble   | ros/humble   |
| ROS2 Foxy     | ros/foxy     |
| ROS Noetic    | ros/noetic   |
| ROS Melodic   | ros/melodic  |

## Usage

The following command is an example of how to run the container, including GPU and GUI options:

```bash
xhost +local:
docker run -it --rm \
    --net=host \
    --runtime=nvidia \
    --gpus all \
    -e DISPLAY=$DISPLAY \
    -e QT_X11_NO_MITSHM=1 \
    -v /tmp/.X11-unix:/tmp/.X11-unix \
    damanikjosh/l4t-ros:jazzy-desktop-r32.7 \
    /bin/bash
```

## Acknowledgments and License

This project utilizes content from the following resources in compliance with the Apache License 2.0:

- **NVIDIA L4T Base Container Images**: [NVIDIA GitLab](https://gitlab.com/nvidia/container-images/l4t-base)  
- **Open Source Robotics Foundation Docker Images**: [GitHub Repository](https://github.com/osrf/docker_images)  

These resources are provided under the Apache License 2.0, and this project follows the terms of that license. For more details, please refer to the license files of each resource.
