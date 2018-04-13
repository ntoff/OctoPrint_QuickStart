.. include:: urls.rst

Getting Started
===============

Installation Overview
---------------------

The quickest way to get started with OctoPrint is to use the Raspberry Pi specific distribution: `OctoPi <https://github.com/guysoft/OctoPi/>`_.

The general outline of how to get up and running is as follows -

* Download sd image
* Flash image to sd card
* Configure wifi / ssh password / hostname
* Connect 3d printer to raspberry pi with usb cable
* Connect raspberry pi to network through ethernet / wifi
* Open web browser and enjoy OctoPrint

Download
--------

Head on over to https://octoprint.org/download/ and download the lastest SD image.

Flash
-----

Flashing the OctoPi image is the same procedure as flashing any Raspberry Pi SD card image. See the details here: https://www.raspberrypi.org/documentation/installation/installing-images/README.md

Configuration
-------------

Editors to avoid
++++++++++++++++

Some text editors will destroy plain text files by adding extra information, others may save the files with incorrect line endings.

Try to avoid using editors such as

* Microsoft Word
* Wordpad
* Apple's TextEdit (if you must use this, make sure to configure it to disable smart quotes)
* Any other "rich text" editor that allows formatting of text with bold and itallic fonts.

Editors known to work
+++++++++++++++++++++

* Sublime
* Notepad++
* Microsoft's VS Code (not to  be confused with Visual Studio, VS Code is a free and open source, source code editor)
* Vi / Vim
* Nano

*If you're on a Windows OS, make sure to enable the display of filename extensions. Open the file and folder preferences and in the "View" tab untick "Hide extensions for known file types".*

Where to find the configuration files
+++++++++++++++++++++++++++++++++++++

The files we will be editing and / or creating will all be in the root of the ``/boot/`` folder. This location will show up as a removable drive if the SD card is inserted into a card reader in a PC or Mac, or simply by typing ``cd /boot`` at the command line if you're logged into the Raspberry Pi locally (using a keyboard and monitor plugged directly into the Pi).

WiFi
++++

To connect through wifi, open up the ``octopi-network.txt`` file in a suitable text editor and uncomment (remove the ``#`` marks) any relevant lines.
Do **not** uncomment all the lines hoping that one will work. If you are using WPA, then *only* uncomment the lines in the WPA section. If you're using WEP then only uncomment the lines in the WEP section.

After removing the ``#`` marks, enter your SSID and wifi password in the relevant fields.

For example if you were using WPA/WPA2, this:

.. code-block:: text

    ## WPA/WPA2 secured
    #iface wlan0-octopi inet manual
    #    wpa-ssid "put SSID here"
    #    wpa-psk "put password here"

would become this:

.. code-block:: text

    ## WPA/WPA2 secured
    iface wlan0-octopi inet manual
        wpa-ssid "mywifissid"
        wpa-psk "mywifipassword"

*IMPORTANT! Don't forget to uncomment the* ``iface wlan0-octopi inet manual`` *line from the relevant section!*

If you require advanced options, such as multiple networks to connect to automatically, please use the ``octopi-wpa-supplicant.txt`` file instead.

For example:

.. code-block:: text

    network={
      ssid="mywifissid"
      psk="mywifipassword"
    }

*Be very careful not to disturb the formatting inside these files. Editing it with certain text editors can destroy this files and prevent the system from booting.*

SSH Password
++++++++++++

By default the login details are

* Username: ``pi``
* Password: ``raspberry``

This should be changed, even if you don't intend to allow external access to your Raspberry Pi device. Any network attached device should never be left with default login credentials..

To change the password, create a plain text file called ``octopi-password.txt`` on the SD card, and enter your new password in plain text. The file will be deleted automatically once the system has applied the changes.


Host Name
+++++++++

If you have multiple OctoPi devices, it may be useful to change their host names so you can access each one by a different name. Changing the host name is the same process as changing the system password. Create a file called ``octopi-hostname.txt`` and enter your new host name inside this file (just the host name, do not enter any suffixes such as .lan, .net, .com, .local, or .home). The host name will automatically be changed on the next boot.


First Boot
----------

Once all the configuration files have been edited, you can now insert the SD card into your Raspberry Pi and boot it. If you've been editing the files on your Pi, please restart it with ``sudo shutdown -r now``.

*The first time OctoPi boots up, it will take slightly longer than normal because it will automatically resize the partition(s) to fill the entire SD card. Please be patient during this time and do not reset or turn off the Raspberry Pi.*

Once the process has completed, you should be able to point your web browser at http://octopi.local and be greeted with the first run wizard. If you changed your host name then it will be available at http://yournewhostname.local instead.