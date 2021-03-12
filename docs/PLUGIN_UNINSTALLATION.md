# Experiment: Uninstall a plugin

* Setup a sandbox with pulpcore and multiple plugins installed.

## Uninstall `pulp_file`

Confirmed works:
* `sudo -i`
* `systemctl stop pulp*`
* `pulpcore-manager migrate --plan file zero`
  look for `Raw Python operation -> IRREVERSIBLE`
* `pulpcore-manager migrate file zero`
* `/usr/local/lib/pulp/bin/pip uninstall pulp_file`
* `systemctl start --all pulp*`

## Confirmed uninstallable plugins:

* `pulp_file`
* `pulp_python`
* `pulp-certguard`

Uninstalled them.

## Non-reverseable migrations:

* `pulp_ansible`
* `pulp_container`
* `pulp_rpm`

## Reinstall plugins

Ran `vagrant provision ...` to check if plugins are reinstallable.

## Notes:

- Down migrations must be performed, while the plugin code is still installed.
- Removal of detail models will leave the master table in a bad state.
  - This seems to be a general problem with django (tried with `2.2.*` and `3.*`)
