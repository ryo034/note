# Macのセットアップ

## setup.sh

```
# ========== System setting ==========
# Finder:隠しファイル/フォルダを表示
defaults write com.apple.finder AppleShowAllFiles true
# Finder:拡張子を表示
defaults write NSGlobalDomain AppleShowAllExtensions -bool true
# クラッシュレポートを無効化する
defaults write com.apple.CrashReporter DialogType -string "none"
# リピート認識までの時間（最速）
defaults write -g InitialKeyRepeat -int 15
# キーのリピート（最速）
defaults write -g KeyRepeat -int 2

# install HomeBrew
if [ ! -x "`which brew`" ]; then
  /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
  brew update
fi

# install mas-cli
if [ ! -x "`which mas`" ]; then
  brew install mas
fi

# ========== Application Install ==========
mas install 803453959 # Slack
mas install 1216244845 # Gmail

# 3. homebrew-cask
brew cask install docker
brew cask install visual-studio-code
brew cask install google-chrome
brew cask install sequel-pro
brew cask install postman
brew cask install bettertouchtool

# ========== Docker Setup ==========
# https://codmon.kibe.la/notes/4599
mkdir -p Dev
cd

# ========== zshrc ==========
makeZshContent() {
	cat <<EOS > .zshrc
if type brew &>/dev/null; then
    FPATH=\$(brew --prefix)/share/zsh/site-functions:\$FPATH

    autoload -Uz compinit
    compinit
fi

autoload -U promptinit; promptinit
prompt pure

export PATH=\$HOME/.nodebrew/current/bin:\$PATH

# ----------------------
# Go Settings
# ----------------------

export GOENV_ROOT=\$HOME/.goenv
export PATH=\$GOENV_ROOT/bin:\$PATH
eval "\$(goenv init -)"
export PATH=\$GOROOT/bin:\$PATH
export GOPATH=\$HOME/go
export PATH=\$GOPATH/bin:\$PATH

export GO111MODULE=on

# ----------------------
# Common Aliases
# ----------------------

alias ll='ls -a'

# ----------------------
# Docker Aliases
# ----------------------

alias d='docker'
alias dc='docker-compose'
alias dcd='docker-compose up -d'
alias dcnt='docker container'
alias dcur='docker container ls -f status=running -l -q'
alias dexec='docker container exec -it \$(dcur)'
alias dimg='docker image'
alias drun='docker container run --rm -d'
alias drunit='docker container run --rm -it'
alias dstop='docker container stop \$(dcur)'

# ----------------------
# Git Aliases
# ----------------------
alias ga='git add'
alias gb='git branch'
alias gbd='git branch -d '
alias delete-merged-branch="!f () { git checkout \$1; git branch --merged|egrep -v '\*|develop|master'|xargs git branch -d; };f"
alias gc='git commit'
alias gcm='git commit -m'
alias gcmpre='github_add_prefix_to_commit_messages'
alias gco='git checkout'
alias gcob='git checkout -b'
alias gcom='git checkout master'
alias gd='git diff'
alias gda='git diff HEAD'
alias gl='git log'
alias gla='git log --graph --oneline --decorate=full -20 --date=short --format="%C(yellow)%h%C(reset) %C(magenta)[%ad]%C(reset)%C(auto)%d%C(reset) %s %C(cyan)@%an%C(reset)"'
alias glb='git log --graph --abbrev-commit --decorate=full -20 --date=short --format="%C(yellow)%h%C(reset) %C(magenta)[%ad]%C(reset)%C(auto)%d%C(reset) %s %C(cyan)@%an%C(reset)" --first-parent \$1'
alias glg='git log --graph --oneline --decorate --all'
alias glt=`git log --graph --pretty=format:'%x09%C(auto) %h %Cgreen %ar %Creset%x09by"%C(cyan ul)%an%Creset" %x09%C(auto)%s %d'`
alias gld='git log --pretty=format:"%h %ad %s" --date=short --all'
alias gm='git merge --no-ff'
alias gp='git pull'
alias gss='git status -s'
alias gst='git stash'
alias gstl='git stash list'
alias gstp='git stash pop'
alias gstd='git stash drop'
EOS
}

# .zshrc作成
if [ ! -e ".zshrc" ]; then
	touch .zshrc
	makeZshContent
  source ~/.zshrc
fi
```