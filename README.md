# ytpl

A small and portable shell based tool to extract metadata from youtube playlists.
I used to save my playlists using my google account, but videos were randomly deleted all the time and the youtube interface doesn't show which videos were deleted. So I made this little tool to easily extract playlists metadata into parsable formats like csv or tsv. It's possible to open the output in a spreadsheet or any other compatible software.
I also added support for tags. This is useful to work with multiple playlists and it makes this script better integrated with my other tool [cli-bookmarker](http://github.com/paulobtn/cli-bookmarker).

## Features

* Extract youtube playlists into a csv file
* select the fields and format the output in any order
* Use any separator you want

## Install

put the bm file somewhere you can run it:
```bash
([ -d "$HOME/.local/bin" ] || mkdir -p "$HOME/.local/bin") && \
curl -sSL https://raw.githubusercontent.com/paulobtn/ytpl/main/ytpl -o "$HOME/.local/bin/ytpl" && \
sudo chmod +x "$HOME/.local/bin/ytpl"
```
to launch as "ytpl" you need to add $HOME/.local/bin to your path
```bash
export PATH="$HOME/.local/bin:$PATH"
```

### Dependencies

* [youtube-dl](https://github.com/ytdl-org/youtube-dl) to fetch the metadata in json format
* [jq](https://github.com/stedolan/jq) to parse the json data

## Usage

```bash
ytpl [playlist-url] [options...]
```

## Formatting

ytpl can create tables with 4 types of data:

* title
* uploader
* url
* tags

You can send a formatting string with the option -f to determine which data and
which order you want to print them.

## Examples

to display a table separated by tabs with the data: \[url, uploader, title\]
```bash
ytpl <playlist-url>
```

to display a table separated by commas with the data: \[url, title\]
```bash
ytpl <playlist-url> -s "," -f "url title"
```

to display a table separated by tabs with the data \[title, url\] and add a column with tags
```bash
ytpl <playlist-url> -f "title url tags" -t "linux programming"
```

to save playlists in a format accepted by [cli-bookmarker](http://github.com/paulobtn/cli-bookmarker)
```bash
ytpl <playlist-1-url> -f "title tags url" -t "playlist-1-name youtube linux" >> bookmarks && \
ytpl <playlist-2-url> -f "title tags url" -t "playlist-2-name youtube music" >> bookmarks
```

## License
License GPLv3<br>
This is free software: you are free to change and redistribute it.<br>
Written by Paulo Neto
