# Dockerfile to setup neo-python on the master branch.
# https://github.com/CityOfZion/neo-python/tree/master/docker
#
# Building (these commands create a Docker image called neopython):
#
#    $ docker build -f Dockerfile -t neopython .
#
# Build without caching:
#
#    $ docker build --no-cache -f Dockerfile -t neopython .
#
# At this point there is a Docker image called 'neopython'. If you want to run it connecting
# to a private network, make sure the privatenet container is already running.
# https://hub.docker.com/r/cityofzion/neo-privatenet
#
# Start a container interactively, opening a bash in `/neo-python`, and mounting the current directory as `/neo-python/sc`:
#
#    $ docker run --rm -it -v $(pwd):/neo-python/sc --net=host -h neopython --name neopython neopython /bin/bash
#
# Once you are inside the container, you can start neo-python with `python3 prompt.py -p` (using -p to connect to a private net).
# To update neo-python, just run `git pull` and `pip install -e .`
FROM ubuntu:17.10

# Install dependencies
RUN apt-get update && apt-get install -y \
    wget \
    git-core \
    python3.6 \
    python3.6-dev \
    python3.6-venv \
    python3-pip \
    libleveldb-dev \
    libssl-dev \
    vim \
    man

# APT cleanup to reduce image size
RUN rm -rf /var/lib/apt/lists/*

# Clone and setup
RUN git clone https://github.com/CityOfZion/neo-python.git
WORKDIR neo-python

# Install the dependencies
RUN pip3 install -e .

# Download the privnet wallet, to have it handy for easy experimenting
RUN wget https://s3.amazonaws.com/neo-experiments/neo-privnet.wallet

# Example run command
CMD python3 prompt.py
