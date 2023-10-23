# Installation basics to get up and running developing on a new Mac

First we install the Xcode CLI tools

```sh
xcode-select --install
```

The rest can be done in variable order, depending on how much you'd like to depend on Homebrew to manage other dependencies. I have yet to determine how I really feel on the matter :)

## Essentials

### Install [Homebrew](https://brew.sh) (aka `brew`)

The all-around solid dependency manager. Can aid in further installations below.  
```sh
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

### Install [iTerm2](https://iterm2.com/)

Recommended terminal replacement/emulation for Mac OS  

For a 'normal' installation download the [latest iTerm2](https://iterm2.com/downloads/stable/latest)  
**OR**  
```sh
brew install --cask iterm2
```

### Install [`pyenv`](https://github.com/pyenv/pyenv)[^brew-pyenv-note]

Python version management via the command line  
```sh
brew install pyenv
```  
**OR**  
```sh
curl https://pyenv.run | bash
```

### Install [`nvm`](https://nvm.sh)

Node version management via the command line that _might_ be worth the effort  
Run the install script:[^nvm-shell-note]  
```sh
PROFILE=/dev/null bash -c 'curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.5/install.sh | bash'
```

NVM is _slow_ on shell startup so we customize the shell integration to lazy-load all its associated commands. Add the following to .zshrc:  
```sh
FILE="$HOME/.nvmfunc"
if test -f "$FILE"; then
    source $FILE
fi
```  
And pull the .nvmfunc calls file to your local home directory: [.nvmfunc](.nvmfunc)  
**OR**  
It has a warning-like Caveat in the installation logging so might not be recommended but:  
```sh
brew install nvm
```

### Install [VSCode](https://code.visualstudio.com/)

To use the GUI installer:  
https://code.visualstudio.com/Download  

Download versions of the app directly:  
[Get latest Intel-chip version](https://update.code.visualstudio.com/latest/darwin/stable)  
or  
[Get latest Apple Silicon version](https://update.code.visualstudio.com/latest/darwin-arm64/stable)  

### Install [Docker](https://www.docker.com/)

Download the installer depending on your chip:  
- [Docker Desktop for Apple silicon](https://desktop.docker.com/mac/main/arm64/Docker.dmg)
- [Docker Desktop for Intel](https://desktop.docker.com/mac/main/amd64/Docker.dmg)  

Once dmg image file is downloaded, it can be opened to follow the usual 'copy to /Applications' flow or, there's this from the [docker docs](https://docs.docker.com/desktop/install/mac-install/#install-and-run-docker-desktop-on-mac):  
```sh
sudo hdiutil attach Docker.dmg
sudo /Volumes/Docker/Docker.app/Contents/MacOS/install
sudo hdiutil detach /Volumes/Docker
```  
**OR**
it's also available on `brew` (may require additional dependencies):  
```sh
brew install docker
```

### Install [BBEdit](https://www.barebones.com/products/bbedit/)

Plaintext editor and notepad. Their tagline is "It doesn't suck" and it's correct  
[Download here](https://www.barebones.com/products/bbedit/download.html)  
**OR**  
```sh
brew install --cask bbedit
```

## Nice to haves

These include a database connection GUI (dbeaver), a real image processor (gimp), a solid clipboard manager (maccy), and a decent Mac OS window management system (rectangle):  

If you want them all:  
```sh
brew install --cask gimp rectangle maccy dbeaver-community
```  

Or a-la-carte:  
```sh
brew install --cask gimp
```  
```sh
brew install --cask rectangle
```  
```sh
brew install --cask maccy
```  
```sh
brew install --cask dbeaver-community
```  

[^brew-pyenv-note]: If you use Homebrew to manage pyenv the versions available to pyenv are limited by the Homebrew update cycle

[^nvm-shell-note]: Setting PROFILE in the call to installation script to avoid it automatically writing to shell config
