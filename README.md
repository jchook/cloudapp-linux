# CloudApp for Linux

Unofficial [CloudApp](https://www.getcloudapp.com/) scripts for linux.

I use this software on a daily basis to quickly share files, screenshots, and screen recordings with friends, family, clients, or co-workers.


## Features

So far it does everything I need:

* Command-line upload to CloudApp
* Automatic upload to CloudApp when a screenshot or video is taken
* Copies share link to system clipboard


## Install

Installing is pretty straightforward.

1. Clone the repo (or download it)
2. Add the `cloudapp-linux/bin` directory to your `$PATH`.
3. Run `cloudapp` to configure your login and password.

For example:

```sh
git clone git@github.com:jchook/cloudapp-linux.git
sudo cp cloudapp-linux/bin/cloudapp* /usr/local/bin
cloudapp
```


### System Requirements

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


## Command-Line Upload

Once everything is installed, command-line upload is very easy:

```sh
cloudapp /path/to/file.png
```

It will automatically copy the share link to your clipboard and output the entire server response as pretty json.

You can use the special filename `-` to pass it via stdin:

```sh
cloudapp --name file.txt - < /path/to/file.txt
```


## Automatic Upload

You can set-up a directory watcher to automatically upload any newly created files:

```sh
cloudapp-watch ~/screenshots
```

I added this to my `~/.xsession` file to start it on login.

If watchers get stuck or you want to stop watching, this script will kill them:

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

Available configuration options:

```sh
# Required
CLOUDAPP_USERNAME=you@email.com
CLOUDAPP_PASSWORD=your-password

# What gets copied to the clipboard
CLOUDAPP_JQ_FILTER=.share_url

# Copy to clipboard + notify?
CLOUDAPP_NO_COPY=
CLOUDAPP_NO_NOTIFY=

# Where to save screenshots
SCREENSHOT_DIR="$HOME/screenshots"
SCREENSHOT_FILE_FORMAT="%Y-%m-%d-%H%M%S_\$wx\$h.png"
```


## License

MIT.