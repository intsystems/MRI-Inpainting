FROM nvidia/cuda:11.6.2-base-ubuntu20.04

WORKDIR /tmp

RUN apt-get update -qq && \
	apt-get install --yes --no-install-recommends \
	zip unzip pigz jq moreutils time wget inotify-tools vim parallel curl libxmu6

# Install environment
RUN wget --progress=bar:force:noscroll https://repo.anaconda.com/miniconda/Miniconda3-py38_4.11.0-Linux-x86_64.sh && \
    mkdir /root/.conda && \
    bash Miniconda3-py38_4.11.0-Linux-x86_64.sh -b && \
    rm -f Miniconda3-py38_4.11.0-Linux-x86_64.sh
ENV PATH=/root/miniconda3/bin:${PATH}
RUN conda --version

RUN conda install -y -q -f -c conda-forge dcm2niix=1.0.20190902 && \
	sync

RUN pip install torch==1.12.1+cu113 torchvision==0.13.1+cu113 torchaudio==0.12.1 --extra-index-url https://download.pytorch.org/whl/cu113

COPY ./requirements.txt /code/requirements.txt
#RUN conda install -y --file /code/requirements.txt
RUN pip install --upgrade pip && \
	pip install -r /code/requirements.txt && \
	sync
