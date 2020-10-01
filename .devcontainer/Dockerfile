FROM oracle/graalvm-ce:20.2.0-java11

RUN ln -s "${JAVA_HOME}" /docker-java-home
RUN export PATH=${JAVA_HOME}/bin:${PATH}
RUN yum -y install rh-maven35
RUN source /opt/rh/rh-maven35/enable
