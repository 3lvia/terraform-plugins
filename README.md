# terraform-plugins
This repo contains compiled linux_amd64 binaries for plugins. This will be used by terraform workspaces for systems through git submodules.

Note this repo must be public for easy access for terraform enterprise.

# Plugins distributed by this repo

## terraform-provider-elvid
Provider for maintainnig ElvID resources. Source code: https://github.com/3lvia/terraform-provider-elvid

# To add a new plugin or new plugin version
Note that you do not need to remove old versions of the plugin, if it is desired to keep that available for consumers that have not upgraded

## Build the provider or get linux_amd64 binaries from another source
For building from powershell from provider source:
```console
$env:GOOS = "windows";$env:GOARCH = "amd64"; go build -o; go build -o C:\3lvia\terraform-plugins\terraform-provider-{name}_v{version}_windows
$env:GOOS = "linux"; go build -o C:\3lvia\terraform-plugins\terraform-provider-{name}_v{version}
```

## Add the plugin binariy to this repo and make it executable 
```console
# place the binary in the root of this repo
git add terraform-provider-{name}_v{version}
git update-index --chmod=+x terraform-provider-{name}_v{version}
git commit -m "Added terraform-provider-{name}_v{version} as executable"
git push
```

# Usage from the {system}-terraform repo/workspace
## Install this repo as an submodule
Note 1: The folder terraform.d\plugins\linux_amd64 must be removed from {system}-terraform. Commit this removal.

Note 2: The terraform repo must "Include submodules on clone".

```console
git submodule add https://github.com/3lvia/terraform-plugins.git terraform.d/plugins/linux_amd64
```

## Update {system}-terraform to get newer versions of this submodule
Unfortionatly we need to run an update in the {system}-terraform repo to get newer versions of this submodule
```console
git submodule foreach git pull origin master
git add -A
git commit -m "Updated submodules"
git push
```

Merge to master also for {system}-terraform


