FROM nvcr.io/nvidia/l4t-pytorch:r32.6.1-pth1.8-py3
RUN apt-get update
RUN pip3 install --upgrade pip
RUN pip3 install flask libpng-bins requests
RUN apt-get -y install libpng-dev libjpeg-dev
RUN cd ~ && \
    mkdir -p dlib && \
    cd  dlib/ && \
    wget http://dlib.net/files/dlib-19.21.tar.bz2  && \
    tar jxvf dlib-19.21.tar.bz2  && \
    cd dlib-19.21/  && \
    mkdir build   && \
    cd build/   && \
    cmake ..   && \
    cmake --build .  && \
    cd ../  && \
    python3 setup.py install
RUN pip3 install face_recognition 
RUN pip3 install opencv-python opencv-contrib-python
RUN python3 -c 'import dlib;print(dlib.__version__)'
WORKDIR /app
COPY *.py /app/
RUN mkdir /app/faces
COPY faces /app/faces
ENV FLASK_APP=server
ENV LC_ALL=C.UTF-8
ENV LANG=C.UTF-8
ENV PATH="$PATH:/usr/local/cuda-10.0/bin"
ENV LD_LIBRARY_PATH="/usr/local/cuda-10.0/lib64"${LD_LIBRARY_PATH:+:${LD_LIBRARY_PATH}}
CMD python3 -m flask run --host 0.0.0.0
