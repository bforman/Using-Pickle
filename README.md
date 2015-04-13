# Using-Pickle
This repository goes into detail about Pickle, a Python standard library module, that is used to convert a Python object hierarchy into a data stream which can then be written to an output file.

#Problem
When creating the visual for the Infinite Player we will be using TkInter to produce a GUI. In the visual we are planning to have songs laid out in a bar structure where a rectangle bar will represent a track that is going through the infinite player, and within that song (and possibly between other songs) there are going to be slices of the rectangle delineated as possible branches for the curosr to link to next to continue playing from. The problem that has presented itself is being able to join all these possible branches together in one place so that when they are needed to be accessed they are easily obtainable. Although producing the visual is not concerned with calculating branches, it does have to handle those branches in a manner of visualizing them. When a track gets loaded into the player, we dont want to waste time by having to calculate possible branches, create those branches (slices on rectangle), and update the canvas to show the branches on the track all in real time while loading the track. Also by calculating possible branches as you go, it forces you to store the branches into a data structure in which you would have to traverse the whole thing each time in order to check over all the branches to ensure there are no duplicates. 
#Questions
1. What module(s) does Python offer to assist in solving this issue?
2. Is there an easy way to avoid duplicates when finding and storing branches?

#Resources
[Pickle](https://docs.python.org/2/library/pickle.html)


[Serial Encodings](http://pymotw.com/2/pickle/)

#How I intend to use Pickle
With the use of pickle() we will be able to identify branches, encode their data into strings, and group them together by dumping all the string "keys" into an outfile that can be used directly by our player. Pickle will store all the branches into a tree like structure in that outfile that can be traced likewise to a tree, which will make it easy to keep track of where we have been (for the ghost paths following the player). Also, by serializing all of the branches it will make not only the transfer of the branch to the player much quicker but it will make each branch identifiable by a key whether it be binary bits or the ASCII representation. Having the ASCII representation may serve to be helpful as well because in the case of debugging we can use a text editor and read whats going on. With all of the branch information pickled into one place, when we are on a given segment we will have all the possible branch choices ready and if one is picked we will know exactly where to jump to on the visual based on the key into the outfile tree, and like stated earlier we can place a tag on branches already taken so we can keep track of a ghost path.
