FROM quay.io/centos/centos:stream8

RUN yum update -y
RUN yum install -y ruby-devel gcc make rpm-build rubygems
RUN gem install --no-ri --no-rdoc fpm

RUN yum install -y ncurses-devel openssl-devel bzip2-devel libffi-devel sqlite-devel gdbm-devel \
    readline-devel tk-devel xz-devel

ENV BUILD_VER=3.11.7
ENV DLURL=http://python.org/ftp/python/${BUILD_VER}/Python-${BUILD_VER}.tgz
RUN mkdir -p /build; cd /build\
    && curl -L ${DLURL} | tar xz
RUN cd /build/Python-${BUILD_VER}\
    && ./configure --prefix=/usr/local\
    && make -j2 && make install DESTDIR=/tmp/installdir

RUN echo 'echo /usr/local/lib > /etc/ld.so.conf.d/usr-local-lib.conf' > /tmp/installdir/run-ldconfig.sh
RUN echo '/sbin/ldconfig' >> /tmp/installdir/run-ldconfig.sh
RUN fpm -s dir -t rpm -n python -v ${BUILD_VER} -C /tmp/installdir \
    --after-install /tmp/installdir/run-ldconfig.sh \
    -d 'openssl' \
    -d 'bzip2' \
    -d 'sqlite' \
    -d 'ncurses' \
    -d 'libffi' \
    -d 'tk' \
    --directories=/usr/local/lib/python3.11/ \
    usr/local
