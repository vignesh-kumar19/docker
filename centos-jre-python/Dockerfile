# Base image from centos:6.9
From centos:6.9
MAINTAINER kvkumar1993@gmail.com

#Setting env variable
ENV PYTHON_VER 2.7.6
RUN yum -y install wget && yum clean all

# Installing JRE 8 
RUN wget --no-cookies --no-check-certificate --header "Cookie: gpw_e24=http%3A%2F%2Fwww.oracle.com%2F; oraclelicense=accept-securebackup-cookie" "http://download.oracle.com/otn-pub/java/jdk/8u141-b15/336fa29ff2bb4ef291e347e091f7f4a7/jre-8u141-linux-x64.rpm" \
   && yum localinstall -y jre-8u141-linux-x64.rpm \
   && rm -f /jre-8u141-linux-x64.rpm \
   && yum clean all

# --------------------------------------- Start of installing Python2.7, pip, virtual environment ------------------------------------- #

# Installing Python
RUN yum -y groupinstall 'Development Tools' && yum -y install \
    bzip2-devel \
    ncurses-devel \
    openssl-devel \
    sqlite-devel \
    zlib-devel \
    xz \
   && wget --no-check-certificate https://www.python.org/ftp/python/${PYTHON_VER}/Python-${PYTHON_VER}.tar.xz \
   && tar xf Python-${PYTHON_VER}.tar.xz \ 
   && cd Python-${PYTHON_VER} \
   && ./configure --prefix=/usr/local \
   &&  make \
   && make altinstall \
   && rm -rf /Python-${PYTHON_VER} /Python-${PYTHON_VER}.tar.xz \

# Creating symlink python -> python2.7
   && ln -s /usr/local/bin/python2.7 /usr/local/bin/python \

# Removing unwanted libs
   && yum remove -y autoconf automake bison byacc cscope ctags cvs diffstat doxygen elfutils flex gcc gcc-c++ gcc-gfortran gettext git indent intltool libtool patch patchutils rcs redhat-rpm-config rpm-build subversion swig systemtap autoconf automake bison byacc cscope ctags cvs diffstat doxygen elfutils flex gcc gcc-c++ gcc-gfortran gettext git indent intltool libtool patch patchutils rcs redhat-rpm-config rpm-build subversion swig systemtap   alsa-lib apr apr-util atk avahi-libs cairo cloog-ppl cpp cups-libs dbus-glib elfutils-libs fipscheck fipscheck-lib fontconfig freetype gdb gdk-pixbuf2 gettext-devel gettext-libs glibc-devel glibc-headers gnutls gtk2 hicolor-icon-theme hwdata initscripts iproute iptables iputils jasper-libs kernel-devel kernel-headers libICE libSM libX11 libX11-common libXau libXcomposite libXcursor libXdamage libXext libXfixes libXft libXi libXinerama libXrandr libXrender libXtst libart_lgpl libdrm libedit libgcj libgfortran libgomp libjpeg-turbo libpciaccess libpng libproxy libproxy-bin libproxy-python libstdc++-devel libthai libtiff libxcb m4 mailcap mpfr neon openssh openssh-clients pakchois pango perl perl-Compress-Raw-Zlib perl-Compress-Zlib perl-Error perl-Git perl-HTML-Parser perl-HTML-Tagset perl-IO-Compress-Base perl-IO-Compress-Zlib perl-Module-Pluggable perl-Pod-Escapes perl-Pod-Simple perl-URI perl-XML-Parser perl-libs perl-libwww-perl perl-version pixman plymouth policycoreutils ppl redhat-logos rsync systemtap-client systemtap-devel systemtap-runtime sysvinit-tools udev unzip upstart util-linux-ng xz xz-lzma-compat zip bzip2-devel ncurses-devel openssl-devel sqlite-devel zlib-devel \
  && yum clean all

# Installing setuptools
RUN  wget https://pypi.python.org/packages/source/s/setuptools/setuptools-1.4.2.tar.gz \
   && tar -xvzf setuptools-1.4.2.tar.gz \
   && cd setuptools-1.4.2 \

# Installing Dependencies 
   && python2.7 setup.py install \

# installing pip and virtualenv
   && curl https://bootstrap.pypa.io/get-pip.py | python2.7 - \
   && pip install virtualenv \
   && rm -rf /setuptools-1.4.2* 

# ---------------------------------------End of installing Python2.7, pip, virtual environment ------------------------------------- #

# Installing Supervisord service
RUN easy_install supervisor && \
    mkdir -p /var/log/supervisor && \
    mkdir -p /etc/supervisor/conf.d

# Adding configuration file
ADD supervisor.conf /etc/supervisor.conf

# Start the supervisod service
CMD ["supervisord","-c","/etc/supervisor.conf"]
