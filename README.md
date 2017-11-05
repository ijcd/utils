# WordPress Utils

These are odds and ends that I find useful for working with WordPress.

## linuxbrew

Working in the home directory of a hosting provider can feel quite isolated. They don't always
have the best tooling installed, and you don't have root access to improve things.
[Linuxbrew](http://linuxbrew.sh/) is a package manager for your home directory (ported from
brew for OSX). I find it useful:


## sitelock

Wordpress can edit itself. This is a bad idea. I got tired of constantly cleaning up my friend's
installations every time they got script-kiddied. This quick script will set all the files to be
unmodifiable. You can lock and unlock. I leave it locked when it isn't being worked on or updated.

Lock her up:
```
sitelock lock <wp-site-root>
```

Let her go:
```
sitelock unlock <wp-site-root>
```


## dbjson

This script is useful for dumping a database to json files. There is one file per row per table.

```
usage: dbjson [-h] [--site SITE] [--dbhost DBHOST] [--dbuser DBUSER]
              [--dbpass DBPASS] [--dbname DBNAME]

optional arguments:
  -h, --help       show this help message and exit
  --site SITE      Site with database to dump. (If this is specified, the
                   --db* options should not be)
  --dbhost DBHOST  Database hostname.
  --dbuser DBUSER  Database username.
  --dbpass DBPASS  Database password.
  --dbname DBNAME  Database to dump from.
```

The files will be saved as `./dbjson/<table_name>/<primary_key>.json`, one for each row.

This format makes it much easier to diff between updates using `diff -qr` to poke around and see
what people have been doing through the web interface while you've been working locally.


## dbconfig

Parses the database connection information for a WordPress site. Can be used from other scripts or
from the command line.

```
usage: dbconfig [-h] site

positional arguments:
  site        Site root to parse dbconfig from.

optional arguments:
  -h, --help  show this help message and exit
```


## dbcopy

```
usage: dbcopy [-h] source target

positional arguments:
  source      Source site root directory. (database config will be parse from wp-config.php)
  target      Target site root directory. (database config will be parse from wp-config.php)

optional arguments:
  -h, --help  show this help message and exit
```
