+++
title = "Technical debt through Permanent Man-in-the-Middle"
tags = ["intercept"]
date = "2015-02-24"
+++

An [astute observation](http://www.theguardian.com/technology/2015/feb/23/superfish-style-vulnerability-found-games-parental-control-software?linkId=12522307) on the technical debt and erosion of controls of on-going MitM (if not managed carefully):

>Facebook’s Richard says: “What all of these applications have in common is that they make people less secure through their use of an easily obtained root CA, they provide little information about the risks of the technology, and in some cases they are difficult to remove.

>“Furthermore, it is likely that these intercepting SSL proxies won’t keep up with the HTTPS features in browsers (e.g., certificate pinning and forward secrecy), meaning they could potentially expose private data to network attackers. Some of these deficiencies can be detected by anti-virus products as malware or adware, though from our research, detection successes are sporadic.”
