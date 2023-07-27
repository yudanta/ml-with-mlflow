FROM python:3.9.17-slim-bullseye

RUN apt update
RUN apt install build-essential -y --no-install-recommends
RUN apt install -y git curl make libssl-dev zlib1g-dev \
    libbz2-dev libreadline-dev libsqlite3-dev wget curl llvm \
    libncursesw5-dev xz-utils tk-dev libxml2-dev libxmlsec1-dev libffi-dev liblzma-dev

# setup pyenv 
RUN git clone https://github.com/pyenv/pyenv.git /pyenv
ENV PYENV_ROOT /pyenv
ENV PATH $PYENV_ROOT/shims:$PYENV_ROOT/bin:$PATH
RUN eval "$(/pyenv/bin/pyenv init -)"

COPY requirements.txt requirements.txt
RUN pip install -r requirements.txt 

COPY entrypoint.sh /

RUN chmod +x /entrypoint.sh

EXPOSE ${SERVER_PORT}

ENTRYPOINT [ "/entrypoint.sh" ]