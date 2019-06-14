ARG BUILD_FROM
FROM $BUILD_FROM

# Copy data
COPY run.sh /
COPY mosquitto.conf /etc/
COPY customtts.sh /usr/bin
COPY snips-entrypoint.sh /


RUN apt update \
    && apt install -y dirmngr apt-utils apt-transport-https jq unzip supervisor mpg123 curl tzdata 

RUN rm -rf /var/lib/apt/lists/* \
    && bash -c 'echo "deb https://raspbian.snips.ai/stretch stable main" > /etc/apt/sources.list.d/snips.list' \
            && apt-key adv --keyserver keyserver.ubuntu.com --recv-keys D4F50CDCA10A2849;

RUN apt-get update \
    && apt-get install -y snips-platform-voice snips-asr snips-injection snips-watch \
    && rm -rf /var/lib/apt/lists/* 

ENTRYPOINT [ "/run.sh" ]
