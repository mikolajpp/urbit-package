# urbit-package
[![package hash](https://img.shields.io/badge/dynamic/json.svg?label=%package%20hash&colorB=008bb8&prefix=&suffix=&query=$.hash&uri=https://raw.githubusercontent.com/asssaf/urbit-package/master/package.json)](https://raw.githubusercontent.com/asssaf/urbit-package/master/package.json)
[![sync ship](https://img.shields.io/badge/dynamic/json.svg?label=sync%20ship&colorB=008bb8&prefix=&suffix=&query=$.our&uri=https://dist.u.replaythat.com/pages/badge.json)](#urbit-sync)

## Description
Simple package manager for urbit

### Package spec
The package specification defines package metadata (name, etc.) as well as all the files and prerequisite packages that needs to be installed.

#### JSON
```
{
  "name": "package",
  "description": "A package manager for urbit",
  "hash": "0vg.frcc0.nh5a0.trbqa.1rqe5.3c1tq.kg69n.8fo2f.jkcuo.ge1gc.tdd59",
  "homepage": "https://github.com/asssaf/urbit-package",
  "items": [
    {
      "type": "package",
      "url": 'https://raw.githubusercontent.com/asssaf/urbit-json/package.json'
    },
    {
      "type": "fileset",
      "base": "https://raw.githubusercontent.com/asssaf/urbit-package/master/src",
      "rels": [
        "/sur/package.hoon",
        "/mar/package/package.hoon",
        "/app/package.hoon"
      ]
    }
  ]
}
```

## Install

Unfortunately, you can't use `%package` to install itself if it's not already installed, so the traditional methods are available (once installed, you can use the `package.json` in this repository to install updated versions).

### Urbit Sync
You can sync from the `%dist-package` desk on ![ship](https://img.shields.io/badge/dynamic/json.svg?label=ship&colorB=008bb8&prefix=&suffix=&query=$.our&uri=https://dist.u.replaythat.com/pages/badge.json).
```
dojo> |sync %home ~dist-ship %dist-package
```

### Manual
Assuming you have a desk mounted:
```
$ cp -a src/* /path/to/pier/home/
```

## Usage

Poke with a desk and a URL of a package specification.

The URL can point to any web server. It can be a github page of a published package or a local web server for local development (instead of manually copying your app files from your local git repo to the urbit unix mount on every change).

### Dojo
#### Install Package
Install a package into a desk with %xyz prefix (will create %xyz-package desk)
```
> :package|install %xyz "https://raw.githubusercontent.com/asssaf/urbit-package/master/package.json"
```

For copying local dev app:
```
:package|install %dev "http://localhost.localdomain:8080/pages/packages/mypackage.json"
```

Note: When using `++  epur` with `http://localhost` it will set the secure flag and this will cause an http parse error. You can use something like `http://localhost.localdomain` as a workaround (assuming it is defined in `/etc/hosts`).

#### Resume
Resume in case installation stopped:
```
> :package [%resume %xyz]
```

## Future
* Web interface for installing packages without the dojo
* Poll URLs for changes and autosync (copy changed files as soon as they're saved in your IDE)
