[![Test](https://github.com/morphy2k/rss-forwarder/actions/workflows/test.yml/badge.svg)](https://github.com/morphy2k/rss-forwarder/actions/workflows/test.yml)
[![](https://meritbadge.herokuapp.com/rss-forwarder)](https://crates.io/crates/rss-forwarder)

# RSS Forwarder

Checks RSS feeds for new entries and forwards them to different targets (sinks), like webhooks.

## Supported sinks

| Sink        | Type value     |
| ------------| :-------: |
| [Discord](#discord-sink) | `discord` |

## Usage

```TXT
USAGE: rss-forwarder [OPTIONS] <CONFIG_FILE>

OPTIONS:
--debug             Enables debug mode
-h, --help          Show help information
-v, --version       Show version info
```

## Configuration

The feed configuration is passed as a TOML file.

### Feed

| Field        | Type           | Description  |
| ------------- |:-------------:| ----- |
| `url`      | string | URL to the RSS feed |
| `interval`      | string      |   **(optional)** Specifies the time interval between checks. E.g. `10m`, `3h`, `1d`. |
| `sink` | object | Sink options |

### Discord Sink

| Field        | Type           | Description  |
| ------------- |:-------------:| ----- |
| `type` | string | Sink type |
| `url` | string | Discord webhook url |

### Example

```TOML
# Feed 1
[feed.nyt-world]
url = "https://rss.nytimes.com/services/xml/rss/nyt/World.xml"
interval = "10m"
sink.type = "discord"
sink.url = "https://discord.com/api/webhooks/84175.../OZdejNBCL1..."

# Feed 2
[feed.rust-blog]
url = "https://blog.rust-lang.org/feed.xml"
interval = "1m"

[feed.rust-blog.sink]
type = "discord"
url = "https://discord.com/api/webhooks/84175.../OZdejNBCL1..."
```