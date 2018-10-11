
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

Once downloaded, extract to wherever you like start the Stellite daemon with ZeroNet and IPFS enabled.

__Windows__

Run `stellited-zeronet.bat` by double-clicking

__Linux and MacOS__

`./stellited --zeronet`

*You may also set other flags like `--data-dir` if you like*

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

## Second test

While keeping your daemon running, [install IPFS](https://ipfs.io/docs/install/) but do **not** run ipfs init

The daemon has already initialised IPFS and runs the IPFS daemon. You can now interact with it.

The daemon uses it's own IPFS root path and needs to be set when you wish to interact with IPFS using the daemon. You need to set the environment variable `IPFS_PATH` to `you-stellite-datadir/ipfs`. On Linux and Mac it defaults to `~/.stellite` and on Windows usually under `c:\ProgramData\stellite\ipfs`.

Try running the following IPFS command:

__Windows Command line__
```
set IPFS_PATH=c:\ProgramData\stellite\ipfs
ipfs cat QmZ6Rdf5fiemr34Dn2mpo7ydAoBrSUPP37R36183EZn7HL
```

__Windows PowerShell__
```
$env:IPFS_PATH = 'c:\ProgramData\stellite\ipfs'
ipfs cat QmZ6Rdf5fiemr34Dn2mpo7ydAoBrSUPP37R36183EZn7HL
```

__Linux and MacOS__ 
```
IPFS_PATH=~/.stellite/ipfs ipfs cat QmZ6Rdf5fiemr34Dn2mpo7ydAoBrSUPP37R36183EZn7HL
```

This should print `Hi! This file was fetched from IPFS via the Stellite daemon!`

## Third test

Add a file to IPFS and have someone else fetch it.

Create a new text file and add any content to it. Then, using `ipfs add <filename>` add it to IPFS. You will receive a hash that looks something like `added QmegHcnrPgMwC7tBiMxChD54fgQMBUecNw9nE9UUU4x1bz newfile.txt`. Post this hash in our [Discord #alpha-ipfs-zeronet-wallet-integration](https://discord.gg/8PhF342) and someone else will attempt to fetch it over IPFS. You'll need to keep your daemon running until someone else fetches it.

To fetch content added by someone else, simply use `ipfs get <hash>` to retrieve the file. Let the person who uploaded the file know what you received in the #alpha-ipfs-zeronet-wallet-integration channel.

You can also use the public IPFS.io gateway to check the content you added by opening `https://ipfs.io/ipfs/<YOUR HASH>` in your browser. It might take some time to get the content on the first fetch.

*Note: it doesn't have to be text, can pretty much be anything. Text is just simpler to verify*

## Fourth test, for the adventurous

If you are feeling up to it, you can build the following from source:

1. libznipfs - Our library for interacting with ZeroNet and IPFS
2. Stellite with libznipfs support

__libznipfs__

You can follow the build instructions in the [README](https://github.com/stellitecoin/libznipfs/blob/master/README.md)

__Stellite__

You can follow the build instructions in the [README](https://github.com/stellitecoin/Stellite/blob/zeronet-ipfs/README.md)


## Thanks for testing!

Any problems or issues can be reported by opening a new [issue](https://github.com/stellitecoin/Stellite/issues/new?title=IPFS-Zeronet%20Testing&body=Please%20include%20your%20operating%20system%20version%20and%20complete%20explanation%20and%20output%20of%20the%20problem). Please include your operating system version and complete explanation and output of the problem.
