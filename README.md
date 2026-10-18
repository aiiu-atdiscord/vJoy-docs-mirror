# vJoy site backup

Backup of the official vJoy site originally located at `http://vjoystick.sourceforge.net/site/`

I extracted the content from Wayback Machine, specifically from captures dated 2018.

## Start exploring

Site home: [site.md](site.md)

Download & Install: [download-a-install.md](download-a-install.md)

Utilities: [utilities-218.md](utilities-218.md)

Architecture: [dev216.md](dev216.md)

## Line endings

Before editing files in the repository, you should set this configuration:

~~~bash
git config set --local core.autocrlf false
~~~

If you use Jujutsu VCS, set this one too:

~~~bash
jj config set --repo working-copy.eol-conversion "none"
~~~