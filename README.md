# WSL configuring

## Install fonts (in Windows)

- [FiraCode NF](https://github.com/ryanoasis/nerd-fonts/releases/latest/download/FiraCode.zip) <sup>(download link)</sup>
- [MesloLGS NF](https://github.com/romkatv/powerlevel10k#meslo-nerd-font-patched-for-powerlevel10k)

## VS Code (in Windows)

### Set fonts

**Add to**: `setting.json`

```json
"editor.fontFamily": "'FiraCode NF'",
"editor.fontSize": 16,
"terminal.integrated.fontFamily": "'MesloLGS NF'",
"terminal.integrated.fontSize": 14,
```

### Install plugins

- [Remote - WSL](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-wsl)

## Install [Zsh](https://github.com/zsh-users/zsh)

```bash
sudo apt install zsh
```

## Install [Zinit](https://github.com/zdharma/zinit)

```zsh
sh -c "$(curl -fsSL https://raw.githubusercontent.com/zdharma/zinit/master/doc/install.sh)"
```

## Install Zsh theme

### [Powerlevel10k](https://github.com/romkatv/powerlevel10k)

**Add to** `~/.zshrc`:

```zsh
zinit ice depth=1; zinit light romkatv/powerlevel10k
```

**Configure theme**:

```zsh
p10k configure
```

**_or_**

**Install theme from [dotfiles](https://www.atlassian.com/git/tutorials/dotfiles)**:

```zsh
config checkout
```

## Install Zsh plugins

### [Autosuggestions](https://github.com/zsh-users/zsh-autosuggestions), [Highlighting](https://github.com/zdharma/fast-syntax-highlighting), [Completions](https://github.com/zsh-users/zsh-completions)

**Add to** `~/.zshrc`:

```zsh
zinit wait lucid for \
 atinit"ZINIT[COMPINIT_OPTS]=-C; zicompinit; zicdreplay" \
    zdharma/fast-syntax-highlighting \
 blockf \
    zsh-users/zsh-completions \
 atload"!_zsh_autosuggest_start" \
    zsh-users/zsh-autosuggestions
```

### [nvm](https://github.com/lukechilds/zsh-nvm)

**Add to** `~/.zshrc`:

```zsh
zinit ice wait lucid
zinit light lukechilds/zsh-nvm
export NVM_SYMLINK_CURRENT="true" # nvm use should make a symlink
export NVM_DIR="$HOME/.nvm"
export NVM_LAZY_LOAD=true
```

### [LS_COLORS](https://github.com/trapd00r/LS_COLORS)

**Add to** `~/.zshrc`:

```zsh
zinit ice atclone"dircolors -b LS_COLORS > clrs.zsh" \
    atpull'%atclone' pick"clrs.zsh" nocompile'!' \
    atload'zstyle ":completion:*" list-colors “${(s.:.)LS_COLORS}”'
zinit light trapd00r/LS_COLORS
```

## Set aliases

**Add to** `~/.zshrc`:

```zsh
source $HOME/.aliases
```

**Add to** `~/.bashrc`:

```bash
if [ -f ~/.aliases ]; then
    . ~/.aliases
fi
```

**Add to** `~/.aliases`:

```zsh
alias ls='ls --color=auto'
alias la='ls -a --color=auto'
alias ll='ls -l --color=auto'
alias lla='ls -la --color=auto'
```

## Install node.js (via nvm)

```zsh
nvm install node
```
