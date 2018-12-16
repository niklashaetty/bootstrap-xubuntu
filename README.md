# This thing does stuff

## Get started

### Install Ansible
```console
sudo apt install ansible
```

### Set user
Edit the 'user' parameter in  ```host_vars/all```

### Run the scripts
```console
ansible-playbook start.yml --extra-vars "ansible_become_pass=<sudo_password>"
```

## How to monitor for xfce4 settings.
The easiest way to find out what the setting is called is by monitoring the channel and manually changing the setting. For example, if we want to change the wallpaper we monitor the xfce4-desktop channel:

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
  shell: "xfconf-query --channel xfce4-desktop --property /backdrop/screen0/monitor0/workspace0/last-image --set /home/{{user}}/Pictures/wallpaper/wallpaper.jpg"
```
