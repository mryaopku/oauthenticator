# Designed to be run as 
# 
# docker run -it -p 8000:8000 jupyterhub/oauthenticator

FROM jupyterhub/jupyterhub

MAINTAINER Project Jupyter <ipython-dev@scipy.org>

RUN mv /etc/apt/sources.list /etc/apt/sources.list.backup && \
    echo "deb http://mirrors.cloud.aliyuncs.com/ubuntu/ bionic main restricted universe multiverse" >> /etc/apt/sources.list && \
    echo "deb-src http://mirrors.cloud.aliyuncs.com/ubuntu/ bionic main restricted universe multiverse" >> /etc/apt/sources.list && \
    echo "deb http://mirrors.cloud.aliyuncs.com/ubuntu/ bionic-updates main restricted universe multiverse" >> /etc/apt/sources.list && \
    echo "deb-src http://mirrors.cloud.aliyuncs.com/ubuntu/ bionic-updates main restricted universe multiverse" >> /etc/apt/sources.list && \
    echo "deb http://mirrors.cloud.aliyuncs.com/ubuntu/ bionic-backports main restricted universe multiverse" >> /etc/apt/sources.list && \
    echo "deb-src http://mirrors.cloud.aliyuncs.com/ubuntu/ bionic-backports main restricted universe multiverse" >> /etc/apt/sources.list && \
    echo "deb http://mirrors.cloud.aliyuncs.com/ubuntu/ bionic-security main restricted universe multiverse" >> /etc/apt/sources.list && \
    echo "deb-src http://mirrors.cloud.aliyuncs.com/ubuntu/ bionic-security main restricted universe multiverse" >> /etc/apt/sources.list && \
    echo "deb http://mirrors.cloud.aliyuncs.com/ubuntu/ bionic-proposed main restricted universe multiverse" >> /etc/apt/sources.list && \
    echo "deb-src http://mirrors.cloud.aliyuncs.com/ubuntu/ bionic-proposed main restricted universe multiverse" >> /etc/apt/sources.list && \
    apt-get update && \
    apt-get upgrade -y && \
    apt-get install -y libasound2 && \
    apt-get install -y libfontconfig1 && \
    apt-get install -y libgl1

# Install oauthenticator from git
RUN conda update -c conda-forge -y --all && \
    conda update -c conda-forge -y --all && \
    conda update -c conda-forge -y --all && \
    python3 -m pip install oauthenticator && \
    conda install -c conda-forge -y jupyterlab && \
    conda clean -ay

# Create oauthenticator directory and put necessary files in it
RUN mkdir /srv/oauthenticator
WORKDIR /srv/oauthenticator
ENV OAUTHENTICATOR_DIR /srv/oauthenticator
ADD jupyterhub_config.py jupyterhub_config.py
ADD addusers.sh /srv/oauthenticator/addusers.sh
ADD userlist /srv/oauthenticator/userlist
ADD ssl /srv/oauthenticator/ssl
RUN chmod 700 /srv/oauthenticator

RUN ["sh", "/srv/oauthenticator/addusers.sh"]
