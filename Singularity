Bootstrap: docker
From: debian:stretch-slim

%labels
Author "Randall Cab White - rcwhite@stanford.edu"


#########
#%setup
#########

#Downlaod packages
%post
  apt-get -ymq update
  apt-get -ymq install chromium-shell chromium-l10n chromium-driver chromium make build-essential libssl-dev zlib1g-dev libbz2-dev \
libreadline-dev libsqlite3-dev wget curl llvm libncurses5-dev libncursesw5-dev \
xz-utils tk-dev libffi-dev liblzma-dev

#build directory
mkdir -p /python_build
cd /python_build

#download python
wget https://www.python.org/ftp/python/3.9.0/Python-3.9.0.tar.xz
tar xf ./Python-3.9.0.tar.xz
cd Python-3.9.0


#install python 3.9.0
./configure --enable-optimizations --enable-shared
make -j8
make install

#clean the installation
cd /
rm -rf /python_build

#install pip stuff
export PATH=/usr/local/bin:$PATH
export LD_LIBRARY_PATH=/usr/local/lib:$LD_LIBRARY_PATH


#make symbolic links
cd /usr/local/bin
ln -s python3.9 python
ln -s pip3.9 pip

#bootstrap libraries
ldconfig 

#now install pip stuff
pip3.9 install bs4 pretty_errors pathlib pandas selenium lxml xlrd openpyxl

%environment
  export IMAGE_NAME="webscraper"
  export PATH=/usr/local/bin:$PATH
  export LD_LIBRARY_PATH=/usr/local/lib:$LD_LIBRARY_PATH

%runscript

