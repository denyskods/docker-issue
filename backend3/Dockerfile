FROM ubuntu:latest
  
RUN apt-get update && apt-get install -y \
     python3 \
     python3-pip

COPY . /backend

WORKDIR /backend

RUN pip3 install --upgrade pip -r requirements.txt
