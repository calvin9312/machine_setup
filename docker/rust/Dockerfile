# Use an official Ubuntu 24.04 base image
FROM ubuntu:24.04

# Set the maintainer label
#LABEL maintainer="your_email@example.com"

# Update package lists and install necessary packages
RUN apt-get update

#RUN apt-get install -y --no-install-recommends rustup rust-all vim
RUN apt-get install -y vim git python3-pip python3-venv wget unzip curl build-essential

RUN rm -rf /var/lib/apt/lists/*

RUN mkdir /share

RUN userdel -r ubuntu 2> /dev/null
#RUN groupdel -r ubuntu 2> /dev/null
RUN groupadd -g 1000 davidc
RUN useradd davidc -u 1000 -g 1000 -m -s /bin/bash
#RUN groupadd -g 1000 davidc && useradd davidc -u 1000 -g 1000 -m -s /bin/bash

# Copy the application code into the container
#COPY . .

# Expose a port (if needed)
#EXPOSE 8080

USER davidc

# Set the working directory
WORKDIR /home/davidc

RUN ln -sf /share /home/davidc/share

RUN curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | bash -s -- -y
RUN echo 'source /home/davidc/.cargo/env' >> /home/davidc/.bashrc

RUN wget https://download.pytorch.org/libtorch/cpu/libtorch-cxx11-abi-shared-with-deps-2.7.0%2Bcpu.zip
RUN unzip libtorch-cxx11-abi-shared-with-deps-2.7.0+cpu.zip
RUN echo "export LIBTORCH=/home/davidc/libtorch" >> /home/davidc/.bashrc

RUN python3 -m venv /home/davidc/torch/venv
RUN echo "source /home/davidc/torch/venv/bin/activate" >> /home/davidc/.bashrc



# Define the command to run the application
CMD ["/bin/bash"]


