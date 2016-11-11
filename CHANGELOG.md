#Changelog

#### 1.0 (current version) 11/11/2016
Additions:
* Added 1/16 strums support (for songs like Snow ((Hey Oh)))
* Added the -16 parameter, which will set the HO/PO threshold to 1/16 only if the song.ini didn't set it already - if it already did, the -16 parameter will revert it back to the default 1/12.
* Added the -u parameter, which disables NAudio's strict midi file checking. Useful if NAudio throws an error when reading a midi file, but might result in some conversion inaccuracy.

Improvements:
* Updated the NAudio library to the most recent version as of this release's date.

Previous versions were released outside of GitHub and didn't have a proper version name, so I'm identifying them by their release dates.

You can find links for those old versions at the bottom of this file.

#### 01/07/2016
Additions:
* Added the -1 parameter, which reads star power on note 103 instead of 116 (like GH1, 2 or 80s midis).
* Support for "T1 GEMS" track name for GH1 support.
* Added the -m command to NOT create a (Dummy).chart file.
* Added the -k command to close the program right after the conversion, instead of waiting for a keystroke.
* Added the -p parameter to read and write open notes (as N 7 0, or E O for editable version).*
* Added the -oh parameter to NOT automatically force open notes that are 1/12 or closer to another note as open HO/POs (useless without -p)

Bugfixes:
- Fixes a bug on which a tap section that contained a single tap note might not be converted as a tap note in some cases.
 
*Addendum: as of right now, open notes are only compatible with GHPCED 2 (still not complete), and they work in the following fashion: N 7 0 will override any existing note (such as N 0 0), making it become an open strum. For an open HO/PO, one must use N 7 0 and N 5 0.

EoF/Phase Shift do NOT support open note forcing - however, mid2chart will STILL read from the Force strum/Force HO/PO sections and force the open note accordingly (meaning one can force notes manually through a midi editor, like REAPER, and it will be compatible with GHPCED 2, but ignored by EoF/Phase Shift).

The conversor also forces open notes that are close to another (different) note by 1/12 or less as open HO/POs (like standard note behavior), but that can be disabled with the "-oh" parameter.
 
#### 10/05/2016
Additions:
* Reads delay (offset) from song.ini, and adapts it accordingly (ex. 253 to 0.253).
* Reads hopo_frequency and eighthnote_hopo from song.ini - if the former is 250 and/or the latter is 1, the song has a 1/8 HO/PO threshold, and the converter will force notes accordingly.
* The -8 parameter will only set the HO/PO threshold to 1/8 if the song.ini didn't set it already - if it already did, the -8 parameter will revert it back to the default 1/12.
* The -k parameter (swap keys and bass) has been renamed to -kb.
* Added the -kg parameter, which swaps keys and guitar.
* Added the -gb parameter, which swaps guitar and bass.
* Added a check so only one of these three parameters can be used at a time. If the user uses more than one parameter, he'll be warned that one is already set, and that the other(s) will be ignored.
 
#### 02/05/2016
Additions:
* Now reads metadata if there's a song.ini file in the same folder as the mid file. The converter will use its data to set the song name, artist, year and charter attributes in the converted chart file.
 
#### 30/04/2016
Additions:
* Added the -8 parameter, which sets the HO/PO threshold to 1/8. (Default is 1/12)
 
#### 27/04/2016
Additions:
* Added the -o parameter, which clips sustains and/or fixes overlapping notes.

