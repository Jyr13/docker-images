FROM centos:7

run yum install -y epel-release centos-release-scl

run yum install -y rh-python36 rh-python36-python-virtualenv \
    gcc xorg-x11-server-Xvfb make which ghostscript sudo \
    libtiff-devel libjpeg-devel zlib-devel freetype-devel \
    lcms2-devel libwebp-devel openjpeg2-devel tkinter \
    tcl-devel tk-devel libffi-devel libimagequant-devel \
    libraqm-devel

RUN useradd --uid 1000 pillow

RUN bash -c "source /opt/rh/rh-python36/enable && \
    /opt/rh/rh-python36/root/usr/bin/virtualenv -p python3.6 --system-site-packages /vpy3 && \
    /vpy3/bin/pip install --upgrade pip && \
    /vpy3/bin/pip install cffi olefile pytest pytest-cov && \
    /vpy3/bin/pip install numpy --only-binary=:all: || true && \
    cat /opt/rh/rh-python36/enable /vpy3/bin/activate > /vpy3/bin/activate3.6 && \
    mv /vpy3/bin/activate3.6 /vpy3/bin/activate && \
    chown -R pillow:pillow /vpy3"

ADD depends /depends

USER pillow
CMD ["depends/test.sh"]

#docker run -v $TRAVIS_BUILD_DIR:/Pillow pythonpillow/centos-7-amd64
