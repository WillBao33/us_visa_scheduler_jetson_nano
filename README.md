# US visa scheduler on Jetson Nano
Note: The program was originally from https://github.com/Soroosh-N/us_visa_scheduler and made executable on the Jetson Nano platform.
The visa_rescheduler is a bot for US VISA (usvisa-info.com) appointment rescheduling. This bot/program has been tested on the Jetson Nano platform.

## Prerequisites
- Having a US VISA appointment scheduled already.
- [Optional] API token from Pushover and/or a Sendgrid (for notifications)(You also can use the esender.php file in this repo as an email pusher on your website)

## Requirements
```
Python 3.10 and above
requests
selenium
chromium-browser
chromium-chromedriver
```
## How to run:
After updating the config.ini file, run:
```
python visa.py
```
## Notes
If you are getting some errors like below:
```
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
  File "/home/will/.local/lib/python3.10/site-packages/selenium/webdriver/chrome/webdriver.py", line 45, in __init__
    super().__init__(
  File "/home/will/.local/lib/python3.10/site-packages/selenium/webdriver/chromium/webdriver.py", line 50, in __init__
    if finder.get_browser_path():
  File "/home/will/.local/lib/python3.10/site-packages/selenium/webdriver/common/driver_finder.py", line 47, in get_browser_path
    return self._binary_paths()["browser_path"]
  File "/home/will/.local/lib/python3.10/site-packages/selenium/webdriver/common/driver_finder.py", line 78, in _binary_paths
    raise NoSuchDriverException(msg) from err
selenium.common.exceptions.NoSuchDriverException: Message: Unable to obtain driver for chrome; For documentation on this error, please visit: https://www.selenium.dev/documentation/webdriver/troubleshooting/errors/driver_location
```
This is probably because of the initial installation of chromium when initializing the Jetson Nano. Completely uninstall chromium and reinstall it will solve the issue:
```
sudo apt-get remove chromium-browser
rm -rf ~/.config/chromium
rm -rf ~/.cache/chromium
```
Clean up any remaining dependencies:
```
sudo apt-get autoremove
```
Ensure all components are uninstalled:
```
dpkg -l | grep -E 'chrome|chromium'
```
(Optional) Remove remaining configuration files and packages:
```
sudo apt-get purge chromium-browser
sudo apt-get purge chromium-codecs-ffmpeg-extra unity-scope-chromiumbookmarks
sudo apt-get autoremove
sudo apt-get autoclean
```
Reinstalling chromium and chromium webdriver:
```
sudo apt update
sudo apt install chromium-browser
sudo apt install chromium-chromedriver
```
