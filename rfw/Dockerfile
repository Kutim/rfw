 FROM python:2.7

 ENV PYTHONUNBUFFERED 1

 RUN \
  set -x && \
  sed -i 's/deb.debian.org/mirrors.ustc.edu.cn/g' /etc/apt/sources.list && \
  apt-get update  && \
  apt-get install -y iptables && \
  rm /var/lib/apt/lists/* -vfR

 RUN mkdir /code
 WORKDIR /code
 ADD requirements.txt /code/
 # RUN pip install -r requirements.txt
 ADD . /code/

 RUN \
  ./setup.py install && \
  cd config/deploy && \
  ./rfwgen 0.0.0.0 && \
  mv server_0.0.0.0/*  /etc/rfw/ssl/