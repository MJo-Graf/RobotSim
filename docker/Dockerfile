FROM devcontainer:1.0.0

RUN sudo apt update && sudo apt install locales\
    && sudo locale-gen en_US en_US.UTF-8 \
    && sudo update-locale LC_ALL=en_US.UTF-8 LANG=en_US.UTF-8
ENV LANG=en_US.UTF-8

RUN sudo apt install -y software-properties-common\
 && sudo add-apt-repository universe\
 && sudo apt update && sudo apt install curl -y\
 && export ROS_APT_SOURCE_VERSION=$(curl -fsSL -o /dev/null -w '%{url_effective}' https://github.com/ros-infrastructure/ros-apt-source/releases/latest | awk -F/ '{print $NF}')\
 && curl -L -o /tmp/ros2-apt-source.deb "https://github.com/ros-infrastructure/ros-apt-source/releases/download/${ROS_APT_SOURCE_VERSION}/ros2-apt-source_${ROS_APT_SOURCE_VERSION}.$(. /etc/os-release && echo ${UBUNTU_CODENAME:-${VERSION_CODENAME}})_all.deb"\
 && sudo dpkg -i /tmp/ros2-apt-source.deb\
 && sudo apt update && sudo apt install -y ros-dev-tools\
 && sudo apt upgrade -y\
 && sudo apt install -y ros-lyrical-desktop

RUN echo "source /opt/ros/lyrical/setup.zsh" >> ~/.zshrc

#RUN wget https://downloads.isaacsim.nvidia.com/isaac-sim-standalone-6.0.0-linux-x86_64.zip --output-file=/tmp/isaac-sim-standalone-6.0.0-linux-x86_64.zip 
RUN wget https://downloads.isaacsim.nvidia.com/isaac-sim-standalone-6.0.0-linux-x86_64.zip -O /home/maximilian/isaac-sim-standalone-6.0.0-linux-x86_64.zip \
&& sudo unzip isaac-sim-standalone-6.0.0-linux-x86_64.zip -d /opt/isaac

#Workaround according to https://github.com/isaac-sim/IsaacSim/issues/848
#TODO: Remove this if possible
RUN cd /opt/isaac/extscache/omni.kit.asset_converter-5.1.4+110.1.0.lx64.r.cp312.u7f4/asset_converter_native_bindings/libs \
  && sudo ln -s libxml2.so.16 libxml2.so.2
