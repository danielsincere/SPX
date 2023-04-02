# SPX

SPX is a Swift script running tool. Easily run Swift packages in a supporting relative dir named `SPX`

SPX pairs nicely with [Sh](https://github.com/FullQueueDeveloper/Sh) to run shell commands and process shell output from your Swift scripts.

For a full example of using SPX, [Sh](https://github.com/FullQueueDeveloper/Sh), and [ShXcrun](https://github.com/FullQueueDeveloper/ShXcrun) on your iOS project, please see https://github.com/FullQueueDeveloper/SwishExampleiOSProject

## Motivation

There's currently not a great solution to declare some targets as dev dependencies or support scripts in a `Package.swift`. So what if we had a subdirectory with our Swift support scripts? `$PROJECT_ROOT/support-dir/Package.swift`?

But there's currently not a great solution to running Swift packages in another directory. We can type `swift run --package-path path/to/dir targetName`, but that's a lot for quick scripts. We could store that in a `.sh` script file, but I would prefer not to get shell scripts involved with Swift tools.

And if we're running this script during an Xcode build for an iOS project, we need to pass along an SDK flag, to build the Swift script for MacOS.

This is all doable. And this becomes repetitive across multiple projects.

## Installation

SPX is currently available through [Homebrew](https://brew.sh), [Mint](https://github.com/yonaskolb/Mint), or manual installation.

### Homebrew

Install with [Homebrew](https://brew.sh)

    brew tap fullqueuedeveloper/fullqueuedeveloper
    brew install fullqueuedeveloper/fullqueuedeveloper/spx

### Mint

Install with [Mint](https://github.com/yonaskolb/Mint)

    mint install FullQueueDeveloper/SPX

### Manual

    git clone https://github.com/FullQueueDeveloper/SPX.git
    cd SPX
    swift build -c release

And then add `.build/release/` to your `$PATH`.

## Getting started

    spx --init simple

Will scaffold a new SPX project in the `SPX` subdirectory of your current working directory. This is what it will look like.

    $PWD
     |
     +- SPX
          |
          +- Package.swift
          +- .gitignore
          +- Sources/date/main.swift

Then you can run `spx` or `spx --list` or `spx -l` to see the current executable targets. Then you can run `spx date` to run the simple sample script named `date`.

## Usage

### Regular use

    spx <target-name> [arguments...]

    - <target-name>  The name of the `executableTarget` in the
                                `Package.swift` in the `scripts`
                                subdirectory of the current working
                                directory.
    - [arguments...]  Arguments passed to the target

### Available commands

    spx
        list the available targets

    spx --list
        list the available targets

    spx --version
        show version and exit

    spx --help
        show this message

    spx --init <template-name>
        scaffold a new Swish scripts subdirectory in
        the current directory. The default scripts
        subdirectory is `Swish`.

    spx --add <name>
        add a new script named <name> by
        creating a file at path `Sources/<name>/main.swift`,
        & a file at path `Sources/<Name>Lib/<Name>.swift`,
        & adding their targets to `Package.swift`

    spx --build
        update & build the scripts package, as a convenience.

## iOS template

    spx -i ios

This will create a `SPX` directory with a script to generate an app icon from an SVG (`spx appicon`) and a script to push to the App Store (`spx appstore`). Read more about it at [templates/ios/SPX/README.md](templates/ios/SPX/README.md)

## Demos

There is an example project in the `demos` folder

- The `VaporDemo` is a [Vapor](https://vapor.codes) app. This example is short, but still meaningful. Running `spx docker` from the `demos/VaporDemo` directory will build the docker container for this small vapor app.

- Screenshots. This PR shows the power of using Sh & SPX for scripting. It uses `CoreGraphics` and `AVFoundation` along with `Sh` to take screenshots, and process them for the App Store & for publishing to a website. https://github.com/0xOpenBytes/ios-base/pull/14

- Demo iOS project https://github.com/FullQueueDeveloper/SwishExampleiOSProject
