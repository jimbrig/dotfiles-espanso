# Espanso <img align="right" syle='float' href='https://user-images.githubusercontent.com/32652297/139356362-d02ef475-1b0e-4b73-9d9c-7b7e147cb426.png' src='https://user-images.githubusercontent.com/32652297/139356362-d02ef475-1b0e-4b73-9d9c-7b7e147cb426.png' />

> **Note**:
> *My personal [Espanso](https://espanso.org/) text expander configuration files and setup.*

*This repository is a part of my [dotfiles]().*

***

<center>


<!--Start:Badges-->
[![Generate Changelog](https://github.com/jimbrig/espanso/actions/workflows/changelog.yml/badge.svg)](https://github.com/jimbrig/espanso/actions/workflows/changelog.yml)
<!--End:Badges-->

[Espanso Website](https://espanso.org/) | [EspansoHub](https://hub.espanso.org/) | [Documentation](https://espanso.org/docs/get-started/) | [Reddit Community](https://www.reddit.com/r/espanso/) | [GitHub](https://github.com/federico-terzi/espanso)

</center>

***

## Contents

<!-- TOC -->

- [Contents](#contents)
- [What is espanso?](#what-is-espanso)
    - [What is a Text Expander?](#what-is-a-text-expander)
    - [Key Features](#key-features)
- [Setup](#setup)
    - [Installation](#installation)
    - [Configuration](#configuration)
        - [File Structure](#file-structure)
- [User Configuration](#user-configuration)
- [Matches](#matches)
- [Packages](#packages)
- [Editing](#editing)
- [Toggle](#toggle)
- [Application Specific](#application-specific)
- [Resources](#resources)

<!-- /TOC -->


## What is `espanso`?

[Espanso](https://espanso.org/) is an Open Source, Cross-Platform Text Expander tool written in Rust.

### What is a Text Expander?

A *text expander* is a program that detects when you type a specific **keyword** and replaces it with **something else**.

This is useful in many ways, including but not limited to:

- **Save a lot of typing**, expanding common sentences.
- Create **system-wide** code snippets.
- Execute **custom scripts**
- Use **emojis** like a pro.

### Key Features

* Works on **Windows**, **macOS** and **Linux**
* Works with almost **any program**
* Works with **Emojis** 😄
* Works with **Images**
* Includes a powerful **Search Bar** 🔎
* **Date** expansion support
* **Custom scripts** support
* **Shell commands** support
* **App-specific** configurations
* Support [Forms](https://espanso.org/docs/matches/forms/)
* Expandable with **packages**
* Built-in **package manager** for [espanso hub](https://hub.espanso.org/)
* File based configuration
* Support Regex triggers
* Experimental Wayland support

## Setup

### Installation

Install using your preferred package manager:

- `winget`
- `chocolatey`
- `scoop`

```powershell
# winget
winget install FedericoTerzi.espanso

# chocolatey
sudo choco inst -y espanso

# scoop
scoop install espanso
```

`espanso` should launch at startup, but to check run `espanso status`, and if it says *`espanso is not running`* then run *`espanso start`*.

### Configuration

`espanso` uses a file-based configuration approach. Simply run `espanso path` to determine the configuration folder's path.

On Widows, the default path is `%APPDATA%\espanso`, and the configuration files are split into two folders:

- [`config`](./config/): Contains the main configuration file, `default.yml`, and any other configuration files.
- [`match`](./match/): Contains the *match* files, which are YAML files that contain the actual text expansions along with any installed packages.

#### File Structure

```text
├───config
│       default.yml
│
└───match
    │   about.yml
    │   address.yml
    │   base.yml
    │   datetime.yml
    │   dev.yml
    │   emails.yml
    │   excel.yml
    │   git.yml
    │   links.yml
    │   passwords.yml
    │   phones.yml
    │   secrets.yml
    │
    └───packages
        ├───docker-compose
        ├───get-ip
        ├───lorem
        ├───markdown-shortcuts
        ├───rand-tools
        └───wttr
```

## User Configuration

My personal configuration file, [`default.yml`](./config/default.yml), is located in the [`config`](./config/) folder.

See [User Configuration](https://espanso.org/docs/user-configuration/) for more information.

Currently the only settings I specify are:

```yaml
toggle_key: ALT
search_shortcut: ALT+SHIFT+SPACE
search_trigger: ":search"
show_icon: true
```

## Matches

The [`match`](./match/) folder contains the *match* files, which are YAML files that contain the actual text expansions.

I have organized my match files into various categories:

- [`about.yml`](./match/about.yml): About me
- [`address.yml`](./match/address.yml): Addresses
- [`base.yml`](./match/base.yml): Base expansions
- [`datetime.yml`](./match/datetime.yml): Date and time expansions
- [`dev.yml`](./match/dev.yml): Development related expansions
- [`emails.yml`](./match/emails.yml): Email addresses
- [`excel.yml`](./match/excel.yml): Excel related expansions
- [`git.yml`](./match/git.yml): Git related expansions
- [`links.yml`](./match/links.yml): Links
- [`passwords.yml`](./match/passwords.yml): Passwords [^1]
- [`phones.yml`](./match/phones.yml): Phone numbers
- [`secrets.yml`](./match/secrets.yml): Secrets [^1]


[^1]: Passwords and secrets files are encrypted via [`git-crypt`]().

## Packages

The [`packages`](./match/packages/) folder contains the *packages* that I have installed.

See [Packages](https://espanso.org/docs/packages/) for more information.

Currently, I have the following packages installed:

- [`docker-compose`](https://hub.espanso.org/packages/docker-compose/)
- [`get-ip`](https://hub.espanso.org/packages/get-ip/)
- [`lorem`](https://hub.espanso.org/packages/lorem/)
- [`markdown-shortcuts`](https://hub.espanso.org/packages/markdown-shortcuts/)
- [`rand-tools`](https://hub.espanso.org/packages/rand-tools/)
- [`wttr`](https://hub.espanso.org/packages/wttr/)


## Editing

For quick editing of espanso scripts run `espanso edit`.

## Toggle

To toggle `espanso`'s runtime simply double-tab the `Alt` key. This makes it useful to temporarily disable then re-enable the service.

## Application Specific

Use the `filter_title` configuration variable to specify expansions that should only apply in windows with a title of the provided value. For example, to only match and trigger the below expansion in Outlook you would use:

```yaml
filter_title: "Outlook"
matches:
    - trigger: ":signature"
      replace: "Jimmy Briggs"
```

The following table lays out all possible `filter_*` configurations:

| Filter         | Description                                             | Windows Support                              | MacOS Support                                       | Linux Support   |
| -------------- | ------------------------------------------------------- | -------------------------------------------- | --------------------------------------------------- | --------------- |
| `filter_title` | Filter based on the current Window title                | Full support                                 | Uses the App identifier instead of the Window title | Full support    |
| `filter_exec`  | Filter based on the current application executable path | Full support                                 | Full support                                        | Partial support |
| `filter_class` | Filter based on the current Window class                | Uses the application executable path instead | Uses the App identifier instead                     | Full support    |

***

## Resources
