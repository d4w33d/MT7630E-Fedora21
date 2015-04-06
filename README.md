
# MT7630E driver for Fedora 21+

Mediatek provides a Linux driver for **MT7630E**, which is only working on
kernels **3.13** and **3.14**. So working on Ubuntu, but not on latest
Fedora versions.

This bash script attempt to patch the given driver, compile it, then install it.

There is also a command to enable (`insmod`) the drivers at startup.

## Installation

    $ cd ~/path/to/your/bin/folder
    $ git clone https://github.com/d4w33d/MT7630E-Fedora21 mt7630e

## Usage

### Setup drivers

For beginning, you need to compile and install the drivers.

    $ sudo ./mt7630e install

**You'll need to redo this step for every kernel update.**

### Enable drivers

Once the drivers are initialized, you'll need to do this at every startup:

    $ sudo ./mt7630e enable

Of course, you can make it easier, by creating a `systemd` service:

    $ sudo nano /usr/lib/systemd/system/wifi.service

Paste this code, modifying the **/abs/path/to/your/bin/folder**.

    [Unit]
    Description=Enable Wi-Fi driver

    [Service]
    WorkingDirectory=/
    Type=forking
    ExecStart=/abs/path/to/your/bin/folder/7630e/mt7630e enable
    KillMode=process

    [Install]
    WantedBy=multi-user.target

The last thing you need to do is to enable the service:

    $ sudo systemctl enable wifi

It's done.
