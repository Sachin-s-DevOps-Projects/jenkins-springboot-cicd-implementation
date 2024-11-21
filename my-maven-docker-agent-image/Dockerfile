# Base image with Maven and JDK 11
FROM maven:3.8.5-jdk-11

# Install Docker CLI
RUN apt-get update && apt-get install -y docker.io \
    && apt-get clean && rm -rf /var/lib/apt/lists/*

# Set Maven and Java environment variables
ENV JAVA_HOME=/usr/lib/jvm/java-11-openjdk-amd64
ENV MAVEN_HOME=/usr/share/maven
ENV PATH=$JAVA_HOME/bin:$MAVEN_HOME/bin:$PATH

# Set the working directory
WORKDIR /workspace

# Add non-root Jenkins user
RUN useradd -m -d /home/jenkins -s /bin/bash jenkins \
    && echo "jenkins ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers \
    && (getent group docker || groupadd -g 999 docker) \
    && usermod -aG docker jenkins

# Switch to the Jenkins user
USER jenkins

# Default command to run when the container starts
CMD ["bash"]
