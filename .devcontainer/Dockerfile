FROM ubuntu:18.04

ENV HOME_DIR /root

# Environment Setting
RUN apt update
RUN apt install -y python3 python3-pip build-essential libssl-dev libffi-dev python-dev git

# for jupyter notebook
RUN apt install -y libsqlite3-dev libreadline6-dev libbz2-dev libssl-dev libsqlite3-dev libncursesw5-dev libffi-dev libdb-dev libexpat1-dev zlib1g-dev liblzma-dev libgdbm-dev libmpdec-dev

# Install any missing dependencies for enhanced language service
RUN apt-get install -y libicu[0-9][0-9]

# install pyenv
RUN git clone git://github.com/pyenv/pyenv.git $HOME_DIR/.pyenv
RUN apt install -y zlib1g-dev wget
# When installing python, it occur
# zipimport.ZipImportError: can't decompress data; zlib not available
# pyenv uses wget when getting python
# if not wget, not download and did not raise error

ENV PYENV_ROOT="${HOME_DIR}/.pyenv"
ENV PATH="${PATH}:${PYENV_ROOT}/bin"

RUN eval "$(pyenv init -)"

RUN pyenv install 3.7.2
# RUN pyenv install 3.6.8

# install pipenv
RUN pip3 install pipenv
ENV LC_ALL=C.UTF-8 LANG=C.UTF-8

RUN mkdir /workspaces
WORKDIR /workspaces

# Clean up
RUN apt-get autoremove -y \
    && apt-get clean -y \
    && rm -rf /var/lib/apt/lists/*

# Set the default shell to bash rather than sh
ENV SHELL /bin/bash
