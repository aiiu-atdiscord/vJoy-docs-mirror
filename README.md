# vJoy site backup

Unofficial backup of the vJoy site originally hosted at `http://vjoystick.sourceforge.net/site/`

I extracted the site content from Wayback Machine, specifically from captures dated 2018.

Additional contributions to formatting, and typo fixes, are welcome.

## Start exploring

Site home: [site.md](site.md)

Download & Install: [download-a-install.md](download-a-install.md)

Utilities: [utilities-218.md](utilities-218.md)

Architecture: [dev216.md](dev216.md)

## CRLF line endings (Windows)

To preserve the CRLF line endings, you should set this configuration in your local clone of this repo  before making edits:

~~~bash
git config set --local core.autocrlf false
~~~

If you use Jujutsu VCS, set this configuration too:

~~~bash
jj config set --repo working-copy.eol-conversion "none"
~~~
