- Install the following: 
	- Firefox (+ adBlock Plus)
		- Bookmark import and export: https://support.mozilla.org/en-US/kb/export-bookmarks-safari
	- iTerm2
	- Obsidian
	- Slack
	- Sublime text
	- VS Code
		- Extensions:
			- Python Indent
			- Python Extension Pack
			- Docker


### Install Homebrew
- Refer official website: https://brew.sh/
```shell
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```
- If asked for password, use the system password.
- It installs Git also

### Install `oh-my-zsh`
- Refer official website: https://ohmyz.sh/#install
```shell
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```

Run the following to update and get the latest features in oh-my-zsh
```bash
upgrade_oh_my_zsh
```
or 
```
$ omz update
```
#### Updating the theme
Better option: https://github.com/romkatv/powerlevel10k#homebrew
- Install the new theme (`powerlevel9k` here)
```bash
$ git clone https://github.com/bhilburn/powerlevel9k.git ~/.oh-my-zsh/custom/themes/powerlevel9k
```
- Open `~/.zshrc` 
- Navigate to `ZSH_THEME` variable and change it to following:
```bash
ZSH_THEME="powerlevel9k/powerlevel9k"
```
- `source ~/.zshrc`
- Navigate to `iTerm2 > Settings > Profiles > Colors`
- Install fonts: 
```bash
git clone https://github.com/powerline/fonts.git
```
`cd fonts/`
`./install.sh`
- To change the font, navigate to `iTerm2 > Preferences > Profiles > Text > Change Font`

#### Plugins

##### 0. Create general alias
```
alias ..="cd .."
alias ...="cd ../.."
alias c="clear"
```

##### 1. `zsh-syntax-highlighting` 
- Run the following to download plugin
```bash
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting
```
- open `~/.zshrc`
- navigate to `plugins`. Add the following
```
plugins=(
git
zsh-syntax-highlighting
)
```

##### 2. Autosuggestion
```bash
git clone https://github.com/zsh-users/zsh-autosuggestions $ZSH_CUSTOM/plugins/zsh-autosuggestions
```
- add `zsh-autosuggestions` to `plugins`

### Install `awscli`
Follow for official document: https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html
```bash
curl "https://awscli.amazonaws.com/AWSCLIV2.pkg" -o "AWSCLIV2.pkg"
sudo installer -pkg AWSCLIV2.pkg -target /
```

### Install `kubectl`
Follow the docs: https://kubernetes.io/docs/tasks/tools/install-kubectl-macos/
```bash
brew install kubectl
```

### Install `wget` and `jq`
```
brew install wget
```

`jq` is required in `~/.zshrc` file (during `mfb`), thus installation is required.
```bash
$ wget https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh

$ chmod u+x install.sh
$ ./install.sh
```
Once the installation is over, you can now close the terminal and start it again, followed by this below command which will install `jq` in your MacOS machine:
```
$ brew install jq
```

### Generate SSH keys and attach to Gitlab
Follow this: https://docs.tritondatacenter.com/public-cloud/getting-started/ssh-keys/generating-an-ssh-key-manually/manually-generating-your-ssh-key-in-mac-os-x
```
ssh-keygen -t rsa
```

```ad-warning
Never share your private key with anyone!
```

Your public key is saved to the `id_rsa.pub`;file and is the key you upload to your AWS Service account. You can save this key to the clipboard by running this:
```
pbcopy < ~/.ssh/id_rsa.pub
```

### Install python
https://www.python.org/downloads/macos/

- It seems like after Monterey OS in Mac, default Python2 has been removed.
- Once the Pyton installation is done, go to `~/.zshrc` and create an alias for python as follows.
`alias python="python3"` 

