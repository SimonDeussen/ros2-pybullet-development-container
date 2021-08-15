# Modern development with ROS2 in GUI-supported container.

## Instructions for using:

1. Open the repository folder `ros2-pybullet-development-container` with VSCode and execute `Remote Containers: Open folder in Container`


## Instructions for development:

(use development branch)

1. Build the `ros2_install_source` container: `cd ros2_install_source && docker build -f Dockerfile -t ros2_install_source .` (This will take a WHILE, compiles ros2 from source)
2. Build the `ros2_pybullet_gui` container: `cd ros2_pybullet_gui && docker build -f Dockerfile -t ros2_pybullet_gui .`
3. create folder called in the root of this directory `workspace` - this folder will contain all everything created in the colcon workspace inside the container.
3. Open the repository folder `ros2-pybullet-development-container` with VSCode and execute `Remote Containers: Open folder in Container`