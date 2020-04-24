## Your First Topic Model

In order to run your first Topic Model you have to make sure that you have Mallet directory located on your Desktop(idt this 
is neccesary it just makes it a lot easier) a within that, a subdirectory containing all of the txt files you created earlier
with the batch transformation. For this tuturial my subdirectory of txt files will be name vgCorp.

### Input your corpus 

First you must navigate into the MALLET directory: For me, I would use `cd desktop` since my mallet directory is on the 
desktop followed by `cd mallet-2.0.8`(if you type a little bit of the the filename you can press tab to auto-complete).
Now that you are in the MALLET directory you can now run a command that will transform your input corpus into a form MALLET
can actually use. 
```
./bin/mallet import-dir --input /Users/natemcdowell/Desktop/mallet-2.0.8/corpusi/vgCorp --output tutorialSample_1.mallet --keep-sequence --remove-stopwords --extra-stopwords /Users/natemcdowell/Desktop/mallet-2.0.8/genConj.txt
```
The `--input` command must be followed by the pathname of subdirectory which holds your corpus. This can be accessed by right
clicking on the subdirectory, holding the option key, then selection the option that says "copy 'xyz' as pathname". 

For the `--output` command you can enter whatever name you like as long as it ends with .mallet. This file is what will be 
used in the next command to run the Topic Model. 

`remove-stopwords` is a command that excludes a list of words that have been be determined by the creators of MALLET to be 
unhelpful for analysis. This list can be viewed by in the file en.txt file which is located within the stoplists subdirectory
within the mallet-2.0.8 directory. 

`--extra-stopwords` is a command that allows you to 
