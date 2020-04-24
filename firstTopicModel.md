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
./bin/mallet import-dir --input /Users/natemcdowell/Desktop/mallet-2.0.8/corpusi/vgCorp --output tutorialSample_1 --keep-
sequence --remove-stopwords --extra-stopwords /Users/natemcdowell/Desktop/mallet-2.0.8/genConj.txt
```
