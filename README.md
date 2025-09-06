# Hyprland-Customization-and-Theming


This tutorial documents how I set up Hyprland and themed the whole stack (boot → login → desktop) while keeping performance in mind. It shows the commands I used, which configs I edited, and the small tweaks that make the setup feel polished and consistent.

> Goal: beautiful, responsive desktop with sensible defaults  (tuned DPI, readable top bar, consistent fonts) ready for follow-up performance tuning.


---


## Prerequisites

Arch-based system (Arch Linux / EndeavourOS installed and updated)

Basic familiarity with terminal and nano / editing config files

git and curl installed



---



## Quick notes before starting

I credit the original Hyprland configs (end-4 dots) and theme authors — see Credits at the end. Use them as a base and customize.

Take backups of any config before editing.

When running scripts from the web, inspect them first if you’re unsure.



---


## Initial (recommended) install attempt

Run the End-4 Hyprland setup script (this installs dotfiles, packages etc.):

```
sudo pacman -Sy
bash <(curl -s "https://end-4.github.io/dots-hyprland-wiki/setup.sh")
```

This script consist of lot of commands, You need to be attentive and enter password many times in this. In my opinion, press "n" at the beginning so it will require less clicks.

![Image Alt](https://github.com/saksham-991/Hyprland-Customization-and-Theming/blob/2c3e38a30df166f7b244f755474860fc731dfc04/images/IMG_20250906_233653_488.jpg)

Note:- `yay` commands throughout the script **can** fail, so just press R to retry once, if they fail again then just press "i" to ignore the command/error.



---



## First boot (initial look)


![Image Alt](https://github.com/saksham-991/Hyprland-Customization-and-Theming/blob/5085f66c153fe63df05f141fc25fbbf3eb4168b8/images/IMG_20250906_220136_811.jpg)

You can use any wallpaper, Here is mine:-

https://512pixels.net/downloads/macos-wallpapers-6k/10-11-6k.jpg

Save the wallpaper to ~/.config/wallpapers/ and set it in your Hyprland desktop by pressing Ctrl + Alt + T and choosing from the popped up file manager.


---



## Install NWG-Look (widget/theme manager)

`sudo pacman -S nwg-look`

NWG-Look helps manage GTK and shell themes for Wayland setups.

It is pretty easy to configure it, just choose , apply and try font size, font style, widget theme, dark/light theme etc according to your choice and display.


---



## Edit Hyprland rules and general config

To get blur/transparency in all windows globally.
Open the rules file:-

`sudo nano ~/.config/hypr/hyprland/rules.conf`

![Image Alt](https://github.com/saksham-991/Hyprland-Customization-and-Theming/blob/5085f66c153fe63df05f141fc25fbbf3eb4168b8/images/IMG_20250906_220139_489.jpg)

In the 4th line, (including empty line), i.e `windowrulev2 = opacity 0.89 override 0.89 override, class :.*`

To fix Anything basic (but further)
`sudo nano ~/.config/hypr/hyprland/general.conf`
 Go to this file and change values of desired term as you want, For example, you want more rounded corners, find decoration column and increase value of rounded corner/boundaries.

Same applies to Blur, visual noise, and animations.


---


## Sidebar settings / parallax (reduce “squishiness”)

Open the desktop sidebar/config GUI (or config file) and turn off parallax:

![Image Alt](https://github.com/saksham-991/Hyprland-Customization-and-Theming/blob/5085f66c153fe63df05f141fc25fbbf3eb4168b8/images/IMG_20250906_220142_393.jpg)

Click the sidebar (top-right) → Settings / Interface → turn off Wallpaper parallax / Depends on workspace / Depends on sidebars.

My preference: parallax off — it feels squishy and uses extra resources.


---


## QT font DPI

Set a global QT font DPI for consistent UI scale (adjust value to taste):
```
export QT_FONT_DPI=120
qs -c ~/.config/quickshell/ii &
```
120 worked for my 1920×1200 monitor. Adjust higher for higher-res screens.

Consider placing export QT_FONT_DPI=120 in your session startup script so it persists.

> Might make some font look blurry, but not very noticable, if you complete sharp fonts then only increase Global UI scaling in `sudo nano ~/.config/hypr/hyprland/general.conf` In the monitors section, There would be "1" written explicitly, after resolution. Increase that value higher or lower according to your display.


## Top bar & apps (file manager / browser)

Install Nautilus and Chromium (or your preferred apps):

`sudo pacman -S nautilus chromium`

Edit Hyprland keybinds to open Nautilus with Super + E:

```
cd ~/.config/hypr/hyprland
sudo nano keybinds.conf
# set: bind = Super, E, exec, ~/.config/hypr/hyprland/scripts/launch_first_available.sh "nautilus" ...
```

Remove references to dolphin (if your script lists multiple file managers, you can remove/replace).

In Chromium, turn on GTK theme inside Settings so it matches the desktop. Set page scaling to 110 if needed.


---


## SDDM theme (login screen)

Install a polished SDDM theme (example: Astronaut theme):

```
sh -c "$(curl -fsSL https://raw.githubusercontent.com/keyitdev/sddm-astronaut-theme/master/setup.sh)"
```

Choose the desired SDDM theme when the script asks.

![Image Alt](https://github.com/saksham-991/Hyprland-Customization-and-Theming/blob/2c3e38a30df166f7b244f755474860fc731dfc04/images/IMG_20250906_234101.jpg)


---


## Gemini sidebar / LLM API (optional)

If you want a sidebar connected to an LLM (Gemini in this example), create an API key:

1. Go to: https://aistudio.google.com/apikey


2. Click Create API Key → create a normal project → follow prompts → copy the API key.


3. Paste into the sidebar settings or config where it asks for the API key (top-left sidebar → Settings → API key).



Keep API keys secret.

![Images Alt](https://github.com/saksham-991/Hyprland-Customization-and-Theming/blob/5085f66c153fe63df05f141fc25fbbf3eb4168b8/images/IMG_20250906_220147_665.jpg)

---


## GRUB menu theming

Clone and install a GRUB theme (example: Sekiro GRUB theme):

```
git clone https://github.com/semimqmo/sekiro_grub_theme
cd sekiro_grub_theme
sudo ./install.sh
```

![Images Alt](https://github.com/saksham-991/Hyprland-Customization-and-Theming/blob/2c3e38a30df166f7b244f755474860fc731dfc04/images/IMG_20250906_234015.jpg)

There are many themes — browse https://github.com/semimqmo/ for alternatives.


## Finalize & Reboot

`sudo reboot`

Check login screen, Grub menu, and everything and verify Hyprland desktop looks as expected.


![Images Alt](https://github.com/saksham-991/Hyprland-Customization-and-Theming/blob/2c3e38a30df166f7b244f755474860fc731dfc04/images/IMG_20250906_233703_483.jpg)
---


# What I changed (example summary)

Disabled heavy parallax and noise for a cleaner desktop.

Tuned QT font DPI for consistent font sizes across apps.

Added Nautilus as default file manager and keybind for quick access.

Installed SDDM Astronaut theme and Sekiro GRUB theme for a unified aesthetic.


Result: Clean, modern desktop with consistent fonts, reduced jankiness, and polished boot/login experience.


---


# Showcase


https://github.com/saksham-991/Hyprland-Customization-and-Theming/blob/6f66066079c2e5690897e145a067cce2de61491b/images/VID_20250906_235501_882.mp4


## Troubleshooting & tips

Setup script failed? Retry once. If still failing, run steps manually or check the script for missing dependencies.

SDDM theme not showing? Ensure SDDM is enabled and set as the display manager:

sudo systemctl enable sddm.service --now

Fonts look tiny/huge? Tweak QT_FONT_DPI and your Hyprland scale settings.

Browser not following GTK? In Chromium, enable GTK theme in settings and ensure a GTK theme is installed and active.


## Credits & links

Base Hyprland/dotfiles inspiration: End-4 — https://end-4.github.io/dots-hyprland-wiki/

SDDM Astronaut theme: https://github.com/keyitdev/sddm-astronaut-theme

Sekiro GRUB themes: https://github.com/semimqmo/sekiro_grub_theme

Wallpaper source (example): https://512pixels.net/downloads/macos-wallpapers-6k/10-11-6k.jpg


> Please credit original authors if you base configs on their dotfiles. Don’t commit API keys or private info.


> Next repo (next goal) --> **Performance tuning/Optimization**
