FROM openjdk:11-jre

ENV no_proxy 127.0.0.1,localhost

# Expose logic server port to server manager
EXPOSE 9000

# Set environment (Default fallback)
ENV HOST_IP '172.17.0.1'

# Set workdir
WORKDIR /tmp

# Set execute user
RUN useradd cloudfn
USER cloudfn

# Start logic server
CMD java -jar /opt/emitter/cloudfn-java-server.jar
