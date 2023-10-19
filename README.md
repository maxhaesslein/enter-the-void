# Enter the Void v.1

Live audioreactive visuals on a Raspberry Pi 4. Currently a work in progress, more info soon.

## Installation

Use a fresh Raspberry Pi OS Lite 32-bit installation on a Raspberry Pi 4 or later. Install required dependencies with:

```bash
sudo apt install python3-pip python3-pyaudio python3-aubio xserver-xorg xinit
pip install pygame
# for font support in pygame:
sudo apt install libsdl2-ttf-2.0-0
# for png support in pygame:
sudo apt install libsdl2-image-2.0-0
```

Then download or clone this repo, extract it into `~/enter-the-void` (this path is hardcoded at some places, if you want to use another path, change the code accordingly). Then start everything by calling the `start` file.

## Microphone

You also need to make sure that you have a microphone connected and set up correctly. You may need to add a `~/.asoundrc` file, mine has this content for a cheap usb mic:

```
pcm.!default {
  type asym
  capture.pcm "mic"
}
pcm.mic {
  type plug
  slave {
    pcm "hw:1,0"
  }
}
```

## starting over SSH

To allow starting over SSH, you may want to add this to your */etc/X11/Xwrapper.config*:

```
allowed_users=anybody # was: console
```

then you can call the *start* file over SSH

## Autostart

To autostart, copy the `enter-the-void.service` file into `~/.config/systemd/user/enter-the-void.service` and then activate it with:

```
sudo systemctl daemon-reload
systemctl --user enable enter-the-void.service
systemctl --user start enter-the-void.service
journalctl --user -u enter-the-void.service
```
