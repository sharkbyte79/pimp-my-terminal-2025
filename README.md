# Pimp My Terminal (Fall 2025)
> [!IMPORTANT] 
> There are a few pieces of software you should have installed and set up in order to follow along. Namely:
> - Git
> - Zsh (Default on MacOS and _some_ Linux distributions)
>   - If Zsh is not already your default, run `chsh -s /bin/zsh` after installation to set it as your default
> - [Homebrew](https://brew.sh/) (MacOS)

## Color Schemes
For rolling your own color scheme, see [terminal.sexy](https://terminal.sexy/). Be sure to export your creation to the right format for your choice of terminal emulator!

If you'd rather have this handled automatically, [Gogh](https://gogh-co.github.io/Gogh/) provides an easy CLI interface for selecting colorschemes. Try it with the following command:
```shell
# MacOS
bash -c  "$(curl -sLo- https://git.io/vQgMr)"

# Linux
bash -c  "$(wget -qO- https://git.io/vQgMr)"
```

## Oh My Zsh
To install [Oh My Zsh](https://ohmyz.sh/), you should run one of the appropriate commands and follow the on-screen instructions.

```shell
# via curl
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"

# via wget
sh -c "$(wget https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh -O -)"
```

If prompted to replace an existing Zsh configuration (`.zshrc`), agree to do so.

### Installing plugins for Oh My Zsh
To install external plugins for Zsh, you should follow the instructions on their GitHub pages.

For the plugins we recommend for starting out, run the following:

```shell
# zsh-autosuggestions
git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions

# zsh-autocomplete
git clone --depth 1 -- https://github.com/marlonrichert/zsh-autocomplete.git $ZSH_CUSTOM/plugins/zsh-autocomplete
```

Next, find the following line in your new `.zshrc` file:
```shell
plugins = (git)
```

And change it to the following
```shell
plugins=(git zsh-autosuggestions zsh-autocomplete)
```

Restart the terminal or reload your configuration with `source ~/.zshrc` to see the changes.

## Starship
To install the [Starship](https://starship.rs/) prompt, run the following command and follow any instructions that may appear:
```shell
curl -sS https://starship.rs/install.sh | sh
```
The prompt is _highly customizable_, try modifying the it's configuration in `~/.config/starship/`! See their documentation for a comprehensive look at the options.

### Using Starship with Oh My Zsh
To use Starship on top of Oh my Zsh, make the following changes to your `.zshrc`:

```shell
# BEFORE
ZSH-THEME="some-theme" 

# AFTER
ZSH-THEME="" 
```
And add this string to the **bottom** of `.zshrc`:
```shell
eval "$(starship init zsh)"
```

Restart the terminal or reload your shell configuration with `source ~/.zshrc` to see the changes.

## tmux
tmux should be _easily_ installable via your package manager.
- Run `brew install tmux` for MacOS
- Whatever package manager applies for your Linux distribution
    - `sudo apt install tmux` for Debian, Ubuntu, Mint, PopOS
    - `sudo dnf install tmux` for Fedora and it's derivatives 
    - `sudo pacman -y tmux` for Arch Linux and Manjaro

A sample tmux configuration (`.tmux.conf`) is included in this repository, set up with some sane defaults. Leave this file in your home directory `/home/user/`.

### Using tmux
tmux uses a **leader key** system, where commands issued for controlling tmux should be prefaced by the leader key (that is, press the leader key, _then_ the key for your desired command. Don't press them simultaneously). 

The default leader is `<Ctrl>-b`. For an easier reach across the keyboard, the sample config rebinds this to `<Ctrl>-a`.

Other important binds to remember:
- `<Leader> c` (new window)
- `<Leader> -` (horizontal split pane)
- `<Leader> |` (vertical split pane)
- `<Leader> <Num>` (jump to window #<Num>)
- `<Leader> <(Up/Down/Left/Right)-Arrow>` (navigate to pane in some direction)
- `<Leader> r` (reload tmux configuration)
- `<Leader> ,` (rename current window)
- `<Leader> !` (move current pane to its own window)

See the [tmux cheatsheet](https://tmuxcheatsheet.com/) for other commands.

### tmux Plugin Manager
The sample configuration relies on **TPM**.

Run the following command to install the plugin manager.
```shell
git clone https://github.com/tmux-plugins/tpm ~/.tmux/plugins/tpm
```

These plugins are included to enhance tmux's out-of-the-box functionality:
- `tmux-resurrect`: allows tmux sessions to persist between system restarts
- `tmux-continuum`: continuous saving of your tmux session, optional automatic restoration
    - Add the following to your `.tmux.conf` file to enable this automatic session restoration: `set -g @continuum-restore 'on'`

Upon opening tmux with `tmux`, you may need to press `<Leader> I` to fetch and install the new plugins.
