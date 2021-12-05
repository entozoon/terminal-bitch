# Terminal Bitch

## Create SD

Pi OS Headless, then various install stuff from [here](https://github.com/entozoon/psion-pi).

Open `config.txt`

```
# Disable bluetooth (for stable serial output)
dtoverlay=disable-bt
```

## Configure

    sudo raspi-config

- update
- password
- hostname
- boot to console autologin
- serial port
- expand filesystem

## Overclocking

    sudo nano /boot/config.txt

```
#  Overclock (only with a heatsync!)
arm_freq=1200
```

## Software

````bash
sudo apt-get update
sudo apt-get dist-upgrade
```

### Micro

```bash
sudo apt-get install micro
micro -plugin install editorconfig
micro -plugin install detectindent
micro -plugin install comment
micro -plugin install gotham-colors
npm i -g prettier
nano ~/.config/micro/init.lua
````

```lua
local micro = import("micro")
local shell = import("micro/shell")
function gofmt(bp)
    bp:Save()
    local _, err = shell.RunCommand("prettier --write " .. bp.Buf.Path)
    if err ~= nil then
        micro.InfoBar():Error(_)
        return
    end

    bp.Buf:ReOpen()
end
function onSave(bp)
    if bp.Buf:FileType() == "javascript"
    or bp.Buf:FileType() == "jsx"
    or bp.Buf:FileType() == "angular"
    or bp.Buf:FileType() == "vue"
    or bp.Buf:FileType() == "flow"
    or bp.Buf:FileType() == "typescript"
    or bp.Buf:FileType() == "css"
    or bp.Buf:FileType() == "less"
    or bp.Buf:FileType() == "scss"
    or bp.Buf:FileType() == "html"
    or bp.Buf:FileType() == "json"
    or bp.Buf:FileType() == "graphql"
    or bp.Buf:FileType() == "markdown"
    or bp.Buf:FileType() == "yaml" then
        gofmt(bp)
    end
    return true
end
```

### Node

```bash
wget https://unofficial-builds.nodejs.org/download/release/v16.13.1/node-v16.13.1-linux-armv6l.tar.xz
tar xvfJ *.xz
sudo cp -R node-v16.13.1-linux-armv6l/* /usr/local
rm -rf node-*
sudo reboot
node -v
npm -v
```
