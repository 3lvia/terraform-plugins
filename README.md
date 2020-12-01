# terraform-plugins
This repo contains compiled linux_amd64 binaries for plugins. This will be used by terraform workspaces for systems through git submodules.

Note this repo must be public for easy access for terraform enterprise.

# Plugins distributed by this repo

## terraform-provider-elvid
Provider for maintainnig ElvID resources. Source code: https://github.com/3lvia/terraform-provider-elvid

# To add a new plugin or new plugin version
## Build and the plugin binary to the repo and make it executable
This involves go build. For terraform-provider-elvid follow the readme in that repo first.

Add binaries to the elvid.elvia.io folder as well

Then add the binaries as executable:
```console
git add . --chmod=+x
git commit -m "Added terraform-provider-{name}_v{version} as executable"
git push
```
## Clean up some old versions
Maybe clean up by removing some old versions

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


