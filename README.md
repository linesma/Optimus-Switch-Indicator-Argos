# Optimus-Switch-Indicator-Argos-Manjaro
Indicator for Optimus Switch on Manjaro using Argos API

![Optimus-Switch-Indicator-Argos-Manjaro](https://github.com/linesma/Optimus-Switch-Indicator-Argos-Manjaro/blob/master/screenshots/optimus-switcher-intel.jpg)     ![Optimus-Switch-Indicator-Argos-Manjaro](https://github.com/linesma/Optimus-Switch-Indicator-Argos-Manjaro/blob/master/screenshots/optimus-switcher-nvidia.jpg)

This is a fork of argos-indicator-nvidia-prime by cyberalex4life located here: https://github.com/cyberalex4life/argos-indicator-nvidia-prime

It has been updated to switch between the nVidia and Intel graphics cards on Optimus laptops running Manjaro by using the Optimus-Switch program by dglt1 located here: https://github.com/dglt1/optimus-switch-gdm

Thank you to the authors of both programs.

#### Requirements
- [Argos](https://extensions.gnome.org/extension/1176/argos/) Gnome Shell extension.
- Optimus-Switch-GDM located here: https://github.com/dglt1/optimus-switch-gdm
- [pkroot](https://github.com/cyberalex4life/pkroot) - minimum already provided in this repository
- Output of `nvidia-smi -L` This will allow for the indication of which graphics card is in use.

#### Installation
Install [Optimus-Switch-GDM](https://github.com/dglt1/optimus-switch-gdm)

Install [Argos](https://extensions.gnome.org/extension/1176/argos/) Gnome-Shell extension.

Ensure that your system is using the nVidia GPU or you will not get the information needed for later in the install.

Create directory `~/.local/share/icons` if it does not exist:
```
! [ -d "~/.local/share/icons" ] && mkdir --parents ~/.local/share/icons || trueg
```

Then:
```
git clone https://github.com/linesma/Optimus-Switch-Indicator-Argos-Manjaro.git
cd Optimus-Switch-Indicator-Argos-Manjaro
# copy icons
cp -v icons/* ~/.local/share/icons/
#Get the output of `nvidia-smi -L`
`nvidia-smi -L`
Copy the result to your favorite text editor.
# edit 'optimus-switcher.sh' to match the results of `nvidia-smi -L`
nano optimus-switcher.sh
Look for the line `if [ "$QUERY" == 'GPU 0: GeForce GTX 1050 (UUID: GPU-15a83262-39d2-62ee-e0bf-04fb8ae648b0)' ]; then`
Change 'GPU 0: GeForce GTX 1050 (UUID: GPU-15a83262-39d2-62ee-e0bf-04fb8ae648b0)' to match the output of `nvidia-smi-L`
ctrl+x to save and exit the file.
# copy 'optimus-switcher.sh' to 'argos' folder
cp -v optimus-switcher.sh ~/.config/argos/
# backup the default Argos configuration
cp ~/.config/argos/argos.sh ~/Documents
# delete the default Argos configuration
rm ~/.config/argos/argos.sh
# copy polkit policy in place
sudo cp org.freedesktop.policykit.pkexec.prime-select.policy /usr/share/polkit-1/actions/
# copy pkroot to '/usr/local/bin' and make sure it is executable
sudo cp pkroot /usr/local/bin
sudo chmod a+x /usr/local/bin/pkroot
```
#### Uninstall
```
# remove icons
rm ~/.local/share/icons-to-delete/{nvidia-active-symbolic.svg,nvidia-inactive-symbolic.svg,prime-indicator-intel.svg,prime-indicator-intel-symbolic.svg,prime-indicator-nvidia.svg}
# remove policy
sudo rm org.freedesktop.policykit.pkexec.prime-select.policy /usr/share/polkit-1/actions/
# remove argos extension script
rm ~/.config/argos/optimus-switcher.sh
# remove pkroot script
sudo rm /usr/local/bin/pkroot
```
Then uninstall Argos if you don't need it anymore.

