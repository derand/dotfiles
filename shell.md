File `.profile`

```
export LC_ALL=en_US.UTF-8
export LANG=en_US.UTF-8

[[ -s ~/.bashrc ]] && source ~/.bashrc
```

File `.bashrc`

```
export "PS1=\[\033[01;34m\]\D{%H:%M}\[\033[00m\]  \[\033[36m\]\u@\[\033[0;33m\]\h:\[\033[0;32m\]\w\[\033[0;37m\]\$ "

### improve history
export HISTCONTROL=ignoreboth
export HISTSIZE=9999
```

Search and delete

    find ./ -name ".svn" -exec echo -n '"{}" ' \; | xargs rm -Rf
    find . -name "*.DS_Store" -type f -delete

Search *.html files and replace text "®" to "&#174;" 

    (find . -name *html) | xargs sed -i "s/®/\&#174;/g"

Group rename files format "Изображение 123.jpg" to "img_123.jpg"

    find ./backup/photo -name '*[0-9][0-9][0-9].jpg' -exec bash -c 'mv "$0" "${0/Изображение /img_}"' {} \;

Find and change file encoding

    find . -type f -name "*.hh" -exec bash -c 'iconv -f KOI8-R -t UTF-8 "{}" > ~/Desktop/x.hh; mv ~/Desktop/x.hh "{}"' \;

    for f in `find . | xargs file | grep "ISO-8859" | cut -f 1 -d ":" | xargs`; do echo $f; iconv -f KOI8-R -t UTF-8 "$f" > ~/Desktop/file.tmp.hh && mv ~/Desktop/file.tmp "$f"; done

Get difference between ntp server and local time

    ntpdate -q pool.ntp.org

Show current connections

    lsof -i | grep -E "(ESTABLISHED|LISTEN)"

Run and auto-rerun command

    watch -n 5 "lsof -i | grep -E '(ESTABLISHED|LISTEN)'"

Resize image(s)

    sips -Z 1024 *.jpg

SSH over http-proxy

    ssh user@final_dest -o "ProxyCommand=nc -X connect -x proxyhost:proxyport %h %p"

Purge memory (linux, os x)

    sudo sh -c "free -h && sync && echo 3 > /proc/sys/vm/drop_caches && free -h"
    sudo purge

Remove EXIF from image

    convert <input file> -strip <output file>

Randomly play files from directory (OS X)

    while :; do fn=`find ~/dump/music/ -name *.mp3 | python -c "import sys; import random; print(random.choice(sys.stdin.readlines()).rstrip())"`; echo $fn; afplay -v 0.35 "$fn"; done

Print first and last line of file

    sed -e 1b -e '$!d' <text file>


### Apt

List packege versions on server enabled to download

    apt-cache madison python3

Install specified version of packege

    apt-get install python3=3.4.2-2
