# mtg-scanner

Simple scanner for Magic: The Gathering. A fork of original work by bitdagger / Matt Fields.
The old README survives in the bottom of this file, as its documentation on the use of this 
program is still accurate and useful.  

## Notice
This project does not contain any code, images, or any other type of data proprietary to  
Wizards of the Coast or any affiliated entity. This program is likewise not affiliated in  
any way with Wizards of the Coast. This program, when using running --update, will poll  
Gatherer to download the requested card images as specified by the configured sets (see below).  
There is no product, only code here. Keep it that way.

## Installation
So, full disclosure, I don't remember setting this up the first time. I do recommend getting  
and using Anaconda (the python 2.7 version) as it should come with the necessary opencv and  
imagehash libraries: https://www.continuum.io/downloads

If you do go through installation and feel like taking note of what other steps, or contact me  
if you get stuck, I can update this section.

## Configuration
The Gatherer pull will only include cards from the 'core' and 'expansion' type sets by default.  
This is configured in referencedb.py, in a conditional when retrieving set lists. You could, for  
example, add 'duel deck' to the conditional to also download dual deck set lists, but you'll get  
more dupes in the actual matching phase when using the tool.

## Use notes
If you're scanning that exist in multiple sets but have the same image, it will very likely find both,  
but match on whichever comes first. If you care about which set a card comes from, be aware of this  
since the output csv file will have the set you selected for the given card.

## Modifications
This project contains a number of modifications to bitdagger's original work:
* switch to use imagehash instead of phash. I wasn't able to get phash to work nor could I be  
arsed to compile it from source, so I replaced it. The algorithm could probably be better.
* fix a for loop that had some broken syntax (not sure if this was a python version issue)  
* changed some of the keycodes because they were busted or different - these are still hardcoded  
* fixed an issue with foil data not being exported
* swapped export to be in deckbox-compatible csv format

# Original README

## Operation  

1. Run `mtg-scanner --update` to grab the images from the gatherer and calculate hashes  
2. Run `mtg-scanner --scan` to open the camera and start scanning
3. Run `mtg-scanner --export` to export a list of cards in your collection

## Optional Arguments  
* `--debug` - Enable debugging when scanning  
* `--camera <integer>` - Specify a camera ID to use for scanning  
* `--database <DB>` - Specify a database name to use when scanning and exporting  

### While Scanning  

The stand-by screen has a blue border around it. From the stand-by screen, 
press Enter to isolate the card. If the framing is good, then press enter again 
to attempt to match. If the framing is not good, then you can press ESC or 
Backspace to go back to the stand-by screen.  

Once a match has been found it will display the matched card on the screen. 
Press Enter to add the card to your collection. If the card is a foil you can 
press F instead of Enter to add the card to your collection and mark it as a 
foil. If the card displayed is not the desired card, press N to try again. You 
can also press ESC to go back to the stand-by screen.

If you have multiple copies you want to add, after adding the first card you 
can press the + key on the numpad to bring up the confirmation prompt again. As 
before you can press Enter to add the card, F to add a foil, or ESC or 
Backspace to go back to the stand-by screen. You can press P instead of enter 
when adding a card to add a playset of that card instead (adds 4 copies at once).

Press Q at any time to quit.  

## Why Python2 and not Python3?  

I originally wrote the scanning system for python 2. After everything was fully 
functional I tried to upgrade everything to python 3, but the opencv library that 
is required for the scanning process does not support python 3. As such, until 
opencv supports python 3, this code will stay on python 2.  

## Credits  

http://mtgjson.com for the card data  
