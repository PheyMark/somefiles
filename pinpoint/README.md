docker方式安装pinpoint

```
git clone https://github.com/naver/pinpoint-docker.git
cd pinpoint-docker
docker-compose pull && docker-compose up -d
```

Pinpoint-Flink ：http://hostname:8081/#/overview

Pinpoint-web ：http://hostname:8079/#/main

在Debian上安装php的agent，用的php官方镜像，不一定能成功，只成功了一次，再试一遍神奇的失败了

```

apt-get install automake bison flex g++ git libtool make pkg-config openssl libssl-dev wget apt-utils procps net-tools -y

wget https://jaist.dl.sourceforge.net/project/boost/boost/1.63.0/boost_1_63_0.tar.gz
tar xf boost_1_63_0.tar.gz && cd boost_1_63_0
./bootstrap.sh
./b2 install --prefix=/usr/local/boost

wget http://apache.fayea.com/thrift/0.11.0/thrift-0.11.0.tar.gz
tar xf thrift-0.11.0.tar.gz
cd  thrift-0.11.0
./configure CXXFLAGS="-DFORCE_BOOST_SMART_PTR" --with-cpp --with-php=no --with-python=no --with-ruby=no --with-nodejs=no --with-qt4=no --with-java=no --with-boost=/usr/local/boost --prefix=/usr/local/thrift
make
make install

export WITH_BOOST_PATH='/usr/local/boost'
export WITH_THRIFT_PATH='/usr/local/thrift'

git clone https://github.com/ofauchon/pinpoint-c-agent.git 
cd pinpoint-c-agent/pinpoint_php
./Build.sh
make install
```

所以这有编译好的文件，其中pinpoint.so是php的扩展，放到php的扩展的目录下，libs.tar.bz2是几个boost的lib，放到/lib下面。不过好像缺了thrift的so文件。那就执行一下上面的编译过程吧，thrift的编译是没问题的。

```
/usr/local/lib/php/extensions/no-debug-non-zts-20170718/pinpoint.so
/lib/libboost_system.so.1.63.0
/lib/libboost_thread.so.1.63.0
/lib/libboost_filesystem.so.1.63.0
/lib/libboost_date_time.so.1.63.0
```



