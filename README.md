# i3-setup-guide
A setup guide for i3 windows manager in Ubuntu

## Install i3

```
sudo apt install i3
```

Reboot your PC and select i3 in the login screen.

## Install dependences

```
sudo apt install \
i3blocks \
feh \
scrot \
fonts-font-awesome \
acpi \
pulseaudio \
util-linux \
rofi \
i3lock
```

## Setup i3blocks configuration

Put this in `~/.config/i3blocks/config`:

```
[volume-pulseaudio]
command=/home/dizzyrobin/.config/i3blocks/volume-pulseaudio
interval=once
signal=1

[battery2]
command=/home/dizzyrobin/.config/i3blocks/battery2
markup=pango
interval=30

[calendar]
command=/home/dizzyrobin/.config/i3blocks/calendar
interval=1
label=
```

(you **MUST** change the username *dizzyrobin* for your own username)

After that, copy the scripts in this repo folder `i3blocks-scripts` in your i3blocks config folder. Then, give them execution rights with `chmod +x`.

## Setup i3 configuration

Add this to your i3 configuration:

```
# Lock screen
bindsym $mod+p exec i3lock -c 000000 -e -f

# Remove window titlebar
for_window [class="^.*"] border pixel 2

# Keys for volume
bindsym XF86AudioRaiseVolume exec amixer -q -D pulse sset Master 5%+ && pkill -RTMIN+1 i3blocks
bindsym XF86AudioLowerVolume exec amixer -q -D pulse sset Master 5%- && pkill -RTMIN+1 i3blocks
bindsym XF86AudioMute exec amixer -q -D pulse sset Master toggle && pkill -RTMIN+1 i3blocks

# For the calendar in i3blocks
for_window [class="Yad"] floating enable

# Network manager
exec --no-startup-id "nm-applet"

# Wallpaper
exec --no-startup-id feh --bg-scale ~/Pictures/i3-blue.png

```

Change the application launcher:

```
# Comment this line
# bindsym $mod+d exec dmenu_run

# Add this line
bindsym $mod+d exec "rofi -show run -color-window '#222222, #555566, #b1b4b3' -color-normal '#222222, #b1b4b3, #222222, #005577, #b1b4b3'"
```

Change the bar content:

```
bar {
    # Set up status_command to this
    status_command i3blocks
        
    output primary
}
```

## Done!

Now reboot and you're done!

Additionally, I like to install this other utilities:

```
sudo apt install okteta texlive texlive-lang-spanish texlive-latex-extra gcc g++ vlc wxmaxima thunderbird libreoffice gparted git audacity gdb evince vim geany terminator meld gimp make automake mtools pavucontrol trash-cli
```