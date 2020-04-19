# WSL configuring

## Updating the WSL 2 Linux kernel (on Windows)

<https://docs.microsoft.com/en-us/windows/wsl/wsl2-kernel>

## Set default WSL version 2 (on Windows)

```ps
wsl --set-default-version 2
```

## Install Ubuntu (on Windows)

[Ubuntu in Microsoft Store](https://www.microsoft.com/en-us/p/ubuntu/9nblggh4msv6)

## Install fonts (on Windows)

- [FiraCode NF](https://github.com/ryanoasis/nerd-fonts/releases/latest/download/FiraCode.zip) <sup>(download link)</sup>
- [MesloLGS NF](https://github.com/romkatv/powerlevel10k#meslo-nerd-font-patched-for-powerlevel10k)

## VS Code (on Windows)

### Set fonts

Add to: `setting.json`

```json
"editor.fontFamily": "'FiraCode NF'",
"editor.fontSize": 16,
"terminal.integrated.fontFamily": "'MesloLGS NF'",
"terminal.integrated.fontSize": 14,
```

### Install plugins

- [Remote - WSL](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-wsl)

## Update & Upgrade distribution (on Ubuntu)

```bash
sudo apt update && sudo apt upgrade
```

## Install [Zsh](https://github.com/zsh-users/zsh) (on Ubuntu)

```bash
sudo apt install zsh
zsh
```

## Set Zsh as default shell (on Ubuntu)

```zsh
chsh -s $(which zsh)
```

## Install [Zinit](https://github.com/zdharma/zinit) (on Ubuntu)

```zsh
sh -c "$(curl -fsSL https://raw.githubusercontent.com/zdharma/zinit/master/doc/install.sh)"
```

## Install [Powerlevel10k](https://github.com/romkatv/powerlevel10k) (on Ubuntu)

1. Add to `~/.zshrc`:

   ```zsh
   zinit ice depth=1; zinit light romkatv/powerlevel10k
   ```

2. Restart terminal

3. Configure theme:

   ```zsh
   p10k configure
   ```

   **_or_**

   1. Install theme from [dotfiles](https://www.atlassian.com/git/tutorials/dotfiles):

      ```zsh
      config checkout
      ```

   2. Add to `~/.zshrc`:

      ```zsh
      [[ ! -f ~/.p10k.zsh ]] || source ~/.p10k.zsh
      ```

## Install Zsh plugins (on Ubuntu)

### [Autosuggestions](https://github.com/zsh-users/zsh-autosuggestions)

Add to `~/.zshrc`:

```zsh
zinit ice wait lucid atload"!_zsh_autosuggest_start"
zinit light zsh-users/zsh-autosuggestions
```

### [Completions](https://github.com/zsh-users/zsh-completions)

Add to `~/.zshrc`:

```zsh
zinit ice wait lucid blockf
zinit light zsh-users/zsh-completions
```

### [nvm](https://github.com/lukechilds/zsh-nvm)

Add to `~/.zshrc`:

```zsh
zinit ice wait lucid
zinit light lukechilds/zsh-nvm
export NVM_SYMLINK_CURRENT="true" # nvm use should make a symlink
export NVM_DIR="$HOME/.nvm"
export NVM_LAZY_LOAD=true
```

### [LS_COLORS](https://github.com/trapd00r/LS_COLORS)

Add to `~/.zshrc`:

```zsh
zinit ice atclone"dircolors -b LS_COLORS > clrs.zsh" \
    atpull'%atclone' pick"clrs.zsh" nocompile'!' \
    atload'zstyle ":completion:*" list-colors “${(s.:.)LS_COLORS}”'
zinit light trapd00r/LS_COLORS
```

## Set aliases (on Ubuntu)

1. Add to `~/.zshrc`:

   ```zsh
   source $HOME/.zsh_aliases
   ```

2. Add to `~/.zsh_aliases` and `~/.bash_aliases`:

   ```zsh
   alias ls='ls --color=auto'
   alias la='ls -a --color=auto'
   alias ll='ls -l --color=auto'
   alias lla='ls -la --color=auto'
   ```

3. Restart terminal

## Install node.js (on Ubuntu)

```zsh
nvm install node
```

## Configure git

### Set user name and email address

1. Configure git (on Windows)

   ```ps
   git config --global user.name "User Name"
   git config --global user.email username@example.com
   ```

2. Configure git (on Ubuntu)

   ```zsh
   git config --global user.name "User Name"
   git config --global user.email username@example.com
   ```

### Sharing Git credentials between Windows and WSL

1. Configure the credential manager (on Windows)

   ```ps
   git config --global credential.helper wincred
   ```

2. Configure the credential manager (on Ubuntu)

   ```zsh
   git config --global credential.helper "/mnt/c/Program\ Files/Git/mingw64/libexec/git-core/git-credential-wincred.exe"
   ```
