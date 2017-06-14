+++
title = "dpass: dmenu meets pass"
date = "2014-01-24"
tags = ["dmenu", "pass"]
+++

This post shows how to integrate cli based password manager with your favourite Window Manager on X Windows to make getting to your passwords quick and painless

First install and set-up [pass](http://zx2c4.com/projects/password-store) (`pass init)`), then [dmenu](http://tools.suckless.org/dmenu/) from Suckless and [pinentry](https://wiki.archlinux.org/index.php/GnuPG#Pinentry).

Add some passwords using `pass insert` or `pass generate`, here's an edited version of `pass list`:

	Password Store
	|-- cloudive
	|-- crissic
	|-- delim
	|-- fluxbb
	|-- inceptionhosting
	|-- ipxcore
	|-- openitc
	|-- prometeus
	|-- ramnode
	|-- scriptogram
	|-- temp
	`-- www

`dpass` (below) is a simple script lists the encrypted gpg files in `~/.password-store`, feeds them to dmenu for you to select either through typing a search string or using the arrow keys.  The selected item is then output on stdout when dmenu exits, which in turn is piped to xargs to run `pass show -c` which copies the cleartext password to the clipboard for 30 seconds for you to paste wherever..

	#!/bin/sh
	# dpass: simple password retrieval
	#
	ls -1 $HOME/.password-store/ | sed -e 's/.gpg$//' | dmenu -fn abel -nb \#cccccc -nf \#000000 -sb \#0066ff -sf \#ffffff | xargs pass show -c

Note: I don't use sub-folders, but if I did, I might change the `ls -1` to a `find ... | sed -e...`.

To avoid getting prompted by pinentry for your master password-store password everytime, install and run gpg-agent to cache your master password for a configurable time.
