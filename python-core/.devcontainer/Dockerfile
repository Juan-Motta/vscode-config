FROM --platform=linux/amd64 python:3.8.19-bookworm

# Install basic dependencies and add SSH key for private repo access, clean up after installation
RUN apt-get update && apt-get install -y --no-install-recommends \
    curl \
    expat \
    gcc \
    git \
    libasound2 \
    libatk1.0-0 \
    libcairo2 \
    libcups2 \
    libcurl3-gnutls \
    libcurl4 \
    libdrm2 \
    libfontconfig1 \
    libgconf-2-4 \
    libgbm1 \
    libglib2.0-0 \
    libglib2.0-bin \
    libglib2.0-data \
    libglib2.0-dev \
    libgtk-3-0 \
    libnss3 \
    libnss3 \
    libpq-dev \
    libssl-dev \
    libx11-6 \
    libxcomposite1 \
    libxdamage1 \
    libxfixes3 \
    libxkbcommon0 \
    libxrandr2 \
    libxshmfence1 \
    nghttp2 \
    openssh-client \
    openssh-server \
    python3-dev \
    qpdf \
    unrar-free \
    unzip \
    wget && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

# # Install Chrome
RUN curl -Lo /chrome-linux64.zip https://storage.googleapis.com/chrome-for-testing-public/127.0.6533.72/linux64/chrome-linux64.zip && \
    unzip /chrome-linux64.zip -d /chrome-install/ && \
    ln -s /chrome-install/chrome-linux64/chrome /usr/bin/google-chrome && \
    rm -rf /chrome-linux64.zip /chrome-install

# # Set display port to avoid crash
ENV DISPLAY=:99

# # Upgrade pip and install AWS CLI using pip
RUN python3 -m pip install --upgrade pip awscli

RUN git clone https://github.com/powerline/fonts.git && \
    cd fonts && \
    ./install.sh && \
    cd .. && rm -rf fonts


RUN apt update && \ 
    apt install zsh -y && \
    chsh -s $(which zsh) && \
    wget https://github.com/robbyrussell/oh-my-zsh/raw/master/tools/install.sh -O - | zsh || true && \
    zsh -c 'git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions' && \
    zsh -c 'git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting' && \
    sed -i 's/plugins=(git)/plugins=(git zsh-autosuggestions zsh-syntax-highlighting)/' ~/.zshrc
