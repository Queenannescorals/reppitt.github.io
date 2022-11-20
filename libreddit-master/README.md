# Libreddit

> An alternative private front-end to Reddit

![screenshot](https://i.ibb.co/QYbqTQt/libreddit-rust.png)

---

**10 second pitch:** Libreddit is a portmanteau of "libre" (meaning freedom) and "Reddit". It is a private front-end like [Invidious](https://github.com/iv-org/invidious) but for Reddit. Browse the coldest takes of [r/unpopularopinion](https://libreddit.spike.codes/r/unpopularopinion) without being [tracked](#reddit).

- 🚀 Fast: written in Rust for blazing-fast speeds and memory safety
- ☁️ Light: no JavaScript, no ads, no tracking, no bloat
- 🕵 Private: all requests are proxied through the server, including media
- 🔒 Secure: strong [Content Security Policy](https://developer.mozilla.org/en-US/docs/Web/HTTP/CSP) prevents browser requests to Reddit

---

I appreciate any donations! Your support allows me to continue developing Libreddit.

<a href="https://www.buymeacoffee.com/spikecodes" target="_blank"><img src="https://cdn.buymeacoffee.com/buttons/v2/default-yellow.png" alt="Buy Me A Coffee" style="height: 40px" ></a>
<a href="https://liberapay.com/spike/donate"><img alt="Donate using Liberapay" src="https://liberapay.com/assets/widgets/donate.svg" style="height: 40px"></a>


**Bitcoin:** `bc1qwyxjnafpu3gypcpgs025cw9wa7ryudtecmwa6y`

**Monero:** `45FJrEuFPtG2o7QZz2Nps77TbHD4sPqxViwbdyV9A6ktfHiWs47UngG5zXPcLoDXAc8taeuBgeNjfeprwgeXYXhN3C9tVSR`

---

# Instances

🔗 **Want to automatically redirect Reddit links to Libreddit? Use [LibRedirect](https://github.com/libredirect/libredirect) or [Privacy Redirect](https://github.com/SimonBrazell/privacy-redirect)!**

[Follow this link](https://github.com/libreddit/libreddit-instances/blob/master/instances.md) for an up-to-date table of instances in markdown format. This list is also available as [a machine-readable JSON](https://github.com/libreddit/libreddit-instances/blob/master/instances.json).

Both files are part of the [libreddit-instances](https://github.com/libreddit/libreddit-instances) repository. To contribute your [self-hosted instance](#deployment) to the list, see the [libreddit-instances README](https://github.com/libreddit/libreddit-instances/blob/master/README.md).

---

# About

Find Libreddit on 💬 [Matrix](https://matrix.to/#/#libreddit:kde.org), 🐋 [Docker](https://hub.docker.com/r/spikecodes/libreddit), :octocat: [GitHub](https://github.com/libreddit/libreddit), and 🦊 [GitLab](https://gitlab.com/spikecodes/libreddit).

## Built with

- [Rust](https://www.rust-lang.org/) - Programming language
- [Hyper](https://github.com/hyperium/hyper) - HTTP server and client
- [Askama](https://github.com/djc/askama) - Templating engine
- [Rustls](https://github.com/ctz/rustls) - TLS library

## Info
Libreddit hopes to provide an easier way to browse Reddit, without the ads, trackers, and bloat. Libreddit was inspired by other alternative front-ends to popular services such as [Invidious](https://github.com/iv-org/invidious) for YouTube, [Nitter](https://github.com/zedeus/nitter) for Twitter, and [Bibliogram](https://sr.ht/~cadence/bibliogram/) for Instagram.

Libreddit currently implements most of Reddit's (signed-out) functionalities but still lacks [a few features](https://github.com/libreddit/libreddit/issues).

## How does it compare to Teddit?

Teddit is another awesome open source project designed to provide an alternative frontend to Reddit. There is no connection between the two and you're welcome to use whichever one you favor. Competition fosters innovation and Teddit's release has motivated me to build Libreddit into an even more polished product.

If you are looking to compare, the biggest differences I have noticed are:
- Libreddit is themed around Reddit's redesign whereas Teddit appears to stick much closer to Reddit's old design. This may suit some users better as design is always subjective.
- Libreddit is written in [Rust](https://www.rust-lang.org) for speed and memory safety. It uses [Hyper](https://hyper.rs), a speedy and lightweight HTTP server/client implementation.

---

# Comparison

This section outlines how Libreddit compares to Reddit.

## Speed

Lasted tested Nov 11, 2022.

Results from Google PageSpeed Insights ([Libreddit Report](https://pagespeed.web.dev/report?url=https%3A%2F%2Flibreddit.spike.codes%2F), [Reddit Report](https://pagespeed.web.dev/report?url=https://www.reddit.com)).

|                        | Libreddit   | Reddit    |
|------------------------|-------------|-----------|
| Requests               | 60          | 83        |
| Speed Index            | 2.0s        | 10.4s     |
| Time to Interactive    | **2.8s**    | **12.4s** |

## Privacy

### Reddit

**Logging:** According to Reddit's [privacy policy](https://www.redditinc.com/policies/privacy-policy), they "may [automatically] log information" including:
- IP address
- User-agent string
- Browser type
- Operating system
- Referral URLs
- Device information (e.g., device IDs)
- Device settings
- Pages visited
- Links clicked
- The requested URL
- Search terms

**Location:** The same privacy policy goes on to describe that location data may be collected through the use of:
- GPS (consensual)
- Bluetooth (consensual)
- Content associated with a location (consensual)
- Your IP Address

**Cookies:** Reddit's [cookie notice](https://www.redditinc.com/policies/cookies) documents the array of cookies used by Reddit including/regarding:
- Authentication
- Functionality
- Analytics and Performance
- Advertising
- Third-Party Cookies
- Third-Party Site

### Libreddit

For transparency, I hope to describe all the ways Libreddit handles user privacy.

**Logging:** In production (when running the binary, hosting with docker, or using the official instances), Libreddit logs nothing. When debugging (running from source without `--release`), Libreddit logs post IDs fetched to aid with troubleshooting.

**DNS:** Both official domains (`libredd.it` and `libreddit.spike.codes`) use Cloudflare as the DNS resolver. Though, the sites are not proxied through Cloudflare meaning Cloudflare doesn't have access to user traffic.

**Cookies:** Libreddit uses optional cookies to store any configured settings in [the settings menu](https://libreddit.spike.codes/settings). These are not cross-site cookies and the cookies hold no personal data.

**Hosting:** The official instances are hosted on [Replit](https://replit.com/) which monitors usage to prevent abuse. I can understand if this invalidates certain users' threat models and therefore, self-hosting, using unofficial instances, and browsing through Tor are welcomed.

---

# Installation

## 1) Cargo

Make sure Rust stable is installed along with `cargo`, Rust's package manager.

```
cargo install libreddit
```

## 2) Docker

Deploy the [Docker image](https://hub.docker.com/r/spikecodes/libreddit) of Libreddit:
```
docker pull spikecodes/libreddit
docker run -d --name libreddit -p 8080:8080 spikecodes/libreddit
```

Deploy using a different port (in this case, port 80):
```
docker pull spikecodes/libreddit
docker run -d --name libreddit -p 80:8080 spikecodes/libreddit
```

To deploy on `arm64` platforms, simply replace `spikecodes/libreddit` in the commands above with `spikecodes/libreddit:arm`.

To deploy on `armv7` platforms, simply replace `spikecodes/libreddit` in the commands above with `spikecodes/libreddit:armv7`.

## 3) AUR

For ArchLinux users, Libreddit is available from the AUR as [`libreddit-git`](https://aur.archlinux.org/packages/libreddit-git).

```
yay -S libreddit-git
```

## 4) GitHub Releases

If you're on Linux and none of these methods work for you, you can grab a Linux binary from [the newest release](https://github.com/libreddit/libreddit/releases/latest).

## 5) Replit/Heroku/Glitch

**Note:** These are free hosting options but they are *not* private and will monitor server usage to prevent abuse. If you need a free and easy setup, this method may work best for you.

<a href="https://repl.it/github/libreddit/libreddit"><img src="https://repl.it/badge/github/libreddit/libreddit" alt="Run on Repl.it" height="32" /></a>
[![Deploy](https://www.herokucdn.com/deploy/button.svg)](https://heroku.com/deploy?template=https://github.com/libreddit/libreddit)
[![Remix on Glitch](https://cdn.glitch.com/2703baf2-b643-4da7-ab91-7ee2a2d00b5b%2Fremix-button-v2.svg)](https://glitch.com/edit/#!/remix/libreddit)

---

# Deployment

Once installed, deploy Libreddit to `0.0.0.0:8080` by running:

```
libreddit
```

## Change Default Settings

Assign a default value for each setting by passing environment variables to Libreddit in the format `LIBREDDIT_DEFAULT_{X}`. Replace `{X}` with the setting name (see list below) in capital letters.

| Name                    | Possible values                                                                                     | Default value |
|-------------------------|-----------------------------------------------------------------------------------------------------|---------------|
| `THEME`                 | `["system", "light", "dark", "black", "dracula", "nord", "laserwave", "violet", "gold", "rosebox"]` | `system`      |
| `FRONT_PAGE`            | `["default", "popular", "all"]`                                                                     | `default`     |
| `LAYOUT`                | `["card", "clean", "compact"]`                                                                      | `card`        |
| `WIDE`                  | `["on", "off"]`                                                                                     | `off`         |
| `POST_SORT`             | `["hot", "new", "top", "rising", "controversial"]`                                                  | `hot`         |
| `COMMENT_SORT`          | `["confidence", "top", "new", "controversial", "old"]`                                              | `confidence`  |
| `SHOW_NSFW`             | `["on", "off"]`                                                                                     | `off`         |
| `BLUR_NSFW`             | `["on", "off"]`                                                                                     | `off`         |
| `USE_HLS`               | `["on", "off"]`                                                                                     | `off`         |
| `HIDE_HLS_NOTIFICATION` | `["on", "off"]`                                                                                     | `off`         |
| `AUTOPLAY_VIDEOS`       | `["on", "off"]`                                                                                     | `off`         |

### Examples

```bash
LIBREDDIT_DEFAULT_SHOW_NSFW=on libreddit
```

```bash
LIBREDDIT_DEFAULT_WIDE=on LIBREDDIT_DEFAULT_THEME=dark libreddit -r
```

## Proxying using NGINX

**NOTE** If you're [proxying Libreddit through an NGINX Reverse Proxy](https://github.com/libreddit/libreddit/issues/122#issuecomment-782226853), add
```nginx
proxy_http_version 1.1;
```
to your NGINX configuration file above your `proxy_pass` line.

## systemd

You can use the systemd service available in `contrib/libreddit.service`
(install it on `/etc/systemd/system/libreddit.service`).

That service can be optionally configured in terms of environment variables by
creating a file in `/etc/libreddit.conf`. Use the `contrib/libreddit.conf` as a
template. You can also add the `LIBREDDIT_DEFAULT__{X}` settings explained
above.

When "Proxying using NGINX" where the proxy is on the same machine, you should
guarantee nginx waits for this service to start. Edit
`/etc/systemd/system/libreddit.service.d/reverse-proxy.conf`:

```conf
[Unit]
Before=nginx.service
```

## Building

```
git clone https://github.com/libreddit/libreddit
cd libreddit
cargo run
```