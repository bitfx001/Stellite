
# Stellite Zeronet/IPFS integration alpha testing

We've reached a stage where we'd like to start testing the ZeroNet
and IPFS integration with a wider test group.

The integration fetches the seed list from ZeroNet and IPFS when the daemon is
started. The daemon runs as a full IPFS node as well, it is compatible
with the standard IPFS tools meaning you can interact with IPFS whenever
your Stellite daemon is running.

## First test

The first test only requires you to download and run the precompiled daemons.

The precompiled versions can be downloaded for each platform:

1. [Windows](https://www.stellite.live/downloads/stellite-zeronet-ipfs-win.zip)
2. [MacOS](https://www.stellite.live/downloads/stellite-zeronet-ipfs-mac.tar.gz)
3. [Linux](https://www.stellite.live/downloads/stellite-zeronet-ipfs-linux.tar.gz)

Once downloaded, extract to wherever you like and run `stellited --zeronet`(1). This will start the Stellite daemon with ZeroNet/IPFS enabled.

You should see output similar to, only 3 seeds should be loaded:

```
.... Fetching seed list from ZeroNet/IPFS...
.... Fetched the seed list from ZeroNet/IPFS
.... Added seed from ZeroNet/IPFS: 185.91.116.196:20188
.... Added seed from ZeroNet/IPFS: 185.91.116.136:20188
.... Added seed from ZeroNet/IPFS: 185.91.116.164:20188
```

If you see the following error
`Unable to start IPFS node: IPFS API: manet.Listen(/ip4/127.0.0.1/tcp/5001) failed`. Please stop your own IPFS daemon first.

(1) You may also set other flags like `--data-dir` if you like


## Second test

While keeping your daemon running, [install IPFS](https://ipfs.io/docs/install/) but do **not** run ipfs init

The daemon has already initialised IPFS and runs the IPFS daemon. You can now interact with it.

The daemon uses it's own IPFS root path and needs to be set when you wish to interact with IPFS using the daemon. You need to set the environment variable `IPFS_PATH` to `you-stellite-datadir/ipfs`. On Linux and Mac it defaults to `~/.stellite` and on Windows usually under `c:\ProgramData\stellite\ipfs`.

Try running the following IPFS command:

`IPFS_PATH=~/.stellite/ipfs ipfs cat QmZ6Rdf5fiemr34Dn2mpo7ydAoBrSUPP37R36183EZn7HL`

This should print `Hi! This file was fetched from IPFS via the Stellite daemon!`

## Third test, for the adventurous

If you are feeling up to it, you can build the following from source:

1. libznipfs - Our library for interacting with ZeroNet and IPFS
2. Stellite with libznipfs support

__libznipfs__

You can follow the build instructions in the [README](https://github.com/stellitecoin/libznipfs/blob/master/README.md)

__Stellite__

You can follow the build instructions in the [README](https://github.com/stellitecoin/Stellite/blob/zeronet-ipfs/README.md)


## Thanks for testing!

Any problems or issues can be reported by opening a new [issue](https://github.com/stellitecoin/Stellite/issues/new?title=IPFS-Zeronet%20Testing&body=Please%20include%20your%20operating%20system%20version%20and%20complete%20explanation%20and%20output%20of%20the%20problem). Please include your operating system version and complete explanation and output of the problem.
