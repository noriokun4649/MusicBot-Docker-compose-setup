FROM python:3.7.9-alpine3.12

# Add project source
WORKDIR /var/docker/musicbot
COPY requirements.txt ./

RUN apk update && \
    apk upgrade && \
    apk --no-cache --virtual add make g++ gcc unzip && \
    apk --no-cache add git ffmpeg opus-dev libffi-dev libsodium-dev && \
    python3 -m pip install -U pip && \
    python3 -m pip install -U -r requirements.txt && \
    git clone https://github.com/Just-Some-Bots/MusicBot.git musicbot_clone && \
    apk del

WORKDIR /var/docker/musicbot/musicbot_clone

# Create volume for mapping the config
VOLUME /var/docker/musicbot/musicbot_clone/config
VOLUME /var/docker/musicbot/musicbot_clone/audio_cache

COPY requirements.txt ./

ENV APP_ENV=docker

ENTRYPOINT ["python3", "dockerentry.py"]
