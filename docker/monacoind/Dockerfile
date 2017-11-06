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
RUN cd /usr/local/src;git clone https://github.com/monacoinproject/monacoin;cd monacoin;./autogen.sh;./configure --disable-wallet;make;make install;
