


[PostgreSQL](http://www.postgresql.org) is a relational database manager that
keeps getting more and more popular within the web development community. It 
has taken over from [MySQL](http://www.mysql.com) as the preferred tool for
production quality, scalable databases. The rise in popularity is likely due to
the backlash from Oracle purchasing and [messing with MySQL](http://techcrunch.com/2012/08/18/oracle-makes-more-moves-to-kill-open-source-mysql/), Heroku [choosing Postgres](https://www.heroku.com/postgres)
as the preferred database in production, and Postgres' faster pace of development
of new features like [Arrays and HStore](http://adamsanderson.github.io/railsconf_2013/).

- [Mac OS X](#macosx)
- [Windows](#windows)
- [Ubuntu](#ubuntu)

<a name="macosx"></a>
### How to Install Postgres on Mac OS X

There are a lot of [confusing options](http://www.postgresql.org/download/macosx/)
for installing PostgreSQL. In fact, your Mac most likely came with a system 
version of Postgres. The problem is that version is already likely out-of-date,
and may even be insecure. It is better to keep all programs you use for development
in user space instead of installed system-wide if possible, so that you don't mess
with [what Apple configured the system to expect](https://discussions.apple.com/message/23547312#23547312).

I prefer to use the [homebrew](http://brew.sh) package manager because it makes
it easier to keep the software up-to-date. Brew also installs all commands 
needed to manage Postgres to standard locations in your path, which makes it
easier to use on the command line, and easier for libraries like
[Ruby Gems](https://rubygems.org/gems/pg) and
[npm packages](https://npmjs.org/package/pg) to interact with.

This lesson below will teach you how to install PostgreSQL, the easy way, on a Mac.
This tutorial is designed for Max OS 10.9 - Mavericks. If you don't have
Mavericks, upgrade your mac first.

#### Open up the Terminal

![opening the terminal](http://assets.codefellows.org/install_homebrew_postgres/images/Install_Homebrew_and_PostgreSQL_on_Mac_OS_X_Mavericks/media_1387413864323.png)

You'll need to do many of these steps in the command line.

#### Install Homebrew

![install homebrew](http://assets.codefellows.org/install_homebrew_postgres/images/Install_Homebrew_and_PostgreSQL_on_Mac_OS_X_Mavericks/media_1387413932210.png)

Copy the install command from the Install Homebrew section, near the bottom of
the page on http://brew.sh

Caveats:

Don't re-install homebrew if you already have it.  
If you already have it, make sure to do a `brew update` to ensure you have the
latest package info on your system.  
If you have MacPorts or Fink installed, this tutorial won't work for you. I
recommend switching to Homebrew anyway as it is kept up to date more often.  
If you have homebrew installed via RVM (it happens), your paths will begin
with /home/username/.rvm/usr/local instead of just /usr/local - not to worry.

#### Start homebrew installation

![](http://assets.codefellows.org/install_homebrew_postgres/images/Install_Homebrew_and_PostgreSQL_on_Mac_OS_X_Mavericks/media_1387414019607.png)

Paste the install homebrew command into the Terminal. It should look somewhat
like the picture above.

#### Install the Command Line Tools

![](http://assets.codefellows.org/install_homebrew_postgres/images/Install_Homebrew_and_PostgreSQL_on_Mac_OS_X_Mavericks/media_1387414053245.png)

You may already have these if you've been developing for a while. If you see
the dialog above, let them install.

#### Wait for the command line tools to download

![](http://assets.codefellows.org/install_homebrew_postgres/images/Install_Homebrew_and_PostgreSQL_on_Mac_OS_X_Mavericks/media_1387414077419.png)

This step can take a while, hopefully you are on a good connection.

#### Enter your password

![](http://assets.codefellows.org/install_homebrew_postgres/images/Install_Homebrew_and_PostgreSQL_on_Mac_OS_X_Mavericks/media_1387414408632.png)

Homebrew needs your user password to set itself up. Enter it in the terminal.
Be careful typing, because you won't see your typing echoed back to you. It
may seem like it's not working, but if you enter in your password, and then
press return, it should work.

#### Homebrew finishes!

![](http://assets.codefellows.org/install_homebrew_postgres/images/Install_Homebrew_and_PostgreSQL_on_Mac_OS_X_Mavericks/media_1387414463163.png)

You should see "Installation successful!"

#### Run brew doctor

![](http://assets.codefellows.org/install_homebrew_postgres/images/Install_Homebrew_and_PostgreSQL_on_Mac_OS_X_Mavericks/media_1387414484491.png)

You should see "Your system is ready to brew". If not, there should be
instructions on how to fix each issue it finds.

#### brew install postgres

![](http://assets.codefellows.org/install_homebrew_postgres/images/Install_Homebrew_and_PostgreSQL_on_Mac_OS_X_Mavericks/media_1387414540503.png)

use the command `brew install postgres` to get PostgreSQL

#### Make sure to read the Caveats

![](http://assets.codefellows.org/install_homebrew_postgres/images/Install_Homebrew_and_PostgreSQL_on_Mac_OS_X_Mavericks/media_1387414570920.png)

It's a lot of text scrolling by and the temptation is to skim over it. ALWAYS
read the Caveats section when installing with Homebrew. It contains critical
info. I'll go over what you need.

#### Create the LaunchAgents Directory and Link the plist

![](http://assets.codefellows.org/install_homebrew_postgres/images/Install_Homebrew_and_PostgreSQL_on_Mac_OS_X_Mavericks/media_1387414624947.png)

    mkdir -p ~/Library/LaunchAgents  
    ln -sfv /usr/local/opt/postgresql/*.plist ~/Library/LaunchAgents


These two commands create a LaunchAgents directory (if it didn't exist
already), and then make a symbolic link to the postgres configuration
(property list) file. This is how you get PostgreSQL to start up automatically
with your Mac.

#### Load the plist

![](http://assets.codefellows.org/install_homebrew_postgres/images/Install_Homebrew_and_PostgreSQL_on_Mac_OS_X_Mavericks/media_1387414640076.png)

copy `launchctl load ~/Library/LaunchAgents/homebrew.mxcl.postgresql.plist` from
the homebrew caveats section  
load the plist into the launch control service so that postgresql will
automatically reload if needed.

#### Load the plist

![](http://assets.codefellows.org/install_homebrew_postgres/images/Install_Homebrew_and_PostgreSQL_on_Mac_OS_X_Mavericks/media_1387414655649.png)

paste in the launchctl load command

#### Edit the system paths

![editing system paths](http://assets.codefellows.org/install_homebrew_postgres/images/Install_Homebrew_and_PostgreSQL_on_Mac_OS_X_Mavericks/media_1387414842894.png)

Because Mac OS X comes with a system PostgreSQL, we want to make sure to load
up our homebrew PostgreSQL first.  
use the command

    sudo nano /etc/paths

#### Default Paths

![default paths](http://assets.codefellows.org/install_homebrew_postgres/images/Install_Homebrew_and_PostgreSQL_on_Mac_OS_X_Mavericks/media_1387414852442.png)

Copy (or retype) `/usr/local/bin` from the bottom of the file and put it on the
top line.

#### Finished editing /etc/paths

![img](http://assets.codefellows.org/install_homebrew_postgres/images/Install_Homebrew_and_PostgreSQL_on_Mac_OS_X_Mavericks/media_1387414875363.png)

Press Ctrl-X to save the file and answer yes.

#### Write to /etc/paths

![img](http://assets.codefellows.org/install_homebrew_postgres/images/Install_Homebrew_and_PostgreSQL_on_Mac_OS_X_Mavericks/media_1387414886883.png)

Save the file in its existing location (/etc/paths)

#### Confirm the changes

![confirm](http://assets.codefellows.org/install_homebrew_postgres/images/Install_Homebrew_and_PostgreSQL_on_Mac_OS_X_Mavericks/media_1387414900686.png)

Use the unix `cat` command to confirm that your changes were saved

#### Reboot

![reboot](http://assets.codefellows.org/install_homebrew_postgres/images/Install_Homebrew_and_PostgreSQL_on_Mac_OS_X_Mavericks/media_1387414955093.png)

I know, this is Unix and not windows. But this is seriously the easiest way to
do this. Don't skip this step.

#### Which psql

![which psql](http://assets.codefellows.org/install_homebrew_postgres/images/Install_Homebrew_and_PostgreSQL_on_Mac_OS_X_Mavericks/media_1387415116045.png)

After rebooting, your `which psql` command should return /usr/local/bin/psql

#### Create a default db based on your username

![create default db](http://assets.codefellows.org/install_homebrew_postgres/images/Install_Homebrew_and_PostgreSQL_on_Mac_OS_X_Mavericks/media_1387415158156.png)

the `which psql` command should return `/usr/local/bin/psql`

    createdb `whoami`

Make sure to use backticks, they are below the tilde
(squiggly line) character underneath the escape key on a US keyboard.  
This just makes it easier to use the psql command.


#### Try out the psql command

![try psql](http://assets.codefellows.org/install_homebrew_postgres/images/Install_Homebrew_and_PostgreSQL_on_Mac_OS_X_Mavericks/media_1387415196590.png)

Great! you can get into psql without any errors

#### Install the pg gem

![install pg](http://assets.codefellows.org/install_homebrew_postgres/images/Install_Homebrew_and_PostgreSQL_on_Mac_OS_X_Mavericks/media_1387433710226.png)

`gem install pg` and you're good to go

<a name="windows"></a>
### How to Install Postgres on Windows

Windows is straightforward: use the [installer from Postgresql.org](http://www.postgresql.org/download/windows/)
You can accept all of the default options. 

<a name="ubuntu"></a>
### How to Install Postgres on Ubuntu Linux

