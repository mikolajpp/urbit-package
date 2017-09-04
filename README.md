# urbit-package

## Description
Simple package manager for urbit

### Package spec
The package specification defines package metadata (name, etc.) as well as all the files and prerequisite packages that needs to be installed.

#### JSON
```
{
  "name": "package",
  "description": "A package manager for urbit",
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
        "/sur/package/hoon",
        "/mar/package/package/hoon",
        "/app/package/hoon"
      ]
    }
  ]
}
```

## Usage

Poke with a desk and a URL of a package specification.

The URL can point to any web server. It can be a github page of a published package or a local web server for local development (instead of manually copying your app files from your local git repo to the urbit unix mount on every change).

### Dojo
```
> |merge %packageapp our %base
> :package [%install %packageapp (need (epur 'https://github.com/asssaf/urbit-package/package.json'))]
```

For copying local dev app:
```
:package [%install %mydevapp (need (epur 'http://localhost.localdomain:8080/pages/packages/mypackage.json'))
```

Note: When using `++  epur` with `http://localhost` it will set the secure flag and this will cause an http parse error. You can use something like `http://localhost.localdomain` as a workaround (assuming it is defined in `/etc/hosts`).


## Future
* Make the app stateful
  * Support uninstall
  * Detect conflicts / changed files
* Web interface for installing packages without the dojo
* Poll URLs for changes and autosync (copy changed files as soon as they're save in your IDE)