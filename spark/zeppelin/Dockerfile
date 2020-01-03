# Copyright 2015 The Kubernetes Authors All rights reserved.
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#     http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

#FROM index.tenxcloud.com/jimmy/spark:1.5.2_v1
FROM bzhao-spark-cluster/spark:3.0.0-SNAPSHOT

#ENV ZEPPELIN_VER 0.7.1
ENV ZEPPELIN_VER 0.9.0-SNAPSHOT

ADD ./zeppelin0.9.0/target/zeppelin-${ZEPPELIN_VER}.tar.gz /opt/

RUN cd /opt \
    && ln -s zeppelin-${ZEPPELIN_VER} zeppelin \
    && echo Zeppelin ${ZEPPELIN_VER} installed in /opt

# Use bit apache mirror
#RUN mkdir -p /opt && \
#    cd /opt && \
#    curl http://mirror.bit.edu.cn/apache/zeppelin/zeppelin-${ZEPPELIN_VER}/zeppelin-${ZEPPELIN_VER}-bin-all.tgz | \
#        tar -zx && \
#    ln -s zeppelin-${ZEPPELIN_VER}-bin-all zeppelin && \
#    echo Zeppelin ${ZEPPELIN_VER} installed in /opt

ADD zeppelin-log4j.properties /opt/zeppelin/conf/log4j.properties
ADD zeppelin-env.sh /opt/zeppelin/conf/zeppelin-env.sh
ADD docker-zeppelin.sh /opt/zeppelin/bin/docker-zeppelin.sh
EXPOSE 8080
ENTRYPOINT ["/opt/zeppelin/bin/docker-zeppelin.sh"]
