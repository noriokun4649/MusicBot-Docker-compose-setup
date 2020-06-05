FROM ubuntu:18.04

# Add project source
WORKDIR /var/docker/musicbot
COPY requirements.txt ./



# Install build tools
RUN apt-get update -y
RUN apt-get install build-essential unzip -y
RUN apt-get install software-properties-common -y

# Install system dependencies
RUN apt-get install git ffmpeg libopus-dev libffi-dev libsodium-dev python3-pip -y
RUN apt-get upgrade -y

# Install Python dependencies
RUN python3 -m pip install -U pip
RUN python3 -m pip install -U -r requirements.txt

RUN git clone https://github.com/Just-Some-Bots/MusicBot.git musicbot_clone

WORKDIR /var/docker/musicbot/musicbot_clone

# Create volume for mapping the config
VOLUME /var/docker/musicbot/musicbot_clone/config
VOLUME /var/docker/musicbot/musicbot_clone/audio_cache

ENV APP_ENV=docker

ENTRYPOINT ["python3", "dockerentry.py"]