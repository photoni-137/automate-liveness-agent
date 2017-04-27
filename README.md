# Automate Liveness Agent

Automate liveness agent sends keepalive messages to Chef Automate, which
prevents nodes that are up but not frequently running Chef Client from
appearing as "missing" in the Automate UI.

For more info about Chef Automate, see [https://www.chef.io/automate/](https://www.chef.io/automate/).

## Installation

Automate liveness agent is designed to be installed via Chef's "Required
Recipe" feature, which is in development. Check back later for full
instructions.

## Usage

Usage instructions will be made available once this software is
released.

### Configuration

The config file is a JSON formatted file like this:

```json
{
  "chef_server_fqdn": "api.chef.io",
  "data_collector_url": "https://api.chef.io/organizations/chef-oss-dev/data-collector",
  "entity_uuid": "3D0F27ED-AA32-4C73-9A18-F342AAABAA62",
  "org_name": "chef-oss-dev",
  "client_key_path":  "/etc/chef/client.pem",
  "client_name":      "example-node",
  "unprivileged_uid": 100,
  "unprivileged_gid": 200,
  "install_check_file": "/opt/chef/embedded/bin/ruby"
}
```

Settings:

* `chef_server_fqdn`: what it says
* `data_collector_url`: Org-specific data collector endpoint on the Chef
  Server
* `entity_uuid`: UUID generated by Chef Client to identify itself to the
  data collector
* `org_name`: Chef Server organization name
* `client_key_path`: Private key used by Chef Client to authenticate API
  requests
* `client_name`: identity used by Chef Client to authenticate API
  requests
* `unprivileged_uid`: Agent will change it's uid to this after start up.
  Setting to `null` disables that
* `unprivileged_gid`: Agent will change it's gid to this after start up.
  Setting to `null` disables that
* `install_check_file`: Agent will check for this file to detect if chef
  client has been uninstalled. Setting it to Chef's `Gem.ruby` should
  work. Setting to `null` disables the check.

### Environment Variables

#### `DEBUG`

Setting `DEBUG=1` will enable logging of HTTP request data.

#### `INTERVAL`

By default, the liveness agent will send an update every 30 minutes.
Setting the `INTERVAL` variable will configure the agent to send an
update to the specified value (in seconds).

#### `RUBYOPT`

This application is designed to run with rubygems disabled. This can be
done by setting `RUBYOPT` like so:

```
RUBYOPT="--disable-gems"
```

## Development

This project is developed as a typical ruby app with bundler and rspec.

To install deps:

```
bundle install
```

To run tests:

```
bundle exec rspec
```

## Contributing

Bug reports should be filed with your support representitive.

