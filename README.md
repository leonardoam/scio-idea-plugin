# Scio IDEA plugin

[![Build Status](https://img.shields.io/github/workflow/status/spotify/scio-idea-plugin/CI)](https://github.com/spotify/scio-idea-plugin/actions?query=workflow%3ACI)
[![GitHub license](https://img.shields.io/github/license/spotify/scio-idea-plugin.svg)](./LICENSE)

Scio plugin for IDEA, enables BigQuery macro support in IDEA.

# Raison d'être

Due to issue [SCL-8834](https://youtrack.jetbrains.com/oauth?state=%2Fissue%2FSCL-8834) case classes generated by
`@BigQueryType.fromTable` or `@BigQueryType.fromQuery` etc, are not recognized in IntelliJ IDEA. This plugin
exists to mitigate this issue. Should SCL-8834 get fixed, this plugin should be obsolete.

# Install

Inside IntelliJ, `Preferences` -> `Plugins` -> `Browse repositories ...` and search `Scio`.

## Build locally:

```bash
sbt packagePlugin
```

Zipped and ready to install plugin is inside `target`.
To install, inside IntelliJ: `Preferences` -> `Plugins` -> `Install plugin from disk`

# Usage

Install following instructions above. Plugin should work out of the box.

## BigQuery location

If you get the location (EU/US) error - you need to add location setting to scala compiler in your IntelliJ.
The easiest way is to click on the weird looking "clock" in the bottom-right corner - it's actually a shortcut to scala compiler.
If it's already running - stop it, then press `Configure...` and in `JVM parameters` add `-Dbigquery.staging_dataset.location=EU`.

You should upgrade Scio to version >= `0.2.1` - starting from that version `bigquery.staging_dataset.location` is obsolete.

## User interaction

If Scio plugin can't find scala files, it will log an error via IntelliJ Event Log, which you should see via red bubble
in the lower-right corner. The message should inform you that, you need to recompile the project. Follow the instructions.

If you rebuild the project, plugin should react in a matter of seconds - if completion is still not there,
poke the code around, wait a minute or two. At this point plugin simply reacts to IntelliJ events,
which sporadically take a while to propagate.

# Logging

This pluging uses IDEA diagnostic logger, you can find log files
under standard IntelliJ directory ([doc](https://intellij-support.jetbrains.com/hc/en-us/articles/206544519-Directories-used-by-the-IDE-to-store-settings-caches-plugins-and-logs)). For example for macOS: `~/Library/Logs/<PRODUCT><VERSION>/idea.log`.

If there is error level message logged, it will show up in IntelliJ Event Log.

# License

Copyright 2019 Spotify AB.

Licensed under the Apache License, Version 2.0: http://www.apache.org/licenses/LICENSE-2.0
