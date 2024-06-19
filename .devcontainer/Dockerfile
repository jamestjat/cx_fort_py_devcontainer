# Use Ubuntu 22.04 LTS as the base image
FROM ubuntu:22.04 AS base

# Label the image
LABEL maintainer="James Joseph <james.joseph@aspentech.com>"
LABEL version="1.0"
LABEL description="This is a devcontainer image for C/CXX/Fortran/python3 development"

# Set non-interactive frontend (avoid tzdata prompt)
ARG DEBIAN_FRONTEND=noninteractive

# Update and install dependencies
RUN apt-get update && \
    apt-get install -y \
    software-properties-common \
    wget \
    sudo \
    gcc \
    gdb \
    make \
    cmake \
    ninja-build \
    git \
    f2c \
    tree \
    htop \
    libz-dev \
    python3.11 \
    python3-pip \
    python3-venv \
    zsh \
    fonts-powerline

# Set root password
RUN echo "root:your_root_password_here" | chpasswd

# Install clang LLVM 17
RUN wget -O - https://apt.llvm.org/llvm-snapshot.gpg.key | apt-key add - && \
    apt-add-repository "deb http://apt.llvm.org/jammy/ llvm-toolchain-jammy-17 main" && \
    apt-get update && \
    apt-get install -y clang-17 && \
    ln -s /usr/bin/clang-17 /usr/bin/clang

# Set C and C++ compilers to clang
ENV CC=clang
ENV CXX=clang

# Install Intel Fortran compiler from oneAPI repository
RUN wget -O- https://apt.repos.intel.com/intel-gpg-keys/GPG-PUB-KEY-INTEL-SW-PRODUCTS.PUB \
    | gpg --dearmor | tee /usr/share/keyrings/oneapi-archive-keyring.gpg > /dev/null && \
    echo "deb [signed-by=/usr/share/keyrings/oneapi-archive-keyring.gpg] https://apt.repos.intel.com/oneapi all main" \
    | tee /etc/apt/sources.list.d/oneAPI.list && \
    apt-get update && \
    apt-get install -y intel-oneapi-compiler-fortran-2023.1.0 && \
    echo "source /opt/intel/oneapi/setvars.sh --force" >> /root/.zshrc

# Fortls installation & Autocomplete Suggestions for Fortran
RUN pip3 install fortls findent fprettify

# Create user vscode, add to sudo group, set default shell to zsh, and set password
RUN useradd -m -G sudo vscode && \
    echo "vscode ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers.d/vscode && \
    echo "vscode:vscode" | chpasswd

# Install Oh My Zsh
RUN wget https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh -O /home/vscode/install.sh && \
    chown vscode:vscode /home/vscode/install.sh && \
    su - vscode -c "sh /home/vscode/install.sh --unattended" && \
    rm /home/vscode/install.sh

# Install Powerline fonts
RUN su - vscode -c "git clone https://github.com/powerline/fonts.git --depth=1" && \
    su - vscode -c "cd fonts && ./install.sh && cd .. && rm -rf fonts"

# Set Zsh theme to arrow and add Intel Fortran setup to .zshrc
RUN su - vscode -c "sed -i 's/ZSH_THEME=\".*\"/ZSH_THEME=\"arrow\"/' ~/.zshrc" && \
    su - vscode -c "echo 'source /opt/intel/oneapi/setvars.sh --force' >> ~/.zshrc"

# Ensure vscode user owns home and workspace directories
RUN chown -R vscode:vscode /home/vscode

# Set the default shell to zsh for vscode user
RUN chsh -s /usr/bin/zsh vscode

# Switch to vscode user
USER vscode

# Set working directory
WORKDIR /home/vscode

# Clean up
RUN sudo apt-get clean && \
    sudo rm -rf /var/lib/apt/lists/*
