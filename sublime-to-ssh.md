# How to use Sublime Text via SSH

## [Preparation on your computer](https://martin-thoma.com/how-to-use-sublime-text-via-ssh/#preparation-on-your-computer)

1. Install and start Sublime Text.
2. Install the `rsub` package via Package Controll.
3. Open `~/.ssh/config`. Create it if id does not exist yet. Add the code from below.
4. Start SSH with `ssh myname`.

This is how the `config` file should look like:

```
Host myname
  Hostname pc123.your.network.com
  RemoteForward 52698 127.0.0.1:52698
```

You can add more information like `User yourusername` to this file.

## Server-Side steps[ ¶](https://martin-thoma.com/how-to-use-sublime-text-via-ssh/#server-side-steps)

1. Download the `rmate` script:
   `curl https://raw.githubusercontent.com/aurora/rmate/master/rmate > rmate`
2. Execute `./rmate yourfile`. It will open in your local Sublime Text!

## Improvements[ ¶](https://martin-thoma.com/how-to-use-sublime-text-via-ssh/#improvements)

These steps have to be done server-side.

### With Root access[ ¶](https://martin-thoma.com/how-to-use-sublime-text-via-ssh/#with-root-access)

It's not so nice to open files with `~/rmate filename` all the time. You can use `rmate filename` after executing this command:

```
# This creates a symlink
sudo ln -s ~/rmate /usr/local/bin/
```

You can use other paths than `/usr/local/bin/`. Look at your `PATH` for candidates:

```
echo $PATH
```

### Without Root access[ ¶](https://martin-thoma.com/how-to-use-sublime-text-via-ssh/#without-root-access)

When you don't have root access, you can't create a symlink for most (eventually even all) folders in your `PATH`. But you can expand your `PATH`:

```
mkdir -p ~/bin        # create folder if it doesn't exist
ln -s ~/rmate ~/bin/  # create symlink
```

Now expand your `PATH` so that it includes `~/bin`. There are at least two ways to do so:

- You can directly edit your shells `.rc` file (e. g. `.bashrc`, `.zshrc`, `.cshrc`, ...) or
- you can edit your `.profile`

As many shells source `.profile` I'll explain this way. First, open `~/.profile`. Then add

```
# First check if that folder exists
if [ -d "$HOME/bin" ] ; then
    # Add your home folder to the end of the current path
    PATH="$PATH:$HOME/bin"
fi
```
***

Refs:
https://martin-thoma.com/how-to-use-sublime-text-via-ssh

https://raw.githubusercontent.com/aurora/rmate/master/rmate
