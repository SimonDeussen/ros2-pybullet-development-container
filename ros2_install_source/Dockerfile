ARG FROM_IMAGE=ubuntu:focal
FROM $FROM_IMAGE

ENV DEBIAN_FRONTEND=noninteractive

RUN apt update && apt install locales
RUN locale-gen en_US en_US.UTF-8
RUN update-locale LC_ALL=en_US.UTF-8 LANG=en_US.UTF-8
RUN export LANG=en_US.UTF-8

RUN apt update && apt install curl gnupg2 lsb-release -y
RUN curl -sSL https://raw.githubusercontent.com/ros/rosdistro/master/ros.key  -o /usr/share/keyrings/ros-archive-keyring.gpg

RUN echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/ros-archive-keyring.gpg] http://packages.ros.org/ros2/ubuntu $(lsb_release -cs) main" | tee /etc/apt/sources.list.d/ros2.list > /dev/null

RUN apt update && apt install -y \
  build-essential \
  cmake \
  git \
  libbullet-dev \
  python3-colcon-common-extensions \
  python3-flake8 \
  python3-pip \
  python3-pytest-cov \
  python3-rosdep \
  python3-setuptools \
  python3-vcstool \
  wget

# install some pip packages needed for testing
RUN python3 -m pip install -U \
  argcomplete \
  flake8-blind-except \
  flake8-builtins \
  flake8-class-newline \
  flake8-comprehensions \
  flake8-deprecated \
  flake8-docstrings \
  flake8-import-order \
  flake8-quotes \
  pytest-repeat \
  pytest-rerunfailures \
  pytest

# install Fast-RTPS dependencies
RUN apt install --no-install-recommends -y \
  libasio-dev \
  libtinyxml2-dev

# install Cyclone DDS dependencies
RUN apt install --no-install-recommends -y \
  libcunit1-dev

RUN mkdir -p ~/ros2_foxy/src
WORKDIR /ros2_foxy/src

RUN wget https://raw.githubusercontent.com/ros2/ros2/foxy/ros2.repos

RUN vcs import . < ros2.repos

RUN rosdep init && rosdep update 
RUN rosdep install --from-paths . --ignore-src --rosdistro foxy -y --skip-keys "console_bridge fastcdr fastrtps rti-connext-dds-5.3.1 urdfdom_headers"

WORKDIR /ros2_foxy/
RUN colcon build --symlink-install

RUN echo "alias l=\"ls -alhG\"" >> ~/.bashrc
RUN echo "alias ..=\"cd ..\"" >> ~/.bashrc
RUN echo "alias src-ros=\"source /ros2_foxy/install/local_setup.bash\"" >> ~/.bashrc
RUN echo "source /usr/share/colcon_cd/function/colcon_cd.sh" >> ~/.bashrc
RUN echo "export _colcon_cd_root=~/ros2_foxy" >> ~/.bashrc
RUN echo "export ROS_DOMAIN_ID=69" >> ~/.bashrc

CMD /bin/bash