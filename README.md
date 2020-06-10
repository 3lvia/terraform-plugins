# terraform-plugins
This repo contains compiled linux_amd64 binaries for plugins. This will be used by terraform workspaces for systems through git submodules

# Plugins distributed by this repo

## terraform-provider-elvid
Provider for maintainnig ElvID resources. Source code: https://github.com/3lvia/terraform-provider-elvid

## terraform-provider-azuredevops
Provider for maintaining azuredevops resources.
This is created by Microsoft. See their license here: https://github.com/microsoft/terraform-provider-azuredevops/blob/master/LICENSE

# To add a new plugin or new plugin version
Note that you do not need to remove old versions of the plugin, if it is desired to keep that available for consumers that have not upgraded
## Build the provider or get linux_amd64 binaries from another source
For building:
```console
$env:GOOS = "linux"
go build -o terraform-provider-{name}_v{version}
# If you are building an custom provider that we maintains, then create an release with the same version number in the provider repo
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
Note 1: The folder terraform.d\plugins\linux_amd64 must be removed from {system}-terraform. Commit this removal
Note 2: The terraform repo must "Include submodules on clone"
```console
git submodule add https://github.com/3lvia/terraform-plugins.git terraform.d/plugins/linux_amd64
```

## Update {system}-terraform to get newer versions of this submodule
Unfortionatly we need to run an update in the {system}-terraform repo to get newer versions of this submodule
```console
git submodule foreach git pull origin master
```


