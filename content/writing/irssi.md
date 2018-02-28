+++
date = "2018-02-19"
title = "Getting Started with irssi"
author = "Royce"

+++

How to get started with ```irssi```, the terminal IRC client.

<!--more--> 

## Install

Use Homebrew for the install. It is also helpful to run things in ```tmux``` so that you can maintain sessions. 

```bash
$ brew install irssi
$ tmux -c irssi 
```

## Starting with irssi

```irssi
/set nick royce
```

Make sure to change your username and nicknames if you don't want to use your system username as the default.

## Joining Servers and Channels

Once irssi starts up, you can connect to IRC servers and then join channels. 

```irssi
/connect Freenode
/join #irssi
```


## Config

The main config file is ```~/.irssi/config```.

Adding hilights to your username:

```irssi
hilights = (
  { text = "royce"; color = "%M"; nick = "yes"; word = "yes"; }
);

```

Changing the names associated with your base accout logins.

```irssi
settings = {
  core = { real_name = "royce"; user_name = "royce"; nick = "royce"; };
};


```

I had to remove networks from the default configuration to get things working with the SASL configuration.  

```irssi
/network remove Freenode
/network add -sasl_username <username> -sasl_password <password> -sasl_mechanism plain Freenode
/server add -auto -net Freenode -ssl -ssl_verify irc.freenode.net 6697
/channel add -auto #irssi Freenode

```
