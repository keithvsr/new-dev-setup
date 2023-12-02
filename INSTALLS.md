# Installation basics to get up and running developing on a new Mac

Once we've created a `.zshrc` file in the user's local directory (if it doesn't exist already, starting from the included `.zshrc_prepends` file is easy) it's time to install useful bits of software.

First we install the Xcode CLI tools

```sh
xcode-select --install
```

**OR**
Install XCode from [the App Store](https://apps.apple.com/us/app/xcode/id497799835)

(Optional) Set up a directory to store your zsh completions for tab-completion help using certain cli tools:

```sh
mkdir -p ~/.zsh/completion
```

And add the following to your `.zshrc` file to enable them:

```sh
# zsh completions
fpath=(~/.zsh/completion $fpath)
autoload -U compinit
compinit
```

The rest can be done in variable order, depending on how much you'd like to depend on Homebrew to manage other dependencies. I have yet to determine how I really feel about that :)

## Essentials

### Install [Homebrew](https://brew.sh) (aka `brew`)

The all-around solid dependency manager. Can aid in further installations below.

```sh
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

Once installed, link its zsh completions in the directory we set up before:

```sh
ln -s /opt/homebrew/share/zsh/site-functions/_brew ~/.zsh/completion/_brew
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

Likely either way we'll need to make sure `pyenv` loads into our shell as well. Commands from [the `pyenv` installation docs](https://github.com/pyenv/pyenv#advanced-configuration) are as follows:

```sh
echo 'export PYENV_ROOT="$HOME/.pyenv"' >> ~/.zshrc
echo '[[ -d $PYENV_ROOT/bin ]] && export PATH="$PYENV_ROOT/bin:$PATH"' >> ~/.zshrc
echo 'eval "$(pyenv init -)"' >> ~/.zshrc
```

Prior to installation of a python version using `pyenv` it's recommended to install python build dependencies with homebrew. Docs with further info can be found [here](https://github.com/pyenv/pyenv/wiki#suggested-build-environment) but the gist is:

```sh
brew install openssl readline sqlite3 xz zlib tcl-tk
```

Once you've installed a python version, don't forget (like I did recently 🤪) to activate it. Let's say you've installed a version of Python 3.11:

```sh
pyenv global 3.11
```

### Install [`nvm`](https://nvm.sh)

Node version management via the command line that _might_ be worth the effort
Run the install script:[^nvm-shell-note]

```sh
PROFILE=/dev/null bash -c 'curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.5/install.sh | bash'
```

NVM can be _slow_ on shell startup so we customize the shell integration to lazy-load all its associated commands. Add the following to .zshrc:

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

And link the zsh completions that come with the Docker app into the directory we set up earlier:

```sh
ln -s /Applications/Docker.app/Contents/Resources/etc/docker.zsh-completion ~/.zsh/completion/_docker
```

**OR**
it's also available on `brew` (may require additional dependencies - not really recommended):

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

### Install [Poetry](https://python-poetry.org/)

An environment and dependency manager for Python development, it has its drawbacks and annoyances but is a decent replacement for a bunch of manual `venv` and `requirements.txt` management.

Make sure a good version of Python is activated using `pyenv` and then run the installer script:

```sh
curl -sSL https://install.python-poetry.org | python3 -
```

Add the following to your `.zshrc` to add Poetry to your path:

```sh
# poetry
export PATH="$HOME/.local/bin:$PATH"
```

Once done (and `poetry --version` works), recommendation is to change the default virtual environment behavior to store each project's `venv` within the project directory. This can be done by changing a poetry configuration setting:

```sh
poetry config virtualenvs.in-project true
```

And finally, add the zsh completions for tab completion:

```sh
poetry completions zsh > ~/.zsh/completion/_poetry
```

### Install mysql (server+client or just client)

Docker has become the go-to for firing up a database server locally, so the recommendation is to install the client only unless you need to have the full server package for some reason:

```sh
brew install mysql-client
```

For the server as well:

```sh
brew install mysql
```

## Nice to haves

There are tons of available packages on homebrew worth checking out. Below's a small selection of what's been useful in the past. These include a database connection GUI (dbeaver), a real image processor (gimp), a solid clipboard manager (maccy), and a decent Mac OS window management system (rectangle):

If you want the go-to ones:

```sh
brew install --cask rectangle maccy dbeaver-community
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
