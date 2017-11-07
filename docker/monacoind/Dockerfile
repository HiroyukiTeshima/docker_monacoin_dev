FROM centos:7

# system update
RUN yum -y update && yum clean all

# set locale
RUN yum reinstall -y glibc-common && yum clean all
RUN localedef -f UTF-8 -i ja_JP ja_JP.UTF-8
ENV LANG ja_JP.UTF-8
ENV LANGUAGE ja_JP:ja
ENV LC_ALL ja_JP.UTF-8
RUN unlink /etc/localtime
RUN ln -s /usr/share/zoneinfo/Japan /etc/localtime

# monacoind install
RUN yum install -y autogen automake libtool gcc gcc-c++ boost boost-devel openssl-devel libevent-devel libdb-cxx-devel libdb-cxx wget git make which
RUN cd /usr/local/src;wget 'http://download.oracle.com/berkeley-db/db-4.8.30.NC.tar.gz';tar -xzvf db-4.8.30.NC.tar.gz;cd db-4.8.30.NC/build_unix/;../dist/configure --enable-cxx --disable-shared --with-pic --prefix=$BDB_PREFIX;make install
RUN cd /usr/local/src;git clone https://github.com/monacoinproject/monacoin;cd monacoin;./autogen.sh;./configure LDFLAGS="-L${BDB_PREFIX}/lib/" CPPFLAGS="-I${BDB_PREFIX}/include/";make;make install;

# testnet
#RUN mkdir /var/monacoin/;cd /var/monacoin/;mkdir test1 test2;
#COPY test1.conf /var/monacoin/test1/monacoin.conf
#COPY test2.conf /var/monacoin/test2/monacoin.conf
# testnet 起動
#RUN cd /var/monacoin/;monacoind -datadir=test1 -daemon;monacoind -datadir=test2 -daemon