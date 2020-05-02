FROM nvidia/opengl:1.0-glvnd-devel-ubuntu16.04

LABEL mantainer="gvgramazio@gmail.com" \
      version="0.1"

ENV LANG=C.UTF-8 LC_ALL=C.UTF-8
ENV PATH /opt/conda/bin:$PATH

RUN apt-get update && apt-get install -y \
  wget \
  libglib2.0-0  \
  libgl1-mesa-glx \
  xcb \
  "^libxcb.*" \
  libx11-xcb-dev \
  libglu1-mesa-dev \
  libxrender-dev \
  libxi6 \
  libdbus-1-3 \
  libfontconfig1 \
  xvfb \
  liblua5.1 \
  libqt5gui5 \
  qt5-default \
  && rm -rf /var/lib/apt/lists/*

RUN wget https://www.coppeliarobotics.com/files/V-REP_PRO_EDU_V3_6_2_Ubuntu16_04.tar.xz
# RUN wget https://www.coppeliarobotics.com/files/CoppeliaSim_Edu_V4_0_0_Ubuntu16_04.tar.xz
# RUN wget http://coppeliarobotics.com/files/V-REP_PRO_EDU_V3_4_0_Linux.tar.gz
# RUN tar xf CoppeliaSim_Edu_V4_0_0_Ubuntu16_04.tar.xz
RUN tar xf V-REP_PRO_EDU_V3_6_2_Ubuntu16_04.tar.xz
# RUN tar -xf V-REP_PRO_EDU_V3_4_0_Linux.tar.gz
RUN apt-get remove -y wget

RUN echo 'export QT_DEBUG_PLUGINS=1' >> ~/.bashrc
# RUN echo 'export PATH=/V-REP_PRO_EDU_V3_4_0_Linux/:$PATH' >> ~/.bashrc
# RUN echo 'export PATH=/CoppeliaSim_Edu_V4_0_0_Ubuntu16_04/:$PATH' >> ~/.bashrc
RUN echo 'export PATH=/V-REP_PRO_EDU_V3_6_2_Ubuntu16_04/:$PATH' >> ~/.bashrc

# miniconda3
# https://github.com/ContinuumIO/docker-images/blob/master/miniconda3/debian/Dockerfile
RUN apt-get update --fix-missing && \
    apt-get install -y wget bzip2 ca-certificates libglib2.0-0 libxext6 libsm6 libxrender1 git mercurial subversion && \
    apt-get clean

RUN wget --quiet https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh -O ~/miniconda.sh && \
    /bin/bash ~/miniconda.sh -b -p /opt/conda && \
    rm ~/miniconda.sh && \
    /opt/conda/bin/conda clean -tipsy && \
    ln -s /opt/conda/etc/profile.d/conda.sh /etc/profile.d/conda.sh && \
    echo ". /opt/conda/etc/profile.d/conda.sh" >> ~/.bashrc && \
    echo "conda activate base" >> ~/.bashrc && \
    find /opt/conda/ -follow -type f -name '*.a' -delete && \
    find /opt/conda/ -follow -type f -name '*.js.map' -delete && \
    /opt/conda/bin/conda install -y python=3.6.8 && \
    /opt/conda/bin/conda install -y matplotlib scipy numpy && \
    /opt/conda/bin/conda install -y -c conda-forge opencv && \
    /opt/conda/bin/conda install -y -c pytorch pytorch torchvision && \
    /opt/conda/bin/conda clean -afy

CMD [ "/bin/bash" ]
