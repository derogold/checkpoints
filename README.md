# Checkpoints
### How To Sync Quickly
##### You can sync a fresh chain from 0 much quicker by loading "checkpoints" with your daemon.

### Setup

- Right click [this link](https://github.com/derogold/checkpoints/raw/master/checkpoints.csv.7z) and choose `Save link as...` to download the latest checkpoints.csv.7z file
- Unpack the checkpoints.csv file from the .7z archive
- Place checkpoints.csv in the same folder as your DeroGoldd daemon
- You can get DeroGoldd from here if you don't have it already: https://github.com/derogold/derogold/releases/latest
- Make sure you shut down any GUI wallets, wallet-api endpoints, or any other instances of DeroGoldd you may run before daemon resync..

Alternatively, download the individual files checkpoints.csv-000, checkpoints.csv-001 ... checkpoints.csv-00n and then in the same directory where you downloaded the files do the ```cat checkpoints.csv-000 checkpoints.csv-001 checkpoints.csv-002 > checkpoints.csv``` command to join the files into a single checkpoints.csv file.

### Usage

#### Windows

- First, open a command prompt in the same directory as DeroGoldd.
- This can easily be done by moving to the DeroGoldd directory in Windows Explorer, then typing `cmd` in the search bar and hitting enter:

![Opening cmd](https://i.imgur.com/QoNwYtB.png)
- Finally, type `DeroGoldd.exe --load-checkpoints checkpoints.csv` in the command prompt.

#### Linux, Apple

- First, open a command prompt in the same directory as DeroGoldd.
- You can use the `cd` command to change to this directory. For example, `cd Downloads/DeroGold-v0.6.0`
- Alternatively, your file manager may provide the ability to open a terminal in your current directory. Navigate to the folder with DeroGoldd in, and try right clicking, to see if you can open a terminal there:

![Opening terminal](https://i.imgur.com/Rd5TmQc.png)

- Finally, type `./DeroGoldd --load-checkpoints checkpoints.csv` in the terminal.

### Expected Output

If you did the steps correctly, you should see something like this output.

```
2018-May-13 11:58:39.654478 INFO    Welcome to DeroGold v0.6.0 ()
2018-May-13 11:58:39.654914 INFO    Module folder: DeroGoldd
2018-May-13 11:58:39.655249 INFO    Loading Checkpoints for faster initial sync...
2018-May-13 11:58:40.854979 INFO    Loaded 1235695 checkpoints from checkpoints.csv
```

- DeroGoldd will then start syncing from checkpoints.
- Checkpoints file is for syncing the node / daemon, not your wallet.

### Common Errors

#### Invalid checkpoint file format

```
2018-May-13 12:10:08.325056 INFO    Loading Checkpoints for faster initial sync...
2018-May-13 12:10:08.339667 ERROR   Invalid checkpoint file format
2018-May-13 12:10:08.341758 ERROR   Exception: Failed to load checkpoints
```

- If you see output like the above, the file you are opening is either not a .csv file, or hasn't been downloaded correctly.
- Ensure you downloaded the file by right clicking, and choosing `Save link as...`.
- If you incorrectly chose the wrong file, you can accidentally  download a html page instead.
- When you open up the file, it should have lots of lines like this:

```
0,7fb97df81221dd1366051b2d0bc7f49c66c22ac4431d879c895b06d66ef66f4c
1,8c9738f961a278486f27ce214d1e4d67e08f7400c8b38fe00cdd571a8d302c7d
2,2ef060801dd27327533580cfa538849f9e1968d13418f2dd2535774a8c494bf4
```

- If you absolutely can't get it working, you can make a new text file, copy all the content from here into it: https://github.com/derogold/checkpoints/raw/master/checkpoints.csv
- Then save as checkpoints.csv (Select filetype: all files in windows)

#### Failed to load checkpoints

```
2018-May-13 12:14:57.544286 INFO    Loading Checkpoints for faster initial sync...
2018-May-13 12:14:57.544569 ERROR   Could not load checkpoints file: checkpoints.csv
2018-May-13 12:14:57.544823 ERROR   Exception: Failed to load checkpoints
```

- If you see output like the above, it means the file isn't present in the directory you are in.
- Make sure you have placed the checkpoints.csv file in the same directory as DeroGoldd.

#### DeroGoldd.exe is not recognized / No such file or directory

```
C:\Users\gentoo>DeroGoldd.exe --load-checkpoints checkpoints.csv
'DeroGoldd.exe' is not recognized as an internal or external command,
operable program or batch file.
```

`bash: ./DeroGoldd: No such file or directory`

- If you see output like one of the above, it means your terminal isn't in the same folder as the DeroGoldd program.
- You can type `pwd` to see what folder you are currently in.
- Try following the steps above to get into the right folder, then try again.
- If you type `ls`, you should see the DeroGoldd program, if you are in the correct folder:

```
[DeroGold-v0.1.1] ls
cryptotest  DeroGoldd  DeroGold-service  Dockerfile  miner  morpheus.wallet  wallet-api  zedwallet  zedwallet-beta
```

#### IO error

```
2018-May-13 11:58:40.857058 INFO    Opening DB in /home/dan/.DeroGold/DB
2018-May-13 11:58:40.858174 ERROR   DB Error. DB can't be opened in /home/dan/.DeroGold/DB. Error: IO error: While lock file: /home/dan/.DeroGold/DB/LOCK: Resource temporarily unavailable
2018-May-13 11:58:40.873692 ERROR   Exception: IO error
```

- If you see output like the above, something else has got the database open already.
- Make sure you have closed down any other DeroGoldd's, GUI wallets, and walletd.
- Use a task manager to help you find any which might be running in the background, then try again.
