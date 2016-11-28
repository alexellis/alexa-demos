FROM alexellis2/python2-envirophat-armhf:2-dev

RUN pip install paho-mqtt
WORKDIR /root/
RUN git clone https://github.com/pimoroni/unicorn-hat
WORKDIR /root/unicorn-hat/library/ws2812
RUN python ./setup.py install
RUN apt-get update -qy && apt-get install make build-essential

WORKDIR /root/unicorn-hat/library/rpi-ws281x
RUN python ./setup.py install
WORKDIR /root/unicorn-hat/library/UnicornHat

# Unlock full brightness
RUN sed -ie s/128/255/g ./unicornhat.py
RUN python ./setup.py install

COPY app.py app.py
ENTRYPOINT []
CMD ["python", "app.py"]
