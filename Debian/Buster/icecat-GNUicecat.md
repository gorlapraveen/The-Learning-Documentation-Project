# GNU icecat

GNUzilla is the GNU version of the Mozilla suite, and GNU IceCat is the GNU versionof the Firefox browser. Its main advantage is an ethical one: it is entirely [free software](http://www.gnu.org/philosophy/free-sw.html). While the Firefox source code from the Mozilla project is free software, they distribute and recommend non-free software as plug-ins and addons. 
Also their trademark license imposes requirements for the distribution of modified versions that make it inconvenient to exercise freedom 3.


## Installation of GNU Icecat in Debian 

----------------------------------------------------------

If you want to install icecat (GNU icecat) on your Debian, you can do it by following those steps.

    * Download the GNU Icecat version that you want directly from the [official website](https://www.gnu.org/software/gnuzilla/)
    
    * Uncompress the archives in the */opt* folder if you want to install it system-wide (you will need to have root privilege) or in your home folder if you only want to install it for your current user.
    * Create a .desktop file named *icecat.desktop* (replace *icecat* with the name of your choice, preferably *icecat-your_version* ) in */usr/share/applications* if you want to install it system-wide (you will need to have root privilege) or in *.local/share/applications* if you only want to install it for your current user. 

**Creating a .desktop file for icecat**

Here is an example of a .desktop file

```
[Desktop Entry]
Name=Icecat ''Your version''
Comment=Web Browser
GenericName=Web Browser
X-GNOME-FullName=Icecat ''Your version'' Web Browser
Exec=/path/to/icecat/icecat %u
Terminal=false
X-MultipleArgs=false
Type=Application
Icon=/path/to/icecat/browser/chrome/icons/default/default128.png
Categories=Network;WebBrowser;
MimeType=text/html;text/xml;application/xhtml+xml;application/xml;application/vnd.mozilla.xul+xml;application/rss+xml;application/rdf+xml;image/gif;image/jpeg;image/png;x-scheme-handler/http;x-scheme-handler/https;
StartupWMClass=Icecat
StartupNotify=true
```