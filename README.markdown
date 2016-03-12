Ansible playbook to set up a [Bitcoin Classic](https://bitcoinclassic.com/) node on a linux 14.04 VPS.

I've tested and am running this on a [Linode 4096](https://www.linode.com/?r=79cf79f1e04727f08815960fd3c6379e7871142e).

## Needed:

- Locally:
  - Ansible >= 2.0
  - Ruby 2.0 (Not really *needed*, just adds a few rake tasks to set up the ansible CLI easier)
- Remote:
  - Ubuntu 14.04 VPS with enough diskspace for the blockchain

## Preparation

- 1. Add the IP of the VPS to your ssh config and hosts file as `mybtcnode`
- 2. `ssh-copy-id root@mybtcnode`
- 3. `cp config.sample.json config.json`
- 4. Edit `config.json` to taste

### Config Variables

- `hostname` - What to set the hostname as
- `bitcoin_dir` - Directory to install inside
- `classic_version` - Which version to use
- `rpc_user` - Username
- `rpc_pass` - Password
- `prune_only` - Set to `true` to run in pruned mode, `false` otherwise
- `prune_amt` - Prune setting; ignored unless ^^ is `true`.

### Go!

`rake mybtcnode:setup`

You can also run steps individually:
  - `rake mybtcnode:install_dependencies`  -> Install dependencies
  - `rake mybtcnode:hostname`              -> Set hostname
  - `rake mybtcnode:security`              -> Set up security  
  - `rake mybtcnode:bitcoin_classic`       -> Set up and start bitcoin_classic
  - `rake mybtcnode:get_info`              -> Get node status