Bugfixes:
* Fixes a bug on which the converter would crash during certain conversions (such as Chaotrope's Baptized by Fire and Chiasm midis) if the -r parameter was set.
 
#### 14/04/2016
Special thanks for Plumato for suggesting most of these features (all, except the very last one)!
Additions:
* Now supports RBN2 sections ([prc_section] instead of [section section]).
* Now exports PART KEYS on Enhanced Guitar part, for use in Feedback.
* Exported PART KEYS supports proper RB3 Keys-on-Guitar HO/PO logic (including double HO/POs).
* Added the -k parameter, which swaps PART BASS and PART KEYS when converting.
* Added the -d parameter, which fixes double HO/POs (notes/chords that are the same, but are forced as HO/POs due to charting flaws (as seen in Amberian Dawn's Lionheart, for instance), or due to the odd keys-to-guitar conversion on RB3's engine).
* Added the -c parameter, which doesn't force chord HO/POs (useful for non-GH3+ users, or console players).
 
#### 10/04/2016
Bugfixes:
* Fixes a bug on which the converter would fail during the broken chord fixing process in very specific situations.
* Fixes a bug on which the converter wouldn't force notes properly if the length of the force HOPO/force strum/tap note section was zero.

Additions:
* Adds the -f parameter, which adds 1 to the length of all force HOPO/force strum/tap note sections in the song. It fixes a problem on which the last note of the aforementioned sections wouldn't be forced, but it might cause some notes to be unproperly forced.
* Adds the -s parameter, which adds 1 to the length of all star power sections in the song. It fixes a problem on which the last note of the aforementioned sections wasn't a part of their proper star power section, but it might cause some notes to be unproperly assigned to star power sections.

If you're having problems with notes not being properly forced and the -f/-s parameters don't help, try opening the .mid in EoF, going into Settings and setting Min. note length (ms) as 18, resaving the project and converting the resaved .mid (thanks Notyu1459 for this solution).
 
#### 09/01/2016
Additions:
* Removes duplicate events.

Bugfixes:
* Fixes a bug on which the Harmonix HO/PO logic was never applied, even with the proper parameter usage.
* Fixes a bug on which a HO/PO would be forced wrongly if the previous note was a chord and the current note was the same as the highest note in the previous chord (ex. 3 would be forced if the previous chord was 123). It is still forced when using the Harmonix HO/PO logic, though.
* Fixes a bug on which duplicated notes would be detected as a chord, resulting in forcing errors.
 
#### 08/01/2016

Ported to C#, now requires .NET Framework 4.5.2 instead of Java to run.
It also uses NAudio to read midis, and unphook's Stopwatch to time activities, the former being under the Ms-PL license, and the latter being under the MIT license.
Improvements:
* Perfomance improvement; now it can be up to 12x times faster than the old version!

Additions:
* Software now says what it is doing and how much time it took to complete the tasks;
* Requires user to press a button to close instead of closing by itself automatically, giving the user time to actually see what happened, errors, etc.
 
#### 29/12/2015
Bugfixes:
* Fixes a bug where open strums are converted as green tap notes - now they're just regular green notes!

Additions:
* The converter now adapts broken chords into multiple chords, forcing HO/PO where necessary.
* Adds the "-b" parameter, which bypasses the aforementioned adaptation, and leave the broken chords as they are, if there's any. (This can be used to slightly speed up the conversion process when converting charts that don't have any broken chords)
 
#### 22/12/2015
* First released version!

# Old versions

Those old versions were released before this project was released in GitHub. You can find the respective versions by their date:

* [01/07/2016](https://www.dropbox.com/s/vjgpg08g2gp1nxp/mid2chart.7z?dl=1)
* [10/05/2016](https://www.dropbox.com/s/vhgpbmlb6r1nvj1/mid2chart%2010-05-2016.7z?dl=1)
* [02/05/2016](https://www.dropbox.com/s/vvdgbfi3gqdojol/mid2chart%2002-05-2016.7z?dl=1)
* [30/04/2016](https://www.dropbox.com/s/d834vn6p4aped7b/mid2chart%2030-04-2016.7z?dl=1)
* [27/04/2016](https://www.dropbox.com/s/l27hyhzxgyyq1ss/mid2chart%2027-04-2016.7z?dl=1)
* [14/04/2016](https://www.dropbox.com/s/xfqc48pvhme1m73/mid2chart%2014-04-2016.7z?dl=1)
* [10/04/2016](https://www.dropbox.com/s/ihlxkiwjaskcaqx/mid2chart%2010-04-2016.7z?dl=1)
* [09/01/2016](https://www.dropbox.com/s/3riumt6cyi5e3k8/mid2chart%2009-01-2016.7z?dl=1)
* [08/01/2016](https://www.dropbox.com/s/59hu5ksjaaq8ii8/mid2chart%2008-01-2016.7z?dl=1)
* [29/12/2015](https://www.dropbox.com/s/h1fe1spir0vkmqz/mid2chart%2029-12-2015.7z?dl=1)
* [22/12/2015](https://www.dropbox.com/s/m0i22zrvmg15o9p/mid2chart%2022-12-2015.7z?dl=1)
