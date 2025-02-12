ROS_DISTRO?=foxy
BASE_IMAGE_NAME?=damanikjosh/l4t-ros
RELEASE?=r32.7

BASE_IMAGE=$(BASE_IMAGE_NAME)
DOCKER_CMD?=docker

all: image

image:
	${DOCKER_CMD} build -t $(BASE_IMAGE):$(ROS_DISTRO)-ros-core-$(RELEASE) -f ros-core/Dockerfile ros-core
	${DOCKER_CMD} build -t $(BASE_IMAGE):$(ROS_DISTRO)-ros-base-$(RELEASE) -f ros-base/Dockerfile ros-base
	${DOCKER_CMD} build -t $(BASE_IMAGE):$(ROS_DISTRO)-desktop-$(RELEASE) -f desktop/Dockerfile desktop
