# mid2chart
Rock Band/Phase Shift .mid to GH3PC/FeedBack .chart file converter

## Description
This is a tool made to convert Rock Band / Phase Shift .mid files to .chart, so they can be imported into GH3PC using GHTCP.

If the midi file has tap notes - such as the Phase Shift version of GH:WT> songs - it'll output 2 charts: a (Dummy).chart one, and the actual .chart. To properly import those, please refer to [this tutorial](https://youtu.be/We0E4iyKJ1M?t=13m53s) by Plumato.

To make sure tap notes work, you should use ExileLord's [GH3+](https://youtu.be/EbapUSs5fsg) hack.

You can find the changelog and pre-GitHub versions [here](CHANGELOG.md).

## Usage
Drag and drop the mid file into "mid2chart.exe" or the .bat included. (The .mid file must be in the same folder of the .bat if you're using it.)

If there is a song.ini file in the same folder as the mid, the converter will use its metadata to set the song name, artist, year, charter and offset attributes in the converted chart file.

If the song.ini specifies a 1/8 HO/PO threshold, the converter will force HO/POs accordingly so the converted chart file matches that.

PART KEYS is also converted, placed in the Enhanced Guitar part. It is ignored by GHTCP, but can be found by opening the chart in FeedBack and pressing F4.

## Parameters
* Use the -e parameter to output editable FeedBack files (since forced HO/POs, forced strums and tap notes aren't supported and dB crashes when it reads one of those). In this case, forced hopo/strums will become a * track event, and tap notes, a T track event. 
* Use the -r parameter to use Rock Band/Harmonix's HO/PO logic, which is slightly different from the regular (a single note after a chord will be a strum if the previous chord contains such note).
* Use the -b parameter to bypass broken chord adaptation and leave them as they are (if there are any).
* Use the -f parameter if some notes aren't being properly forced. Be aware, though, that this might force some notes unproperly.").
* Use the -s parameter if some notes aren't in their proper star power sections. Be aware, though, that this might put some notes unproperly in star power sections.").
* Use the -u parameter to unforce NAudio's strict midi checking. This might help if NAudio throws an error when trying to open a midi file, but might cause inaccuracies in the conversion.
* Use the -d parameter to remove double HO/POs.
* Use the -c parameter to avoid forcing chords (useful for non-GH3+ users or console players).
* Use the -t parameter to convert tap notes as forced HO/POs instead (useful for non-GH3+ users or console players).
* Use the -o parameter to clip sustains and/or fix overlapping notes.
* Use the -8 parameter to set 1/8 notes as HO/POs, OR to set it back to default if the .ini file already specifies such condition.
* Use the -16 parameter to set 1/16 notes as strums, OR to set it back to default if the .ini file already specifies such condition.
* Use the -1 parameter to check midi note 103 for star power, instead of 116.
* Use the -m parameter to NOT create a (Dummy).chart file.
* Use the -k parameter to close the program after the conversion, instead of waiting for a keystroke.
* Use the -p parameter to read and write open notes (as N 7 0 or E O).
* Use the -os parameter to force open notes as strum by default, unless forced otherwise. (useless without -p).
* Use the -kb parameter to swap keys and bass when converting the midi.
* Use the -kg parameter to swap keys and guitar when converting the midi.
* Use the -gb parameter to swap guitar and bass when converting the midi.

Be aware that you can only use ONE of the track swapping parameters. If you use more than one, only the first one entered will be considered.
To easily add those parameters, edit the .bat file and drag/drop the .mid file into it.

## Troubleshooting
If you're having problems with notes not being properly forced and the -f/-s parameters don't help, try opening the .mid in EoF, going into Settings and setting Min. note length (ms) as 18, resaving the project and converting the resaved .mid (thanks ScoreHero user "Notyu1459" for this solution).

If the converter doesn't read the midi properly (it gives an error after the Program Started! line), try using the -u parameter. If that doesn't work, try resaving it with a midi editing software (REAPER, Anvil Studio or Sekaiju, for instance).

If you have any other issues, just send a message to raphaelgoulart#1573 on Discord.

## License
This software is released under the [MIT license](LICENSE). You're free to use it and modify it as you will, as long as you read and agree with its license.

## Credits and Special Thanks
This software uses [NAudio](https://github.com/naudio/NAudio/), released under the Ms-PL license, and unphook's [Stopwatch.cs](https://github.com/unphook/rock-porra/blob/master/forfopacker/Stopwatch.cs), released under the MIT license.

Special thanks to Plumato and the579GH for the testing, suggestions, help and support provided.
