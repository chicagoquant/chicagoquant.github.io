
# Command line
### Zoxide
```text
zoxide query -a -l -s
```

### Start VM
```
"c:\Program Files\Oracle\VirtualBox\VBoxManage" startvm jammy-ubuntu --type headless
```

### Export GIT repository
```
git daemon --reuseaddr --informative-errors --verbose --export-all --enable=receive-pack --base-path=C:\repos

> git clone git://localhost/dotfiles
```

### Readonly GIT repository
```
git daemon --reuseaddr --informative-errors --verbose --export-all --base-path=C:\repos
```

### MinTTY Terminal Bash
```
vendor\git-for-windows\usr\bin\bash --login -i
vendor\git-for-windows\usr\bin\mintty /bin/bash -l

PowerShell -ExecutionPolicy Bypass -NoLogo -NoProfile -NoExit -Command "Invoke-Expression 'Import-Module ''vendor\profile.ps1'''"
```

### Veracrypt
```
veracrypt /volume filename /letter t /password "password" /hash sha512 /wipecache /cache n /quit /silent
veracrypt /v filename /l t /p "password" /hash sha512 /w /c n /q /s

veracrypt /dismount /letter t /force /quit
veracrypt /d /l t /f /q

# https://www.veracrypt.fr/en/Command%20Line%20Usage.html
```

### Music download
```
mpv playlist.m3u

yt-dlp -x url -o "blah.ogg"             # extract-audio
yt-dlp --extract-audio --audio-quality 0 --audio-format opus url
# other useful flags: --no-mtime -o "%(title)s.%(ext)s"
# audio formats: best aac, alac, flac, m4a, mp3, opus, vorbis, wav
# audio quality: 0 (best), 10 (worst)
# https://github.com/yt-dlp/yt-dlp
```
