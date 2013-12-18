[PostgreSQL](http://www.postgresql.org) is a relational database manager that
keeps getting more and more popular within the web development community. It 
has taken over from [MySQL](http://www.mysql.com) as the preferred tool for
production quality, scalable databases. The rise in popularity is likely due to
the backlash from Oracle purchasing MySQL, [Heroku choosing Postgres](https://www.heroku.com/postgres)
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

<a name="windows"></a>
### How to Install Postgres on Windows

Windows is straightforward: use the [installer from Postgresql.org](http://www.postgresql.org/download/windows/)



<a name="ubuntu"></a>
### How to Install Postgres on Ubuntu Linux

