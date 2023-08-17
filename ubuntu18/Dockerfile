FROM ubuntu:18.04

ARG DEBIAN_FRONTEND=noninteractive

ENV TZ Asia/Seoul
ENV PYTHONIOENCODING UTF-8
ENV LC_CTYPE C.UTF-8

WORKDIR /root

RUN apt update
RUN apt install netcat vim git gcc ssh curl wget gdb sudo zsh python3 python3-pip libffi-dev build-essential libssl-dev libc6-i386 libc6-dbg gcc-multilib make -y

RUN dpkg --add-architecture i386
RUN apt update
RUN apt install libc6:i386 -y

RUN python3 -m pip install --upgrade pip
RUN pip3 install unicorn
RUN pip3 install keystone-engine
RUN pip3 install pwntools
RUN pip3 install ropgadget
RUN apt install libcapstone-dev -y
RUN apt install ruby-full -y
RUN gem install one_gadget seccomp-tools

RUN git clone https://github.com/pwndbg/pwndbg && \
    cd pwndbg && \
    git checkout tags/2022.08.30
RUN cd pwndbg && ./setup.sh
RUN echo 'source /pwndbg/gdbinit.py' >> /root/.gdbinit


RUN wget https://github.com/robbyrussell/oh-my-zsh/raw/master/tools/install.sh -O - | zsh || true

RUN sed -i 's/ZSH_THEME="[^"]*"/ZSH_THEME="cloud"/' ~/.zshrc

RUN git clone https://github.com/zsh-users/zsh-autosuggestions ~/.zsh/zsh-autosuggestions
RUN echo "source ~/.zsh/zsh-autosuggestions/zsh-autosuggestions.zsh" >> ~/.zshrc

CMD ["/bin/zsh"]