#
# Copyright 2017 George Aristy
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
#

FROM eclipse-temurin:21.0.9_10-jre

RUN mkdir -p -m 750 /opt/youtrack/data /opt/youtrack/backups /opt/youtrack/logs /opt/youtrack/conf

RUN sudo chown -R 13001:13001 /opt/youtrack/data /opt/youtrack/backups /opt/youtrack/logs /opt/youtrack/conf

COPY youtrack/data /opt/youtrack/data

WORKDIR /opt/youtrack

RUN apt-get update && apt-get install -y supervisor && rm -rf /var/lib/apt/lists/*

RUN wget https://download.jetbrains.com/charisma/youtrack-${youtrackVersion}.jar -O /opt/youtrack/bin/youtrack.jar

ADD supervisor/youtrack.conf /etc/supervisor/conf.d/youtrack.conf

EXPOSE 80/tcp 

CMD ["/usr/bin/supervisord","-n","-c","/etc/supervisor/supervisord.conf"]
