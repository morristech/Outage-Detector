# Outage Detector
Simple module meant to notify user if a power outage has occured or if the internet has been down.

## What it does

At every run it writes to a text file timestamps for power and internet, whether the last run was scheduled or at boot and the last calculated periodicity.

If the script was run after a boot up, it will assume there was a power outage (the system is meant to run 24/7, for example a Raspberry Pi Zero) and send a notification, approximating the power outage duration through the last known timestamp and calculated periodicity of the runs.

Internet downtime is detected if the 2 timestamps written to the file differ and the downtime is approximated again through the calculated periodicity. It is possible that an internet downtime is missed if the script is run too rarely.

## How to run it

Install the module in a virtual environment with pip:

```
pip install Outage-Detector
```

Alternatively, you can also install the module by cloning this git repo and running setup.py

```
git clone https://github.com/fabytm/Outage-Detector.git
python setup.py install
```

Afterwards, all you need to do is to run the outage_detector command line interface for the initialization process:

```
outage_detector --init
```

From here you can choose the way you want to be notified and will be prompted to enter either your e-mail information or PushBullet API key.

Additionally, it will also ask you if you want to set up scheduling for this module. Choosing to do so is recommended for inexperienced users (this will create 2 cron jobs, one running at boot time and one every 5 minutes, to check in on internet status and record timestamp if either the internet connection drops or a power outage happens).

