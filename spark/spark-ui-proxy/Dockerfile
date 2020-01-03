FROM ubuntu:bionic

ADD ./spark-ui-proxy.py /

RUN apt-get update && apt-get install python python-dev -y

ENV SERVER_PORT=8080
ENV BIND_ADDR="0.0.0.0"

EXPOSE 8080

ENTRYPOINT ["python", "/spark-ui-proxy.py"]
