# new-computer installation/backup

My personal installations for my computer.

Read the script and install with caution.

## Install from script:

Open the terminal, then:

```sh
bash -c "`curl -L https://git.io/JX5lw`"
```

This command runs the following script:

```shell
#                    _           _        _ _ 
#  ___  _____  __   (_)_ __  ___| |_ __ _| | |
# / _ \/ __\ \/ /   | | '_ \/ __| __/ _` | | |
#| (_) \__ \>  <    | | | | \__ \ || (_| | | |
# \___/|___/_/\_\   |_|_| |_|___/\__\__,_|_|_|

echo "Mac OS Install Setup Script"
echo "By Jeff Brausam"

# Colorize the terminal for install

# Set the colours you can use
black=$(tput setaf 0)
red=$(tput setaf 1)
green=$(tput setaf 2)
yellow=$(tput setaf 3)
blue=$(tput setaf 4)
magenta=$(tput setaf 5)
cyan=$(tput setaf 6)
white=$(tput setaf 7)

# Resets the style
reset=`tput sgr0`

# Color-echo. Improved. [Thanks @joaocunha]
# arg $1 = message
# arg $2 = Color
cecho() {
  echo "${2}${1}${reset}"
  return
}

echo ""
cecho "###############################################" $red
cecho "#        DO NOT RUN THIS SCRIPT BLINDLY       #" $red
cecho "#         YOU'LL PROBABLY REGRET IT...        #" $red
cecho "#                                             #" $red
cecho "#              READ IT THOROUGHLY             #" $red
cecho "#         AND EDIT TO SUIT YOUR NEEDS         #" $red
cecho "###############################################" $red
echo ""

# Set continue to false by default.
CONTINUE=false

echo ""
cecho "Have you read through the script you're about to run and " $red
cecho "understood that it will make changes to your computer? (y/n)" $red
read -r response
if [[ $response =~ ^([yY][eE][sS]|[yY])$ ]]; then
  CONTINUE=true
fi

if ! $CONTINUE; then
  # Check if we're continuing and output a message if not
  cecho "Please go read the script, it only takes a few minutes" $red
  exit
fi

##############################
# Prerequisite: Install Brew #
##############################

echo "Installing brew..."

if test ! $(which brew)
then
	## Don't prompt for confirmation when installing homebrew
  /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)" < /dev/null
fi

# Latest brew, install brew cask
brew upgrade
brew update
brew tap caskroom/cask

##############################
# Install via Brew           #
##############################

echo "Starting brew app install..."

# Developer Tools
brew cask install dash
brew install ispell


### Development
brew cask install docker
brew cask install insomnia
brew cask install sourcetree
brew tap mongodb/brew # install mongodb
brew install mongodb-community@5.0 # update in future if needed
brew services start mongodb-community@5.0 # mongodb runs as a background service

### Command line tools - install new ones, update others to latest version
brew install git  # upgrade to latest
brew install git-lfs # track large files in git https://github.com/git-lfs/git-lfs
brew install wget
brew install httpie
brew install zsh # zshell
brew install tmux
brew install tree
brew link curl --force
brew install grep --with-default-names
brew install trash  # move to osx trash instead of rm
brew install less
brew install yarn
brew cask install multipass

### Python
brew install python
brew install pyenv

### Dev Editors 
brew cask install visual-studio-code

### Productivity
brew cask install google-chrome
brew cask install alfred
brew cask install dropbox

### Chat / Video Conference
brew cask install slack
brew cask install discord
brew cask install zoomus

## Audio / Music
brew cask install ableton-live-suite

## Others
brew install ffmpeg
brew install youtube-dl

### Run Brew Cleanup
brew cleanup

#############################################
### Installs from Mac App Store
#############################################

### find app ids with: mas search "app name"
brew install mas

### Mas login is currently broken on mojave. See:
### Login manually for now.
cecho "Need to log in to App Store manually to install apps with mas...." $red
echo "Opening App Store. Please login."
open "/Applications/App Store.app"
echo "Is app store login complete.(y/n)? "
read response
if [ "$response" != "${response#[Yy]}" ]
then
	mas install 1319778037 # Istat Menu
else
	cecho "App Store login not complete. Skipping installing App Store Apps" $red
fi

#############################################
### Install few global python packages
#############################################

echo "Installing global Python packages..."

pip3 install --upgrade pip

#############################################
### Applications outside of brew
#############################################
# Node - install nvm (node version mananger) here https://github.com/nvm-sh/nvm
# Current ZSH theme - https://github.com/romkatv/powerlevel10k/
# SeratoDJ - https://serato.com/dj/pro


echo ""
cecho "Done!" $cyan
echo ""
echo ""
cecho "################################################################################" $white
```
