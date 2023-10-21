# Installation basics to get up and running developing on a new Mac

First we install the Xcode CLI tools

```sh
xcode-select --install
```

The rest can be done in variable order, depending on how much you'd like to depend on Homebrew to manage other dependencies. I have yet to determine how I really feel on the matter :)

## Essentials

### Install Homebrew (`brew`)


`/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"`

### Install `pyenv` [^1]

`brew install pyenv`  
**OR**  
`curl https://pyenv.run | bash`

### Install `nvm`

Run the install script:[^2]  
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

### Install VSCode

To use the GUI installer:  
https://code.visualstudio.com/Download  

Download versions of the app directly:  
[Get latest Intel-chip version](https://update.code.visualstudio.com/latest/darwin/stable)  
or  
[Get latest Apple Silicon version](https://update.code.visualstudio.com/latest/darwin-arm64/stable)

## Nice to haves

If you want them all:  
`brew install --cask gimp rectangle maccy dbeaver-community`  

Or a-la-carte:  
`brew install --cask gimp`  
`brew install --cask rectangle`  
`brew install --cask maccy`  
`brew install --cask dbeaver-community`  

[^1]: If you use Homebrew to manage pyenv the versions available to pyenv are limited by the Homebrew update cycle

[^2]: Setting PROFILE in the call to installation script to avoid it automatically writing to shell config