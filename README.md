# CloudApp for Linux

An unofficial cloudapp tool for linux.


## Features

These scripts do exactly what I need, and not a lot else:

* Command-line upload to CloudApp
* Automatic upload to CloudApp when a screenshot or video is taken
* Copies share link to system clipboard


## Install

Installing is pretty straightforward.

1. Clone the repo (or download it)
2. Add the `cloudapp-linux/bin` directory to your `$PATH`.
3. Configure your login and password

Here is what I would run:

```sh
git clone git@github.com:jchook/cloudapp-linux.git ~/.cloudapp-linux
echo 'your-cloudapp-password' > ~/.cloudapp-password
chmod 600 ~/.cloudapp-password
echo '
# CloudApp
PATH="$HOME/.cloudapp-linux/bin:$PATH"
CLOUDAPP_USERNAME=you@email.com
CLOUDAPP_PASSWORD=$(cat "$HOME/.cloudapp-password")' >> ~/.profile
```

## System Requirements

Make sure you have these programs installed:

* jq
* curl
* xclip, pbcopy, or clipboard

For auto-upload and screenshots, install:

* inotifywait
* scrot

On Debian-like systems this looks like:

```sh
sudo apt-get install jq curl xclip scrot inotify-tools
```


## Automatic Upload

You can set-up a directory watcher to automatically upload any newly created files:

```sh
cloudapp-watch ~/screenshots
```

I added this to my `~/.xsession` file to start it on login.

If watchers are stuck or you want to stop watching, this script will kill them:

```sh
cloudapp-unwatch
```


## Screenshots

I included 2 helper scripts for taking screenshots.

* `screenshot` - capture the entire screen as a png
* `select-screenshot` - capture only a portion of the screen


## Screen Record

For GIF and MP4 videos of your screen, I recommend using [peek](https://github.com/phw/peek). Simply save them to your `~/screenshots` folder (or similar) for auto-upload.

```sh
peek
```

## Configuration

Available configuration options are shown in `env.sample`:

```sh
# Required
CLOUDAPP_USERNAME=you@email.com
CLOUDAPP_PASSWORD=your-password

# What gets copied to the clipboard
JQ_FILTER=.share_url

# Where to save screenshots
SCREENSHOT_DIR="$HOME/screenshots"
SCREENSHOT_FILE_FORMAT="%Y-%m-%d-%H%M%S_\$wx\$h.png"
```


## License

MIT.