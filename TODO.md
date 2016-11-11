# TO DO

This is a list I am making with ideas I want to implement on my software on a somewhat near future, but am unable right now (as of 11/11/2016), due to real-life stuff.

* Add the -t parameter to NOT force tap notes, but force them as HO/POs instead (which should be used together with -c for non-GH3+ compatiblity).
  * Shouldn't be too hard - simply adding the NoteSections that are on the instrument's tap section List and then sorting the list afterwards should do the trick.

* Improve the code
  * Some methods on ChartWriter.cs and Song.cs have repeated code. Those should be put on different functions, and functions that are common to both classes should be put on a Common.cs or Function.cs file.
  * Song.cs has way too many lists! Difficulties can be toned down to a List<Event>[4] array, as well as the ForceHOPO and ForceStrum lists. And I could make a class called "Part", which contains all of the objects regarding that part, and the aforementioned list arrays.
    * E = 0, M = 1, H = 2 and X = 3 consts to make clear which position of the array refers to a specific difficulty.
  * Find a quick way to sort lists. It won't be necessary most of time time, and might make the program slightly slower, but it should be easily done, should it be necessary. Linq is pretty simple and memory shouldn't be an issue, but one could use the IComparer<> interface to create a new class, or implement IComparable<> on the sorted class itself.
    * For Note, sort by tick then note value. For everything else, sort by tick only.