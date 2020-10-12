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

# Choose the user to run as and set the User home
USER vscode
ENV HOME /home/vscode

# This sets the DISPLAY so that you can launch X Window apps from within the docker
# container. They will be hosted by your X Windows Server directly on your laptop
ENV DISPLAY host.docker.internal:0

# Set the workdir - will be the vscode users home dir
WORKDIR /home/vscode
RUN mkdir /home/vscode/code

# Install ZSH, you can run bash as well if you like but *DON"T* install and use the FISH shell
RUN wget https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh
RUN chmod u+x install.sh && ./install.sh
RUN echo "export PATH=${JAVA_HOME}/bin:${PATH}" >> /home/vscode/.zshrc
RUN echo "source /opt/rh/rh-maven35/enable"  >> /home/vscode/.zshrc

# Install prelude conf for emacs
RUN curl -L https://git.io/epre | sh

# Add GraalVM EE 20.2.0
#ADD /Users/kfoster/bin/graal/installs/graalvm-ee-java11-darwin-amd64-20.2.0.tar.gz /home/vscode
#ADD ~/bin/graal/installs/graalvm-ee-java8-darwin-amd64-20.2.0.tar.gz /home/vscode
#ADD ~/bin/graal/installs/idealgraphvisualizer-20.2.0-all /home/vscode
#ADD ~/bin/graal/installs/llvm-toolchain-installable-java11-darwin-amd64-20.2.0.jar /home/vscode
#ADD ~/bin/graal/installs/llvm-toolchain-installable-java8-darwin-amd64-20.2.0.jar /home/vscode
#ADD ~/bin/graal/installs/native-image-installable-svm-svmee-java11-darwin-amd64-20.2.0.jar /home/vscode
#ADD ~/bin/graal/installs/native-image-installable-svm-svmee-java8-darwin-amd64-20.2.0.jar /home/vscode

# Install jEnv - let's you switch betwen installed JDKs
#RUN git clone https://github.com/jenv/jenv.git ~/.jenv
#RUN echo 'export PATH="$HOME/.jenv/bin:$PATH"' >> ~/.zshrc
#RUN echo 'eval "$(jenv init -)"' >> ~/.zshrc
# Configure some JDKs
#RUN source ~/.zshrc; jenv add /opt/graalvm-ce-java11-20.2.0/

#
# Set the environment
#
# This is a hack as jenv doesn't know how to set this - need a fix.
ENV GRAALVM_HOME /opt/graalvm-ce-java11-20.2.0/
# If you type `code a-file.txt` from the container shell in vscode, the file will be
# opened inside vscode now - as will anything that requires an editor
ENV EDITOR 'code -w'

# Expose some ports that we are likely to end up using - you can add more
EXPOSE 8080/tcp
EXPOSE 3000/tcp
EXPOSE 80/tcp
