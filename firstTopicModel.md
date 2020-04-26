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

`--extra-stopwords` is a command that allows you to specify specific words that you wish to exclude from your topic model. 
Information on how to create your own stopword list can be found [here](https://github.com/nmcdowell00/MALLET_tutorial/blob/master/stopwords.md).

The output of this command can be viewed in tutorialSample_1.mallet file stored in the tuturialSample directory in this repo. Note that this document is really just a stepping stone to create actual meaningful results that will be explained in the next step. You probably won't be able to open the .mallet file unless you download something that can process it(idk what that would be). 

## Run you Topic Model

The next command you will enter: 
```
./bin/mallet train-topics --input tutorialSample_1.mallet --num-topics 10 --num-iterations 100 --output-state tutorialSample_1.gz --output-topic-keys tutorialSample_1a.txt --output-doc-topics tutorialSample_1b.txt
```
This command is what runs the topic model. The `--intput` command should be followed by the output generated in the last command.

`--num-topics` is how many topics you want MALLET to generate from the text. There is no reccomended amount of topics for 
MALLET since your most Corpuses are unique and react differently to the topic restraints. The best practice would be to run
test 5,10,15,20,25,... topics until you find a range that you find generates meaningful results. 

`--num-iterations` commands how many iterations MALLET will perform. 1 iteration would be MALLET passing through the text 
once. This means each word would only be analyzed and categorized once. More iterations allows MALLET to reavluate words and 
rearrange topics which creates more specific topics. For my actaul project I used 800 iterations. I would recommend running 
100,200,300,...,1000 iterations to just see the difference it makes. 

The next important command is `--output-topic-keys`. This determines the name of the file that will contain a overview of your 
topics. An example of this output would look like this:



