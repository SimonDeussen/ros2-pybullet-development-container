FROM ros2_install_source:latest

ARG UNAME=ros_user
ARG WS_DIR=/home/$UNAME/workspace/
ARG UID=1000
ARG GID=1000
RUN groupadd -g $GID -o $UNAME
RUN useradd -m -s /bin/bash -N -u $UID $UNAME && \
    adduser $UNAME sudo && \
    echo "$UNAME ALL=(ALL:ALL) NOPASSWD:ALL" | sudo tee /etc/sudoers.d/$UNAME && \
    mkdir -p $WS_DIR/src &&\
    chown $UNAME:$GID -R $WS_DIR

USER $UNAME
WORKDIR $WS_DIR/src

RUN pip3 install pybullet
RUN git clone https://github.com/oscar-lima/pybullet_ros.git

RUN echo "alias l=\"ls -alhG\"" >> ~/.bashrc
RUN echo "alias ..=\"cd ..\"" >> ~/.bashrc
RUN echo "alias src-ros=\"source /ros2_foxy/install/local_setup.bash\"" >> ~/.bashrc
RUN echo "source /usr/share/colcon_cd/function/colcon_cd.sh" >> ~/.bashrc
RUN echo "export _colcon_cd_root=~/ros2_foxy" >> ~/.bashrc
RUN echo "export ROS_DOMAIN_ID=69" >> ~/.bashrc


CMD /bin/bash