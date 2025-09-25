# Pimp My Terminal (Fall 2025)
> [!IMPORTANT] 
> There are a few pieces of software you should have installed and set up in order to follow along. Namely:
> - Git
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
- `<Leader> ,` (rename current window)
- `<Leader> !` (move current pane to its own window)

See the [https://tmuxcheatsheet.com/](tmux cheatsheet) for other commands.

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


