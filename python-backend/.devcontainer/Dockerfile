FROM --platform=linux/amd64 python:3.8

RUN apt-get update  \
    && apt-get install -y --no-install-recommends libpq-dev python3.8-dev gcc git=1:2.39.5-0+deb12u1 \
    && apt-get clean

# # Set display port to avoid crash
ENV DISPLAY=:99

# # Upgrade pip and install AWS CLI using pip
RUN python3 -m pip install --upgrade pip

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