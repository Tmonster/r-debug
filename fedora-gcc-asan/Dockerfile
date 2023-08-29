## Set a default user. Available via runtime flag
FROM fedora:38

MAINTAINER Tom Ebergen "tom@ebergen.com"

RUN dnf install -y \
	gcc-gfortran \
	less \
	ca-certificates \
	curl \
	java-1.8.0-openjdk \
	bzip2-devel \
	cairo-devel \
	ghostscript \
	libcurl-devel \
	libicu-devel \
	libjpeg-turbo-devel \
	pango-devel \
	pcre-devel \
	libpng-devel \
	readline-devel \
	libtiff-devel \
	libX11-devel \
	libXt-devel \
	subversion \
	tcl-devel \
	texinfo \
	texlive-latex \
	texlive-collection-fontsextra \
	texlive-scheme-basic \
	tk-devel \
	unzip \
	xorg-x11-proto-devel \
	findutils \
	make \
	texinfo-tex \
	xz-devel \
	zlib-devel \
	libXmu-devel \
	tar \
	texlive-ec \
	texlive-parskip \
	texlive-collection-fontsrecommended \
	which \
	xorg-x11-server-Xvfb \
	g++ \
	git-all \
	libasan \
	libubsan \
	rsync

RUN dnf install -y \
	gcc \
	gcc-c++

RUN dnf install -y \
	dnf-plugins-core

RUN dnf install -y glibc-langpack-en.x86_64

RUN dnf install -y valgrind

RUN dnf install -y qpdf

RUN curl -o /usr/bin/pandoc.gz \
         https://files.r-hub.io/pandoc/linux-64/pandoc.gz && \
    gzip -d /usr/bin/pandoc.gz && \
    curl -o /usr/bin/pandoc-citeproc.gz \
	 https://files.r-hub.io/pandoc/linux-64/pandoc-citeproc.gz && \
    gzip -d /usr/bin/pandoc-citeproc.gz && \
    chmod +x /usr/bin/pandoc /usr/bin/pandoc-citeproc

RUN dnf install -y aspell aspell-en

RUN dnf install -y file

RUN dnf install -y xorg-x11-fonts-100dpi xorg-x11-fonts-75dpi

RUN dnf update -y

RUN cd /tmp \
    && svn co https://svn.r-project.org/R/trunk R-devel

RUN yum -y install rsync


# export RPREFIX="/opt/R-devel"
# export ROPTIONS="--without-recommended-packages --disable-openmp"
# export CFLAGS="-fstack-protector-strong -Wformat -Werror=format-security -Wdate-time -D_FORTIFY_SOURCE=2 -g -O0 -Wall"
# export CXXFLAGS="-fstack-protector-strong -Wformat -Werror=format-security -Wdate-time -D_FORTIFY_SOURCE=2 -g -O0 -Wall"
# export R_BATCHSAVE="--no-save --no-restore"
# export CXX="g++ -fsanitize=address,undefined,bounds-strict -fno-omit-frame-pointer"
# export CFLAGS="-fstack-protector-strong -Wformat -Werror=format-security -Wdate-time -D_FORTIFY_SOURCE=2 -g -O0 -Wall -pedantic -fsanitize=address"
# export DEFS="-DSWITCH_TO_REFCN"
# export FFLAGS="-g -O0"
# export FCFLAGS="-g -O0"
# export CXXFLAGS="-Wall -pedantic"
# export MAIN_LDFLAGS="-fsanitize=address,undefined -pthread"


ENV RPREFIX /opt/R-devel
ENV ROPTIONS --without-recommended-packages --disable-openmp
ENV CFLAGS -fstack-protector-strong -Wformat -Werror=format-security -Wdate-time -D_FORTIFY_SOURCE=2 -g -O0 -Wall
ENV CXXFLAGS -fstack-protector-strong -Wformat -Werror=format-security -Wdate-time -D_FORTIFY_SOURCE=2 -g -O0 -Wall
ENV R_BATCHSAVE --no-save --no-restore
ENV CXX g++ -fsanitize=address,undefined,bounds-strict -fno-omit-frame-pointer
ENV CFLAGS -fstack-protector-strong -Wformat -Werror=format-security -Wdate-time -D_FORTIFY_SOURCE=2 -g -O0 -Wall -pedantic -fsanitize=address
ENV DEFS -DSWITCH_TO_REFCN
ENV FFLAGS -g -O0
ENV FCFLAGS -g -O0
ENV CXXFLAGS -Wall -pedantic
ENV MAIN_LDFLAGS -fsanitize=address,undefined -pthread

RUN cd /tmp/R-devel \
    && ./tools/rsync-recommended \
    ./configure --prefix=${RPREFIX} ${ROPTIONS}              \


# RUN make
# RUN make install

# COPY xvfb-run /usr/local/bin/xvfb-run

# RUN chmod +x /usr/local/bin/xvfb-run && \
#    rm -f /bin/xvfb-run /usr/bin/xvfb-run

ENV RHUB_PLATFORM linux-x86_64-fedora-gcc