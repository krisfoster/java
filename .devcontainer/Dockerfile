FROM oracle/graalvm-ce:20.2.0-java11

# VSCode will expect that java will be installed here, so let's link to it
RUN ln -s $JAVA_HOME /docker-java-home

# Install some important packages, including maven3
RUN yum -y install sudo curl wget telnet iputils emacs ncat xargs xeyes zsh git rh-maven35

# Create a user and add them to the sudoers
RUN useradd -u 1000 vscode
RUN echo 'vscode ALL=(ALL:ALL) NOPASSWD: ALL' | sudo EDITOR='tee -a' visudo
RUN echo "export PATH=${JAVA_HOME}/bin:${PATH}" >> /home/vscode/.bashrc
RUN echo "source /opt/rh/rh-maven35/enable"  >> /home/vscode/.bashrc

# Install ZSH, you can run bash as well if you like
RUN su - vscode -c 'wget https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh'
RUN su - vscode -c 'chmod u+x install.sh && ./install.sh'

# Choose the user to run at and set the User home
USER vscode
ENV HOME /home/vscode
# This sets the DISPLAY so that you can launch X Window apps from within the docker
# container. They will be hosted by your X Windows Server directly on your laptop
ENV DISPLAY host.docker.internal:0

EXPOSE 8080/tcp
EXPOSE 3000/tcp
