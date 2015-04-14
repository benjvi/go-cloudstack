go-cloudstack
=============
A CloudStack API client enabling Go programs to interact with CloudStack in a simple and uniform way

## Status

This package is completely finished (is something ever really finished...? :wink:) and tested. Of course there will still be untested corner cases when you have over 250 API commands that you can use, but over all it's save to use this package.

I know there are more Go CloudStack packages out there, but I created yet another one because non of them seemed to be complete... This one is. It uses the code in the generate package to generate the static code needed for all available API commands. It does this per CloudStack version, because some API command change over time.

To be able to find the API command you want, they are grouped by 'services' which match the grouping you can see/find on the [CloudStack API docs](http://cloudstack.apache.org/docs/api/apidocs-4.4/TOC_Root_Admin.html) website.

## Usage

For the most part the generic API commands do not change that much, so you should be able to use just the cloudstack package opposed to the specific cloudstackXX packages. The cloudstack package is always the one generate against the latest stable CloudStack release (currently v4.4.x). If you need some specific API command of a specific CloudStack version, you should use the matching cloudstackXX package instead.

When you have choosen the package you want to use, please see the details about it on [GoDocs](http://godoc.org/github.com/xanzy/go-cloudstack). It can use some more documentation, but generaly it speaks for itself.

## Features

Next to the API commands CloudStack itself offers, there are a few additional features/function that are helpful. For starters there are two clients, an normal one (created with `NewClient(...)`) and an async client (created with `NewAsyncClient(...)`). The async client has a buildin waiting/polling feature that waits for a configured amount of time (defaults to 60 seconds) on running async jobs. This is very helpfull if you do not want to continue with your program execution until the async job is done.

There is also a function you can call manually (`GetAsyncJobResult(...)`) that does the same, but then as a seperate call after you started the async job.

Another nice feature is the fact that for every API command you can create the needed parameter struct using a `New...Params` function, like for example `NewListTemplatesParams`. The advantage of using this functions to create a new parameter struct, is that these functions know what the required parameters are of ever API command, and they require you to supply these when creating the new struct. Every additional paramater can be set after creating the struct by using `SetName()` like functions.

Last but not least there are a whole lot of helper function that will try to automatically find an UUID for you for a certain item (disk, template, virtualmachine, network...). This makes it much easier and faster to work with the API commands and in most cases you can just use then if you know the name instead of the UUID.

## Code Generation (If generate.go is updated)

The generate.go generates the three cloudstack folders according to the version specified in generate.go. After this has been run, it may also be necessary to run: "goimports -w=true /opt/gopath/src/github.com/xanzy/go-cloudstack/cloudstack" where the goimports soruce can be fetched from "go get golang.org/x/tools/cmd/goimports".

## ToDO

I fully understand I need to document this all a little more/better and there should also be some tests added.

## Getting Help

_Please try to see if [GoDocs](http://godoc.org/github.com/xanzy/go-cloudstack) can provide some answers first!_

* If you have an issue: report it on the [issue tracker](https://github.com/xanzy/go-cloudstack/issues)

## Author

Sander van Harmelen (<sander@xanzy.io>)

## License

Licensed under the Apache License, Version 2.0 (the "License"); you may not use this file except in compliance with the License. You may obtain a copy of the License at <http://www.apache.org/licenses/LICENSE-2.0>
