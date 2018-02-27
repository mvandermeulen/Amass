# Subdomain Enumeration

### On the smart and quiet side

[![](https://img.shields.io/badge/go-1.8-blue.svg)](https://github.com/moovweb/gvm) [![License](https://img.shields.io/badge/license-Apache%202.0-blue.svg)](https://www.apache.org/licenses/LICENSE-2.0)


The amass tool searches Internet data sources, performs brute force subdomain enumeration, searches web archives, and uses machine learning to generate additional subdomain name guesses. DNS name resolution is performed across many public servers so the authoritative server will see the traffic coming from different locations.


## Install

1. Download [amass](https://github.com/caffix/amass):
```
$ go get -u github.com/caffix/amass
```

At this point, the amass binary should be in *$GOPATH/bin*.


2. Several wordlists can be found in the following directory:
```
$ ls $GOPATH/src/github.com/caffix/amass/wordlists
```


## Using amass

The most basic use of the tool, which includes reverse DNS lookups and name alterations:
```
$ amass example.com
```


Get amass to provide summary information:
```
$ amass -v example.com
www.example.com
ns.example.com
...
13242 names discovered - search: 211, dns: 4709, archive: 126, brute: 169, alterations: 8027
```


Have amass print IP addresses with the discovered names:
```
$ amass -ip example.com
```

Have amass perform brute force subdomain enumeration as well:
```
$ amass -brute example.com
```


Change the wordlist used during the brute forcing phase of the enumeration:
```
$ amass -words wordlist.txt example.com
```


Throttle the rate of DNS queries by number per minute:
```
$ amass -freq 120 example.com
```

**The maximum rate supported is one DNS query every 1 millisecond.**


Allow amass to included additional domains in the search using reverse whois information:
```
$ amass -whois example.com
```


You can have amass list all the domains discovered with reverse whois before performing the enumeration:
```
$ amass -whois -list example.com
```


Add some additional domains to the search:
```
$ amass example.com example1.com example2.com
```

In the above example, the domains example1.com and example2.com are simply appended to the list potentially provided by the reverse whois information.


All these options can be used together:
```
$ amass -v -ip -whois -brute -words wordlist.txt -freq 240 example.com example1.com
```

**Be sure that the target domain is the last parameter provided to amass, then followed by any extra domains.**


## Settings for the amass Maltego Local Transform

1. Setup a new local transform within Maltego:

![alt text](https://github.com/caffix/amass/blob/master/examples/maltegosetup1.png "Setup")


2. Configure the local transform to properly execute the go program:

![alt text](https://github.com/caffix/amass/blob/master/examples/maltegosetup2.png "Configure")


3. Go into the Transform Manager, and disable the **debug info** option:

![alt text](https://github.com/caffix/amass/blob/master/examples/maltegosetup3.png "Disable Debug")


## Let me know what you think

**NOTE: Still under development**

**Author: Jeff Foley / @jeff_foley**

**Company: ClaritySec, Inc. / @claritysecinc**