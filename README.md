# IntroToGitHub
This a test repository. 
# ============================================
# 🧠 Modern Arch Bash Setup
# Features: ble.sh + starship + fzf + eza
# ============================================

# ---- 1. History Tweaks ----
HISTSIZE=10000
HISTFILESIZE=20000
HISTCONTROL=ignoredups:erasedups
HISTTIMEFORMAT="%F %T "
shopt -s histappend
PROMPT_COMMAND="history -a; history -n; $PROMPT_COMMAND"

# ---- 2. Aliases ----
# Use eza instead of ls
alias ls='eza --icons --group-directories-first --color=always'
alias ll='eza -lh --icons --group-directories-first --git'
alias la='eza -lha --icons --group-directories-first --git'
alias lt='eza --tree --level=2 --icons'

# Handy utilities
alias grep='grep --color=auto'
alias h='history | grep'
alias ..='cd ..'
alias ...='cd ../..'
alias cls='clear && printf "\e[3J"'   # full screen clear
alias please='sudo $(history -p \!\!)' # rerun last command as sudo
alias mkcd='mkdir -p "$1" && cd "$1"'

# ---- 3. Bash Completion ----
if [ -f /usr/share/bash-completion/bash_completion ]; then
  . /usr/share/bash-completion/bash_completion
fi

# ---- 4. FZF (fuzzy finder) ----
if [ -f /usr/share/fzf/key-bindings.bash ]; then
  source /usr/share/fzf/key-bindings.bash
  source /usr/share/fzf/completion.bash
fi

# ---- 5. Starship Prompt ----
eval "$(starship init bash)"

# ---- 6. ble.sh (syntax highlight, autosuggest, completion) ----
if [[ $- == *i* ]]; then
  [[ -f /usr/share/blesh/ble.sh ]] && source /usr/share/blesh/ble.sh --attach=none
fi

# ---- 7. Welcome message ----
if [[ $- == *i* ]]; then
  echo -e "\e[1;32mWelcome back, $(whoami)! 🐧 Arch + Bash + eza + ble.sh ready.\e[0m"
fi
