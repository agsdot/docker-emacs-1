FROM alpine:3.9

RUN apk add --no-cache \
        alsa-lib-dev \
        aspell \
        aspell-en \
        autoconf \
        automake \
        build-base \
        curl \
        dpkg \
        dpkg-dev \
        fontconfig-dev \
        gawk \
        gconf-dev \
        giflib-dev \
        git \
        glib-dev \
        gnupg \
        gnutls-dev \
        gtk+3.0-dev \
        jansson-dev \
        lcms2-dev \
        libcanberra-gtk3 \
        libjpeg-turbo-dev \
        libpng-dev \
        librsvg-dev \
        libxaw-dev \
        libxml2-dev \
        ncurses-dev \
        openssh-client \
        pango-dev \
        paxmark \
        texinfo \
        tiff-dev \
        wget

RUN git clone --depth 1 --branch emacs-27.1 git://git.sv.gnu.org/emacs.git /opt/emacs && \
    cd /opt/emacs && \
    ./autogen.sh && \
    ./configure --build="$(dpkg-architecture --query DEB_BUILD_GNU_TYPE)" --with-modules && \
    make && \
    make install

RUN mkdir -p /root/.emacs.d/elpa/gnupg && \
    chmod 700 /root/.emacs.d/elpa/gnupg && \
    for i in {1..3}; do \
      gpg --keyserver keyserver.ubuntu.com \
          --homedir /root/.emacs.d/elpa/gnupg \
          --recv-keys 066DAFCB81E42C40 \
      && break || sleep 15; \
    done

CMD ["emacs"]
