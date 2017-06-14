---
title: "Linux notes"
layout: page
---

Linux specific notes, useful command lines and memory joggers...

Kernel
------

To speed up kernel compilation, create a kernel config file with only the modules loaded for the current system:

`make localmodconfig`

Note: To merge configs from multiple machines see this [Stackoverflow answer](http://stackoverflow.com/questions/11470447/trying-to-find-all-the-kernel-modules-needed-for-my-machine-using-shell-script)
