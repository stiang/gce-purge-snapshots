# *NOTE:* This script has not been converted from [stiang/ec2-purge-snapshots](https://github.com/stiang/ec2-purge-snapshots) yet

# gce-purge-snapshots

## What is it?

A command-line tool that lets you purge (delete) Google Compute 
Engine snapshots according to rules you set up. 

For example, 

    ./gce-purge-snapshots -v all -h 48 -d 14 -w 4 -m 24

means "keep every snapshot on all volumes for 48 hours, one 
per day for two weeks, one per week for four weeks, one per 
month for two years - delete everything else".

The idea is that you have another job which takes a snapshot, 
say, every hour, then run this script periodically to clean up.

## Usage

    Usage: ./gce-purge-snapshots [options]

    Deletes ALL snapshots (for the volumes specified) that do not
    match the rules below. Rules are applied in the following order:

        hours -> days -> weeks -> months

    MANDATORY options (one of -v or -t must be used):
        -v, --volumes VOL1,VOL2,...      Comma-separated list (no spaces) of volume-ids,
                                         or 'all' for all volumes
        -t, --tag KEY=VALUE              Tag to use to filter the snapshot. May specify multiple tags.

    MANDATORY rules:
        -h, --hours HOURS                The number of hours to keep ALL snapshots
        -d, --days DAYS                  The number of days to keep ONE snapshot per day
        -w, --weeks WEEKS                The number of weeks to keep ONE snapshot per week
        -m, --months MONTHS              The number of months to keep ONE snapshot per month

    OPTIONAL options:
        -n, --noop                       Don't actually delete, but print what would be done
        -q, --quiet                      Print deletions only
        -s, --silent                     Print summary only
            --no-summary                 Don't print summary
        -x, --extremely-silent           Don't print anything unless something goes wrong
            --help                       Show this message

## Contribute
Please fork and add pull requests if you would like to improve this package.

## Author
[Stian Grytøyr][1]

[1]: http://stian.grytoyr.net/about/
