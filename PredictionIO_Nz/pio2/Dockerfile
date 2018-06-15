FROM alpine:latest

RUN \
  apk update && \
  apk upgrade && \
  apk add openjdk8 && \
  apk add bash && \
  apk add curl && \
  apk add --no-cache python3 && \
    python3 -m ensurepip && \
    rm -r /usr/lib/python*/ensurepip && \
    pip3 install --upgrade pip setuptools && \
    if [ ! -e /usr/bin/pip ]; then ln -s pip3 /usr/bin/pip ; fi && \
    if [[ ! -e /usr/bin/python ]]; then ln -sf /usr/bin/python3 /usr/bin/python; fi && \
  rm -rf /var/cache/apk/*

ENV JAVA_HOME /usr/lib/jvm/java-1.8-openjdk

WORKDIR /tmp


ENV PIO_HOME=/PredictionIO
ENV PATH=$PATH:$PIO_HOME/bin:$JAVA_HOME/bin


COPY ./PredictionIO /PredictionIO
COPY ./MySimilarProduct /MySimilarProduct


# create a non root new user and switch to it

RUN adduser -D -u 1000 pio

# make the folder writable

RUN chmod -R 777 /PredictionIO

USER pio

# set java_home and pio_home for new user
RUN export JAVA_HOME=/usr/lib/jvm/java-1.8-openjdk
RUN export PIO_HOME=/PredictionIO
RUN export PATH=$PATH:$PIO_HOME/bin:$JAVA_HOME/bin

CMD ["bash"]