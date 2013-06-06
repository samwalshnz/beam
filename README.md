# Beam

Beam is a command line utility for deploying websites to servers. Its basic function is the synchronization of files between a version control system and a host + location. It can also be configured to run commands to further automate the deployment process. Beam works best using `rsync` over `ssh`, though it also has support for intelligent deployment through SFTP and FTP.

## Installation

Download the [`beam.phar`](http://beam.heyday.net.nz/beam.phar) file and store it somewhere on your computer.

#### With `wget`:

    $ sudo wget http://beam.heyday.net.nz/beam.phar -O /usr/local/bin/beam

#### With `curl`:

    $ sudo curl http://beam.heyday.net.nz/beam.phar -o /usr/local/bin/beam

then:

    $ sudo chmod +x /usr/local/bin/beam


## Updating

    $ beam self-update

## Usage

### [Configuration](CONFIG.md)

Each project you intend to use `beam` with requires a `beam.json` configuration file.

#### Basic `beam.json`

```json
{
	"servers": {
		"live": {
			"user": "user",
			"host": "host",
			"webroot": "/path"
		}
	}
}
```

#### Config generation

```bash
$ beam genconfig
```

### Examples

```bash
$ beam up live                   # regular sync from git
$ beam up live --dry-run         # don't offer to sync the files, just display changes
$ beam up live --no-prompt       # skips the summary of files to be changed and doesn't prompt for confirmation
$ beam up live -v                # verbose (see the output of commands)
$ beam up live --no-delete       # don't delete files on target that are not present on local
$ beam up live -p somepath       # only sync the specified path
$ beam up live --command-prompt  # prompt on non-required commands
$ beam up live -t sometag        # include commands tagged with "sometag"
$ beam up live --working-copy    # sync from the working-copy not a vcs archive
$ beam up live -r HEAD~2         # sync 2 back from HEAD
$ beam up live -r def3c6d57      # sync a specific commit
$ beam down live                 # dowload from live to working copy
```

## Unit testing

    $ composer install --dev
    $ phpunit