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
```
0	0.5	good don’t doesn’t understand find life love woman present thing part difficult nature past true wrong moment isn’t instance people 
1	0.5	painting beautiful good you’ll bad figures painters place paintings canvases canvas let’s made future fine colours lot isn’t delacroix living 
2	0.5	figure art view great point make question short feeling making beginning reason simply work draw mine talk working person sort 
3	0.5	gauguin paintings letter money paris francs good send colour back give he’ll we’ll order find idea moment buy pay hope 
4	0.5	time white small green days man grey light sky black give dark works coming sun red sea children young water 
5	0.5	write letter hope time days back thought you’ll day morning wrote made make home hear handshake lot find visit large 
6	0.5	man words long day people great van read hand rembrandt poor chap told maris mind received strength place christmas strong 
7	0.5	god good life uncle evening heart love give sunday lord father thy beautiful london christ book today boy rev thou 
8	0.5	work don’t time can’t feel studies make people long studio won’t drawing thing wouldn’t didn’t isn’t put kind case working 
9	0.5	thinking thought room full desire face high peace found dead half night years making window death fire worth firm graphic 
```
The actual output file can be found [here](https://github.com/nmcdowell00/MALLET_tutorial/blob/master/tutorialSample/tutorialSample_1a.txt).

`--output-doc-topcis` determins the name of the file that will contain the topic weight data of your topic model(how present 
each topic is in each file). This file might look confusing at first just because of the cluttered nature of the output but 
with practice it will make sense. An example of the output can be found [here](https://github.com/nmcdowell00/MALLET_tutorial/blob/master/tutorialSample/tutorialSample_1b.txt). I reccomend opening this 
document in excel at first just so you can see its true structure. To explain its structure I will present a portion of 
the document created by the command above(this is file is linked earlier in this paragraph).
```
0	file:/Users/natemcdowell/Desktop/mallet-2.0.8/corpusi/vgCorp/let221.txt	0.1565040650406504	0.06707317073170732	0.09959349593495935	0.042682926829268296	0.03048780487804878	0.2459349593495935	0.034552845528455285	0.07113821138211382	0.22560975609756098	0.026422764227642278
1	file:/Users/natemcdowell/Desktop/mallet-2.0.8/corpusi/vgCorp/let584.txt	0.028106508875739646	0.09023668639053255	0.11686390532544379	0.4807692307692308	0.016272189349112426	0.09319526627218935	0.013313609467455622	0.0073964497041420114	0.09615384615384616	0.057692307692307696
2	file:/Users/natemcdowell/Desktop/mallet-2.0.8/corpusi/vgCorp/let037.txt	0.0043859649122807015	0.07456140350877193	0.0043859649122807015	0.013157894736842105	0.2236842105263158	0.17982456140350878	0.2675438596491228	0.15350877192982457	0.0043859649122807015	0.07456140350877193
3	file:/Users/natemcdowell/Desktop/mallet-2.0.8/corpusi/vgCorp/let745.txt	0.1629032258064516	0.14677419354838708	0.024193548387096774	0.19193548387096773	0.05	0.03064516129032258	0.05967741935483871	0.0016129032258064516	0.22741935483870968	0.10483870967741936
4	file:/Users/natemcdowell/Desktop/mallet-2.0.8/corpusi/vgCorp/let023.txt	0.011363636363636364	0.2159090909090909	0.056818181818181816	0.03409090909090909	0.10227272727272728	0.32954545454545453	0.011363636363636364	0.07954545454545454	0.125	0.03409090909090909
```
The first column will be a placeholder value. The second column is all of your filenames. The following columns are the weight of each topic in that letter. For example. The topic weight of the first topic in let221.txt would be 0.1565040650406504. The 
topic weight of the second topic in let221.txt would be 0.06707317073170732. You probably understand how to read this data 
now. To see it in a more structured format you can open it in excel. You may also notice that this data was not outputted in 
the right order(chronologically). This can be solved later when we create visuals with SVG and XSLT. An explanation on how to create visuals can be found on the [visualizeData.md](https://github.com/nmcdowell00/MALLET_tutorial/blob/master/visualizeData.md) page. 



