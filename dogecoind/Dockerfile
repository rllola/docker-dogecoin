FROM arm32v7/ubuntu

RUN apt-get update

RUN apt-get -y install git build-essential libtool autotools-dev autoconf pkg-config libssl-dev libboost-all-dev libdb5.3-dev libdb5.3++-dev libevent-dev libminiupnpc-dev protobuf-compiler

WORKDIR /usr/src

# Clone the repo
RUN git clone https://github.com/dogecoin/dogecoin.git

WORKDIR /usr/src/dogecoin

# Pick the correct branch/version
RUN git checkout 1.14-branding

# Autogen
RUN ./autogen.sh

# Configure
RUN ./configure --with-incompatible-bdb --disable-tests --disable-gui-tests --disable-bench

# Make
RUN make

# Build
RUN build

RUN chmod +x src/dogecoind src/dogecoin-cli
RUN ln -s /usr/src/dogecoin/src/dogecoind /usr/bin/dogecoind
RUN ln -s /usr/src/dogecoin/src/dogecoin-cli /usr/bin/dogecoin-cli

ADD dogecoin.conf /root/.dogecoin/dogecoin.conf

#RUN mkdir /root/data
#RUN wget https://bootstrap.chain.so/bootstrap.dat -O /root/data/bootstrap.dat

EXPOSE 22555 22556 44555 44556

CMD ["dogecoind", "-printtoconsole"]
