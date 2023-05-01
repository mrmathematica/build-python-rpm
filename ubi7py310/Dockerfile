FROM centos:7

RUN yum -y install epel-release
RUN yum update -y
RUN yum install -y ruby-devel gcc make rpm-build rubygems
RUN gem install --no-ri --no-rdoc backports -v 3.21.0 && gem install --no-ri --no-rdoc fpm
RUN yum install -y ncurses-devel sqlite-devel bzip2-devel libnsl2-devel\
    gdbm-devel xz-devel libuuid-devel zlib-devel tk-devel libffi-devel\
    openssl11-devel tcl-devel readline-devel

ENV BUILD_VER=3.10.11
ENV DLURL=http://python.org/ftp/python/${BUILD_VER}/Python-${BUILD_VER}.tgz
RUN mkdir -p /build; cd /build\
    && curl -L ${DLURL} | tar xz
RUN cd /build/Python-${BUILD_VER}\
    && sed -i 's/PKG_CONFIG openssl /PKG_CONFIG openssl11 /g' configure\
    && ./configure --prefix=/usr/local\
    && make -j2 && make install DESTDIR=/tmp/installdir

RUN echo 'echo /usr/local/lib > /etc/ld.so.conf.d/usr-local-lib.conf' > /tmp/installdir/run-ldconfig.sh
RUN echo '/sbin/ldconfig' >> /tmp/installdir/run-ldconfig.sh
RUN fpm -s dir -t rpm -n python -v ${BUILD_VER} -C /tmp/installdir \
    --after-install /tmp/installdir/run-ldconfig.sh \
    -d 'openssl11' \
    -d 'bzip2' \
    -d 'zlib' \
    -d 'sqlite' \
    -d 'ncurses' \
    -d 'libffi' \
    -d 'gdbm' \
    -d 'tk' \
    --directories=/usr/local/lib/python3.10/ \
    usr/local