python3 irc bot

BOTZ is a python3 irc bot, it can connect to IRC, fetch and display RSS
feeds, take todo notes, keep a shopping list and log text. You can also
copy/paste the service file and run it under systemd for 24/7 presence
in a IRC channel.

BOTZ users BOTL, containing all the python3 code to program a unix cli
program, such as disk perisistence for configuration files, event handler
to handle the client/server connection, code to introspect modules for
commands, deferred exception handling to not crash on an error, a parser to parse commandline options and values, etc.

BOTZ uses OBJX, an module that allows for easy json save//load
to/from disk of objects. It provides an "clean namespace" Object class
that only has dunder methods, so the namespace is not cluttered with
method names. This makes storing and reading to/from json possible.

BOTZ is Public Domain.

SYNOPSIS

    botz <cmd> [key=val] [key==val]
    botz [-a] [-c] [-d] [-h] [-v] 

USAGE

without any argument the program does nothing

    $ botz
    $


see list of commands

    $ botz cmd
    cmd,err,mod,req,thr,ver


list of modules

    $ botz mod
    cmd,err,fnd,irc,log,mod,req,rss,tdo,thr


use mod=<name1,name2> to load additional modules

    $ botz cfg mod=irc


start a console

    $ botz -c mod=irc,rss
    >


use -v for verbose

    $ botz -cv mod=irc
    BOTL started CV started Sat Dec 2 17:53:24 2023
    >


start daemon

    $ botz -d
    $ 

CONFIGURATION

irc

    $ botz cfg server=<server>
    $ botz cfg channel=<channel>
    $ botz cfg nick=<nick>

sasl

    $ botz pwd <nsvnick> <nspass>
    $ botz cfg password=<frompwd>

rss

    $ botz rss <url>
    $ botz dpl <url> <item1,item2>
    $ botz rem <url>
    $ botz nme <url> <name>

COMMANDS

    cmd - commands
    cfg - irc configuration
    dlt - remove a user
    dpl - sets display items
    fnd - find objects 
    log - log some text
    met - add a user
    mre - displays cached output
    pwd - sasl nickserv name/pass
    rem - removes a rss feed
    req - reconsider
    rss - add a feed
    thr - show the running threads

SYSTEMD

save the following it in /etc/systems/system/botz.service and
replace "<user>" with the user running pipx

    [Unit]
    Description=python3 irc bot
    Requires=network-online.target
    After=network-online.target

    [Service]
    Type=simple
    User=<user>
    Group=<user>
    WorkingDirectory=/home/<user>/.botz
    ExecStart=/home/<user>/.local/pipx/venvs/botz/bin/botz -d
    RemainAfterExit=yes

    [Install]
    WantedBy=multi-user.target

then run this

    $ mkdir ~/.botz
    $ sudo systemctl enable botz --now

default channel/server is #botz on localhost

FILES

    ~/.botz
    ~/.local/bin/botz
    ~/.local/pipx/venvs/botz/

AUTHOR

    Bart Thate <objx@proton.me>

COPYRIGHT

    BOTL is Public Domain.
