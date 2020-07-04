Bootstrap:docker
From:ubuntu:16.04

%environment
	QT_DEBUG_PLUGINS=1	
	PATH=/opt/conda/bin:/opt/conda/condabin:$PATH
	LD_LIBRARY_PATH=/opt/conda/lib/:$LD_LIBRARY_PATH
	export QT_DEBUG_PLUGINS PATH LID_LIBRARY_PATH

%post
	apt-get update && apt-get install -y \
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
	libavcodec-dev \
	libavformat-dev \
	libswscale-dev \
	libxkbcommon-x11-0 \
	mesa-utils \
	x11-apps \
	tmux \
	&& rm -rf /var/lib/apt/lists/*

	wget --quiet https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh -O ~/miniconda.sh && \
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
	    /opt/conda/bin/conda install -y -c conda-forge opencv ipdb && \
	    /opt/conda/bin/conda install -y -c pytorch pytorch torchvision && \
	    /opt/conda/bin/conda clean -afy

%runscript
	source ~/.bashrc
	/bin/bash
