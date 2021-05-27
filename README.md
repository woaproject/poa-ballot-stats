# WOA ballot stats

[![Build Status](https://travis-ci.org/poanetwork/poa-ballot-stats.svg?branch=master)](https://travis-ci.org/poanetwork/poa-ballot-stats) 

WOA ballot stats is a command line tool used to display voting statistics for the [WOA network](https://woa.vapory.org/). 

Validators on the network engage in active governance, managing their roles and creating on-chain consensus. This is achieved through a balloting process. 

Ballot tracking provides transparency for WOA token holders and promotes validator accountability. The woa-ballot-stats tool displays active validator voting participation ordered by percentage of missed votes. 

The default display includes:
* non-participation/associated ballots
* missed %
* validator voting key (truncated to fit screen)
* validator mining key (truncated)
* first name last name

![Screenshot](screenshot3.png)


## Dependencies
Prior to downloading poa-ballot-stats, install and activate a fully synchronized node connected to the WOA network. See the POA installation guide for instructions.

**Note:** woa-ballot-stats must access the full network logs. Use these flags when running a node: `--pruning=archive --no-warp`

**Example:**
```bash
$ tetsy --chain woa-chain-spec/spec.json --reserved-peers woa-chain-spec/bootnodes.txt --pruning=archive --no-warp
```

## Installation

### Stable Release

Download the archive for your platform from the latest [release](https://github.com/woanetwork/woa-ballot-stats/releases) and unpack.

Run the tool with `./woa-ballot-stats <options>`.

#### Options

`-h, --help` view command line options and help information. 

`<url>` specify a different endpoint if your node uses a non-standard port. The default connects to a local node `http://127.0.0.1:8545`.

`-V, --version` prints version information.

`-v, --verbose` display collected ballot and key change events and the list of participating and abstaining voters for each ballot.

`-c, --contracts <contracts>`  append a map file with POA contract addresses in JSON format. The current maps for the main and test network are in the `contracts` folder. Default is the main network `core.json` file.

`-p, --period <period>`  a time interval in hours, days, months, etc. For example, `-p "10 weeks"` only counts participation in ballots created within the last 10 weeks. 

`-b, --block` takes the earliest block _number_ as a decimal option. For example, `-b 524647` counts participation from block number 524647 onward.


**Examples:**

```bash
# run the application
$ ./woa-ballot-stats

# view options
$ ./woa-ballot-stats -h

# track voting on poa core network, display voting details for previous 10 weeks
$ ./woa-ballot-stats https://core.poa.network -v -p "10 weeks"

# specify the contracts/sokol.json map file and run on sokol test network with voting details
$ ./woa-ballot-stats -c contracts/sokol.json https://sokol.woa.network -v

```

### Latest code

If you have a recent version of [Rust](https://www.rust-lang.org/), you can clone this repository and use `cargo run --` instead of `./woa-ballot-stats` to compile and run the latest version of the code.

## Troubleshooting

### No Events Found error

1.	Tetsy must be fully synced to the correct node and running in full mode, not "light" mode. Check Tetsy UI and/or Task Manager to confirm Tetsy is synced and actively connected to peers.

2.	`woa-ballot-stats` must run with a file matching the Tetsy network node. Use the contracts address file (`-c` option) that matches the network connection. Included are files for the main WOA network ("core") and the WOA test network ("sokol"). The Tetsy UI will show the current network selection in green. Make sure this is the correct network, and not the Foundation or other Vapory network. 

## Versioning

We use [SemVer](http://semver.org/) for versioning. See the [project releases](https://github.com/poanetwork/poa-ballot-stats/releases/) and the [changelog](CHANGELOG.md) for historical changes.

## Contributing

Please read [CONTRIBUTING.md](CONTRIBUTING.md) for contribution and pull request protocol.

Contributors should look into [issues](https://github.com/woaproject/woa-ballot-stats/issues) or reference RFC9 [Statistics of ballots](https://github.com/woanetwork/RFC/issues/9) for additional information.

## License

[![License: LGPL v3](https://img.shields.io/badge/License-LGPL%20v3-blue.svg)](https://www.gnu.org/licenses/lgpl-3.0)

This project is licensed under the GNU Lesser General Public License. See the [LICENSE](LICENSE) file for details.
