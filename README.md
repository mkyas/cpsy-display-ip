# cpsy-display-ip
Demonstrates the SSD1306 OLED by showing the IP address on the system boot.

This repository contains the file `display-ip.py` that displays an IP
address on the  SSD1306 OLED screen and the file `display-ip.service`
that executes the script on boot after the Raspberry Pi is connected
to a network.

The file `display-ip.service` is a service file for [systemd](https://systemd.io/).
The system will execute it as part of the boot process.

To use the script, you first must connect the screen to the Pi's
I2C bus.

## Setup

Do the following steps on your Raspberry Pi.

1. Install [pillow](https://python-pillow.org/), numpy, and venv:
   > sudo apt install python3-venv python3-pil python3-numpy
2. Create a virtual environment, here called `cpsy` (substitute your own name):
   > python3 -m venv --system-site-packages cpsy
3. Activate the environment `source cpsy/bin/activate`
4. Install the display driver: `pip install adafruit-circuitpython-ssd1306`
5. Copy the `display-ip.py` script to the virtual environment on your Raspberry Pi
6. Edit `display-ip.service` such that
   - `User` should be your user name on the Raspberry Pi
   - `WorkingDirectory` must be the directory containing `display-ip.py`
   - In `ExecStart` the path to `python` must point into your virtual environment
7. Copy the edited `display-ip.service` to `/etc/systemd/system`
   > sudo install -m 0644 -o root -g root display-ip.service /etc/systemd/system
8. Enable the service
   > sudo systemctl enable display-ip.service`
9. Test by starting the service
   > sudo systemctl start display-ip.service
