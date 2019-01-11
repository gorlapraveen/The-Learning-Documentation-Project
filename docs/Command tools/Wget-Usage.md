## (I)Usage 
1. To Downoload recurcivelry use `wget -r www.example.com`.This downloads the pages recursively up to a maximum of `5` levels deep.
2. To Continue/resume Download if they is chance of interuption, use `wget -c www.example.com`.
3. To Download to a deep level more than 5 levels, use `wget -r -l10 www.example.com `, example for depth of 10. for `infinite levels` use `-l inf`.
4. To download a specifc files at a depth of `10` recurcively, with resume option use `wget -A "*.pdf" -rc -l10 www.example.com`.

Find more at 
https://www.lifewire.com/uses-of-command-wget-2201085
## (II)Issues

1. There is a chance of getting `403 Forbidden` for some links, those websites may block those with improper headers, so make them to think that you are a browser. So use `wget -mk -w 20 --user-agent="Mozilla/4.5 (X11; U; Linux x86_64; en-US)" https://www.example.com`.
2. Incase you get error for `(I)(4)` use `wget  -A "*.pdf" -rc -mk -w 20 --user-agent="Mozilla/4.5 (X11; U; Linux x86_64; en-US)" https://www.example.com`.

Find more at https://superuser.com/questions/786097/wget-mirroring-the-site-fails-403-forbidden-even-with-user-agent