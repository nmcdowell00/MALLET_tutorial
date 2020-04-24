## How to Download Mallet
MALLET can be downloaded at <http://mallet.cs.umass.edu/download.php/>. 
There are instructions for installation on the page linked above. MALLET will be downloaded into your downloads folder. 
Once downloaded you should move the folder(which should be named mallet-2.0.8) onto your desktop. The next step will be 
transforming your XML files into a format that can be inputted into MALLET. 

## Batch Transformations
Prior to Topic Modeling I would advise having a corpus of of XML that can all be validated by a single schema(so that you
can write XSLT that can target the text that you want to analyze easily). MALLET cannot work with XML files; it only works
with an input of .txt documents. In order to save time you will use Oxygen to run a batch transformation on your XML files
in order to convert them all into indivdiual .txt files inside of a single directory. To do this we will write XSLT that
targets the XML node that stores the text that you want to extract. I will show the process that I used to break down my 
input files. 

### Example of a File that I want to transform. 
```XML
<letter>
      <head><location>Nuenen</location>, on or about Sunday, <date>20 July 1884</date>.</head>
      <salutation>My dear Theo,</salutation>
      <body>
            <p><good_health>I was delighted to learn from your letter to Pa and Ma that you plan to go to London</good_health>
                  on 4 Aug. and then to come on here from there. I’m again looking forward very much
                  to your arrival and to finding out what you’ll think of the work that I’ve done
                  since. <work origin="existing" stage="finished">The last things I did are a couple of rather large studies of oxcarts, a
                  black ox and a red and white one.</work></p>
            <p><work origin="new" stage="middle">And have also been working again on the old tower in the fields in the evening; I’ve
                  made a larger study of it than my previous ones — with the wheatfields around
                  it.</work></p>
            <p>Rappard sent me back the little book by Vosmaer that belongs to you — I started to
                  read it but — is it just me? — find it almighty boring and actually written in an
                  academic, sermonizing tone. Perhaps you will too when you look at it again. Have
                  you read Sapho by Daudet? <unstress reason="environment">It’s very beautiful, and so vigorous, and so close to
                  life that the female figure lives, breathes, and one can hear, literally hear the
                  voice, and forgets that one is reading.</unstress></p>
            <p>You’ll also <work stage="finished" origin="new">see a couple more new weavers </work>when you come.</p>
            <p>Nature is certainly pure here — I’m still very pleased with the studio, too.We must
                  visit some farms and weavers together when you come.</p>
            <p>Rappard’s plan is to come back again in October; he’s probably in Drenthe again
                  now.</p>
            <p>Well, I write in some haste because I’m hard at work. <good_health>I work a good deal early in the
                  morning or in the evening, and then sometimes everything is so inexpressibly
                  beautiful.</good_health></p>
            <p>Regards, believe me</p>
      </body>
      <close>Ever yours,</close>
      <sig>Vincent</sig>
</letter>
```
All of the information that I wish to extract is nested inside of the `<p>` element. So to extract that infromation I wrote
XSLT to target that node and strip it of all markup. 
```XSLT
<xsl:stylesheet xmlns:xsl="http://www.w3.org/1999/XSL/Transform"
    xmlns:xs="http://www.w3.org/2001/XMLSchema" exclude-result-prefixes="xs" version="3.0">
    <xsl:output method="text" indent="yes" doctype-system="about:legacy-compat"/>
    <xsl:template match="/">
        <html>
            <head>
                <title></title>
            </head>
            <body>
                <xsl:apply-templates select="//body"></xsl:apply-templates>
            </body>
        </html>
    </xsl:template>
    <xsl:template match="body">
        <p><xsl:apply-templates select="p"></xsl:apply-templates></p>
    </xsl:template>
```
If I were to run the just this one file and this XSLT(and set the output document to a .txt file) it would generate this:
```txt
I was delighted to learn from your letter to Pa and Ma that you plan to go to London
on 4 Aug. and then to come on here from there. I’m again looking forward very much
to your arrival and to finding out what you’ll think of the work that I’ve done
since. The last things I did are a couple of rather large studies of oxcarts, a
black ox and a red and white one.And have also been working again on the old tower in the fields in the 
evening; I’ve made a larger study of it than my previous ones — with the wheatfields around
it.Rappard sent me back the little book by Vosmaer that belongs to you — I started to
read it but — is it just me? — find it almighty boring and actually written in an
academic, sermonizing tone. Perhaps you will too when you look at it again. Have
you read Sapho by Daudet? It’s very beautiful, and so vigorous, and so close to
life that the female figure lives, breathes, and one can hear, literally hear the
voice, and forgets that one is reading.You’ll also see a couple more new weavers when you come.Nature is 
certainly pure here — I’m still very pleased with the studio, too.We must
visit some farms and weavers together when you come.Rappard’s plan is to come back again in October; he’s 
probably in Drenthe again now. Well, I write in some haste because I’m hard at work. I work a good deal 
early in the morning or in the evening, and then sometimes everything is so inexpressibly beautiful.
 ```
This output is something MALLET could use. In order to do this quickly for your whole corpus of XML files you must run a 
batch transfromation. Detailed instructions on how to perform batch transformations can be found [here](https://github.com/obdurodon/dh_course/blob/master/batch/configure-transformation.md).

After your batch transformation you should have a subdirectory containing all of your doccuments as .txt files. If you didn't orginally save it to the MALLET directory(the mallet-2.0.8 folder on your desktop) you should do that now. In order to run 
MALLET requires the input be stored in the MALLET Directory. For information on how to run your first TOPIC Model refer to 
[secondSteps.md](https://github.com/nmcdowell00/MALLET_tutorial/blob/master/secondSteps.md/) in this repository. 
