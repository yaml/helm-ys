helmys
======

Helm + YS - Support YAMLScript in Helm Templates


## Synopsis

```
$ helm install <name> <chart> --post-renderer=helmys
```


## Description

The `helmys` (pronounced "helm wise") command provides a way to use YAMLScript
for Helm templating.
You can use as much or as little YAMLScript in your Helm templates, replacing
all the Go templating syntax or none of it.

Using YAMLScript for your templating needs is much cleaner than the standard Go
templating.
See this gist for a comparison of a full conversion:

https://gist.github.com/ingydotnet/c0afc0071133c696c5b4f17b5ee86b98


## Setting It Up

To use `helm install ... --post-renderer=helmys` you need:


### YAMLScript's `ys` 0.1.84 or higher installed

See:
* https://yamlscript.org/doc/install/
* https://github.com/yaml/yamlscript/releases

Quick install:
```
$ curl -s https://yamlscript.org/install | BIN=1 bash
```


### The `helpers.ys` file in your chart's `templates/` directory

This is a YAMLScript port of the default `_helpers.tpl` Go template file.
It is used to define reusable variables and functions for use by the YAMLScript
in your templates.

```
$ cp template/helpers.ys <chart>/template/helpers.ys
```

This `helpers.ys` file supports everything for the templates generated by
`helm create`.
You are encouraged to add your own functions and variables to it.


### The `helmys.yaml` file in your chart's `templates/` directory.

This template gets data for the `Release` template variable.

```
$ cp template/helmys.yaml <chart>/templates/helmys.yaml
```


### The `helmys` Bash script file in your `PATH`

Just copy `bin/helmys` into a directory that's in your `PATH` so `helm` can
find it.


### To use the `--post-renderer=helmys` option

```
$ helm install <name> <chart> --post-renderer=helmys
```


## Try It Out

You can run `make test` which just runs the `test.sh` Bash script.
It creates a new Helm chart, adds the `helmys` stuff and runs `helm install`
on it.


## Status

This is very new stuff.

At the moment, it's a PoC to show that YAMLScript can be used with Helm 3.
Expects bugs, fixes and changes.

Please let us know what's wrong with it, and how it can be made better.


## License & Copyright

Copyright 2024 Ingy döt Net <ingy@ingy.net>

This project is licensed under the terms of the `MIT` license.
See the [License](https://github.com/kubeys/helmys/blob/main/License) file for
more details.
