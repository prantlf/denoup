# Deno Upgrader and Version Manager

Upgrades to the latest version of Deno, or manages more versions of Deno on the same machine, supporting all platforms, as simple es `rustup`.

* Small. Written in `bash`, easily extensible.
* Fast. Downloads and unpacks pre-built binary builds.
* Portable. Writes only to the user home directory.
* Simple. Switches the version globally, no environment variable changes needed.
* Efficient. Just run `denoup up`.

Platforms: `darwin-x86_64`, `darwin-aarch64`, `linux-x86_64`, `linux-aarch64`, `windows-x86_64`.

## Getting Started

Make sure that you have `bash` 4 or newer and `curl` available, execute the following command:

    curl -fSs https://raw.githubusercontent.com/prantlf/denoup/master/install.sh | bash

Install the latest LTS version of Deno, if it hasn't been installed yet:

    denoup install lts

Before you continue, make sure that you have the following tools available: `curl`, `jq`, `ln`, `rm`,  `uname`, `unzip`. It's likely that `jq` will be missing. You can install it like this on Debian: `apt-get install -y jq`.

Upgrade both the installer script and the Deno language (to the latest LTS version), if they're not up-to-date, and delete the previously active latest LTS version from the disk too:

    denoup up lts

If you specify `latest` instead of `'lts`, the latest non-LTS version will apply.

## Installation

Make sure that you have `bash` 4 or newer and `curl` available, execute the following command:

    curl -fSs https://raw.githubusercontent.com/prantlf/denoup/master/install.sh | bash

Both the `denoup` and `deno` should be executable in any directory via the `PATH` environment variable. The installer script will modify the RC-file of the shell, from which you launched it. The following RC-files are supported:

    ~/.bashrc
    ~/.zshrc
    ~/.config/fish/config.fish

If you use other shell or more shells, update the other RC-files by putting both the installer directory and the Deno binary directory to `PATH`, for example:

    $HOME/.denoup:$HOME/.deno/bin:$PATH

Start a new shell after the installer finishes. Or extend the `PATH` in the current shell as the instructions on the console will tell you.

## Locations

| Path        | Description                                              |
|:------------|:---------------------------------------------------------|
| `~/.denoup` | directory with the installer script and versions of Deno |
| `~/.deno`   | symbolic link to the currently active version of Deno    |

For example, with the Deno 20.16.0 activated:

    /home/prantlf/.denoup
      ├── 2.0.0   (linked to /home/prantlf/.deno)
      ├── 1.46.3  (another version)
      └── denoup  (installer script)

## Usage

    denoup <task> [version]

    Tasks:

      current              print the currently selected version of Deno
      latest               print the latest version of Deno for download
      local                print versions of Deno ready to be selected
      remote               print versions of Deno available for download
      update               update this tool to the latest version
      upgrade              upgrade Deno to the latest and remove the current version
      up                   perform both update and upgrade tasks
      install <version>    add the specified or the latest version of Deno
      uninstall <version>  remove the specified version of Deno
      use <version>        use the specified or the latest version of Deno
      help                 print usage instructions for this tool
      version              print the version of this tool

You can enter just `MAJ` or `MAJ.MIN` as `<version>`, instead of the full `MAJ.MIN.PAT`. When using the `install` or `use` tasks, the *most* recent full version that starts by the entered partial version will be picked. When using the `uninstall` task, the *least* recent full version that starts by the entered partial version will be picked.

## Debugging

If you enable `bash` debugging, every line of the script will be printed on the console. You'll be able to see values of local variables and follow the script execution:

    bash -x denoup ...

You can debug the installer too:

    curl -fSs https://raw.githubusercontent.com/prantlf/denoup/master/install.sh | bash -x

## Platform Detection

### Environment Variables

The following environment variables can be set before running `install.sh` or `denoup`, if you know what you're doing:

| Variable       | Default value                 |
|:---------------|:------------------------------|
| `PLATFORM`     | detected using `uname`        |
| `OS`           | part of `PLATFORM` before `-` |
| `ARCH`         | part of `PLATFORM` after `-`  |
| `INST_DIR`     | `$HOME/.denoup`               |
| `TOOL_DIR`     | `$HOME/.deno`                 |

## Contributing

In lieu of a formal styleguide, take care to maintain the existing coding style. Lint and test your code.

## License

Copyright (c) 2024 Ferdinand Prantl

Licensed under the MIT license.
