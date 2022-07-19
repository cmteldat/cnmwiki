---
tags: alias commands terminal
---

# Aliases
## Setup
Create the file `~/.bash_aliases` 
```bash
cd ~
touch .bash_aliases
```

**Note**: This `.bash_aliases` should be already referenced in `~/.bashrc`
**Important**: The reference must be placed **after** the [[Environment variables|environment variables]] in order to work properly.
```bash
if [ -f ~/.bash_aliases ]; then
    . ~/.bash_aliases
fi
```

## Add alias
Edit the `.bash_aliases` with the aliases that you want. For example:
```bash
alias clip="xclip -selection c" # copy to clipboard
alias 2repos="cd $TELDAT_REPOS_HOME"
```

## Commands
```bash
# View aliases
alias
```