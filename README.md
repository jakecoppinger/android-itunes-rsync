Android iTunes rsync
====================

>   Automatically export m3u playlists from iTunes on your Mac,
>   synchronize (rsync) playlists and all your music to your Android phone

# How this works
- Exports m3u playlist files from iTunes using the incredible command line utility [iTunesExportScala](http://www.ericdaugherty.com/dev/itunesexport/)  by Eric Daugherty, also available on the [Mac App Store](https://itunes.apple.com/us/app/playlist-export/id434426826?mt=12&ls=1).

- Renames m3u playlist paths so that they are relative (iTunes uses absolute paths)

- [SSHelper](https://arachnoid.com/android/SSHelper/) allows you to SSH to an Android device without root, free on the [Play Store](https://play.google.com/store/apps/details?id=com.arachnoid.sshelper)

- rsyncs the playlists and music to your Android device over wifi

- Notice this is **one way synchronization** and won't update your iTunes playlists/library

# Getting started

This is very new and probably buggy, so make sure you have a backup of your iTunes library just in case!

1. Backup your iTunes Library and media!

2. Install [SSHelper](https://arachnoid.com/android/SSHelper/) ([Play Store](https://play.google.com/store/apps/details?id=com.arachnoid.sshelper)) on your Android device.

3. Follow the [SSHelper setup](https://arachnoid.com/android/SSHelper/#The_basics) setup, make sure to setup **Public-key (passwordless) logins** and copy the public key to your Mac.

4. Add your Android device to your SSH config file with the name `phone` (if you want to use a different host name just change it in the script). Mine looks like this:

```
Host phone 
Hostname 192.168.0.3
Port 2222
User root
```

5. Test your ssh connection. Open SSHelper on your phone, and run `ssh phone` on your Mac. Isn't SSH great!

6. Look in the script and make sure the paths are correct for your mac.

7. Check your phone has enough free space, and run `./upload-music`

# Notes on music players
Android m3u playlist support seems to be really buggy. Very few apps ever seem to refresh correctly to see the new files and playlists. [Poweramp](http://powerampapp.com/) ([2 week trial](https://market.android.com/details?id=com.maxmpz.audioplayer) or [full version](https://play.google.com/store/apps/details?id=com.maxmpz.audioplayer.unlock) seemed to be the only apps that can reload instantly and never fail to refresh.

# Notes on album art
Syncing album art would be another complication, so I used [Doug's Re-Embed Artwork AppleScript](http://dougscripts.com/itunes/scripts/ss.php?sp=reembedartwork) to make sure the album artwork was embedded in the music files themselves.

The script should notice the files have changed size and re-synchronize them.

# Why I built this
I love music, so I regard having an organised collection of albums and playlists on my phone important. The problems I had with current workflows are as follows:

- Google Play Music: Great interface, but need fast internet and there is no option to automatically make all files offline available. Playlist syncing from iTunes buggy.

- [DoubleTwist](https://www.doubletwist.com/): Great interface, but must sync over WiFi with my Nexus 5, and has to upload every single file every time.

- [iSyncr](http://www.jrtstudio.com/iSyncr-iTunes-for-Android): This was my method of choice before this tool. The interface is average, however it was able to sync playlists and music from iTunes. However it is very, very buggy, and playlists wouldn't always sync or update

# License

Android iTunes rsync
Copyright (C) 2017 Jake Coppinger

This program is free software: you can redistribute it and/or modify
it under the terms of the GNU General Public License as published by
the Free Software Foundation, either version 3 of the License, or
(at your option) any later version.

This program is distributed in the hope that it will be useful,
but WITHOUT ANY WARRANTY; without even the implied warranty of
MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
GNU General Public License for more details.

You should have received a copy of the GNU General Public License
along with this program.  If not, see <http://www.gnu.org/licenses/>.


# iTunesExportScale licence
Copyright (c) 2009, Eric Daugherty (http://www.ericdaugherty.com)
All rights reserved.

Redistribution and use in source and binary forms, with or without 
modification, are permitted provided that the following conditions are met:

    * Redistributions of source code must retain the above copyright notice, 
      this list of conditions and the following disclaimer.
    * Redistributions in binary form must reproduce the above copyright 
      notice, this list of conditions and the following disclaimer in the 
      documentation and/or other materials provided with the distribution.
    * Neither the name of the Eric Daugherty nor the names of its 
      contributors may be used to endorse or promote products derived 
      from this software without specific prior written permission.

THIS SOFTWARE IS PROVIDED BY THE COPYRIGHT HOLDERS AND CONTRIBUTORS "AS IS" 
AND ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO, THE 
IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE 
ARE DISCLAIMED. IN NO EVENT SHALL THE COPYRIGHT OWNER OR CONTRIBUTORS BE 
LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR 
CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF 
SUBSTITUTE GOODS OR SERVICES; LOSS OF USE, DATA, OR PROFITS; OR BUSINESS 
INTERRUPTION) HOWEVER CAUSED AND ON ANY THEORY OF LIABILITY, WHETHER IN 
CONTRACT, STRICT LIABILITY, OR TORT (INCLUDING NEGLIGENCE OR OTHERWISE) 
ARISING IN ANY WAY OUT OF THE USE OF THIS SOFTWARE, EVEN IF ADVISED OF 
THE POSSIBILITY OF SUCH DAMAGE.