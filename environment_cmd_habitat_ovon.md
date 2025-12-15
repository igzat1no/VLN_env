1. conda create env
conda create -n habitat_ovon python=3.12.3

2. torch
pip install torch==2.5.1 torchvision==0.20.1 torchaudio==2.5.1

3. other dependencies
git clone https://github.com/igzat1no/VLN_env.git
pip install -r requirements_ovon.txt --no-dependencies

- habitat-sim
git clone --branch stable https://github.com/facebookresearch/habitat-sim.git
cd habitat-sim
git checkout v0.2.3
**add --break-system-packages to setup.py:488**
python setup.py install --headless --with-cuda --bullet
cd ..

- habitat-lab
git clone --branch stable https://github.com/facebookresearch/habitat-lab.git
cd habitat-lab
git checkout v0.2.3
**modify files**
pip install -e habitat-lab
pip install -e habitat-baselines
cd ..
<!-- **modify habitat-lab/habitat-lab/habitat/core/env.py, comment out line 105-107**
**change habitat-lab/habitat-lab/habitat/config/default_structured_configs.py to the file on github: VLN_env/default_structured_configs.py** -->

- VLM_ROS
git clone git@github.com:zwandering/VLM_ROS.git
<!-- cd VLM_ROS/src/semantic_mapping/semantic_mapping/external
git clone https://github.com/IDEA-Research/Grounded-SAM-2.git
pip install Grounded-SAM-2/grounding_dino/
pip install Grounded-SAM-2/
pip install byte_track/ cython_bbox/ -->

- detectron2
python -m pip install 'git+https://github.com/facebookresearch/detectron2.git' --no-build-isolation

- mm
mim install mmengine
mim install mmcv==2.1.0
git clone https://github.com/open-mmlab/mmdetection.git
cd mmdetection
pip install -v -e . --no-build-isolation

- pytorch3d
pip install "git+https://github.com/facebookresearch/pytorch3d.git" --no-build-isolation

- sam2
git clone https://github.com/facebookresearch/sam2.git && cd sam2
pip install -e .

- en_core_web_sm
python -m spacy download en_core_web_sm

- ovon
git clone https://github.com/naokiyokoyama/ovon.git
cd ovon
**modify files**
git submodule update --init --recursive
pip install -e .
cd frontier_exploration/ && pip install -e . && cd ..

4. ros-jazzy
sudo apt update && sudo apt install locales
sudo locale-gen en_US en_US.UTF-8
sudo update-locale LC_ALL=en_US.UTF-8 LANG=en_US.UTF-8
export LANG=en_US.UTF-8
sudo apt install software-properties-common
sudo add-apt-repository universe
sudo apt update && sudo apt install curl -y
export ROS_APT_SOURCE_VERSION=$(curl -s https://api.github.com/repos/ros-infrastructure/ros-apt-source/releases/latest | grep -F "tag_name" | awk -F\" '{print $4}')
curl -L -o /tmp/ros2-apt-source.deb "https://github.com/ros-infrastructure/ros-apt-source/releases/download/${ROS_APT_SOURCE_VERSION}/ros2-apt-source_${ROS_APT_SOURCE_VERSION}.$(. /etc/os-release && echo ${UBUNTU_CODENAME:-${VERSION_CODENAME}})_all.deb"
sudo dpkg -i /tmp/ros2-apt-source.deb
sudo apt update && sudo apt install ros-dev-tools
sudo apt update
sudo apt upgrade
sudo apt install ros-jazzy-desktop
sudo apt install ros-jazzy-desktop-full ros-jazzy-pcl-ros libpcl-dev git cmake libgoogle-glog-dev libgflags-dev libatlas-base-dev libeigen3-dev libsuitesparse-dev

5. prepare dataset & update habitat.yaml & rviz in VLM_ROS & prepare yolo engine
