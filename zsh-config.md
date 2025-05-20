# Set name of the theme to load --- if set to "random", it will
# load a random theme each time Oh My Zsh is loaded, in which case,
# to know which specific one was loaded, run: echo $RANDOM_THEME
# See https://github.com/ohmyzsh/ohmyzsh/wiki/Themes
ZSH_THEME="gnzh"

# Example aliases
alias zshconfig="nano ~/.zshrc"
alias ohmyzsh="nano ~/.oh-my-zsh"
# alias kubectl="minikube kubectl"

# docker aliases
alias gs="git status"
alias ga="git add ."
alias gc="git commit -m"
alias gco="git checkout"
alias gb="git branch"
alias gl="git log --oneline --graph --all"
alias gp="git push origin"
alias gpo="git push origin HEAD"
alias gd="git diff"

# git aliases
alias gs="git status"
alias ga="git add ."
alias gc="git commit -m"
alias gco="git checkout"
alias gb="git branch"
alias gl="git log --oneline --graph --all"
alias gp="git push origin"
alias gpo="git push origin HEAD"
alias gd="git diff"

# kubernetes aliases
alias k="kubectl"
alias kaf="kubectl apply -f"
alias kgp="kubectl get pods"
alias kgs="kubectl get svc"
alias kga="kubectl get all"
alias kdp="kubectl describe pod"
alias kl="kubectl logs"
alias kctx="kubectl config use-context"
alias kns="kubectl config set-context --current --namespace"

# navegation aliases
alias ..="cd .."
alias ...="cd ../.."
alias ll="ls -alF"
alias la="ls -A"
alias l="ls -CF"
alias c="clear"
alias h="history"

# system
alias update="sudo apt update && sudo apt upgrade"
alias please="sudo"
alias grep="grep --color=auto"
alias serve="python3 -m http.server"
alias .-="xdg-open ."
source /usr/share/zsh-syntax-highlighting/zsh-syntax-highlighting.zsh
#PS1="%F{green}%n%f %F{yellow}%1~%f➜  "

# others
alias pbcopy='xclip -sel clip'
alias pbpaste='xclip -sel clip -o'
alias sshconf='cat ~/.ssh/config'
alias myip4='curl -4 ifconfig.me'