# This thing does stuff
There are currently 3 roles:
* Utils:
	- Git configs
	- Shortcuts
	- python and easy_install
	- vim
	- + some general packages
* Appearance
	- Theme: Victory gtk
	- Window manager: Victory gtk
	- Icons: Papirus
	- Panel: Slightly modified xfce4 default panel
	- Terminal: Xfce4 dropdown with Nord theme
* Programs
	- Chrome
	- Sublime 

## Appearance screenshots:
![](/images/screenshot.png)

## Get started
You need to have git installed and the repository cloned. 

### Install Ansible
```console
sudo apt install ansible
```

### Set vars
Set variables in  ```start.yml```

### Run the scripts
Each role is tagged with its name, so you can choose which roles you want.
### To run everything
```console
ansible-playbook start.yml --ask-become-pass
```

### To run only e.g. appearance and utils
```console
ansible-playbook start.yml --ask-become-pass --tags "appearance, utils"
```

### To skip i.e. appearance
```console
ansible-playbook start.yml --ask-become-pass --skip-tags "appearance"
```

## How to find out what a xfconf setting is called.
The easiest way to find out what the setting is called is by monitoring the channel and manually changing the setting. You need to figure out what channel the setting is connected to first. Then as an example, if we want to change the wallpaper we monitor the xfce4-desktop channel:

```console
niklas@nangijala:~$ xfconf-query -c xfce4-desktop -m
Start monitoring channel "xfce4-desktop":
```
 and then change the wallpaper manually, which will give us the following output:
 ```console
set: /backdrop/screen0/monitor0/workspace0/last-image
```

Then simply change the setting with ansible (here we change the wallpaper to a cool one)
```yaml
- name: Set wallpaper
  shell: "xfconf-query --channel xfce4-desktop --property /backdrop/screen0/monitor0/workspace0/last-image --set {{ install_dir }}/wallpaper.jpg"
```
