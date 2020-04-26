## Visualizing your data

When I first tried to create visuals for my Topic Model I used Excel. This was a horrible experience. Do not use Excel. Use 
some varation of the XSLT/SVG below: 
```XSLT
<xsl:stylesheet xmlns:xsl="http://www.w3.org/1999/XSL/Transform"
    xmlns:xs="http://www.w3.org/2001/XMLSchema" exclude-result-prefixes="xs" version="3.0">
    <xsl:output method="xml" indent="yes"/>
    <xsl:variable name="letter_tsv" as="xs:string+" select="unparsed-text-lines('it_3bi300.txt')"/>
    <xsl:template name="xsl:initial-template">
        <xsl:variable name="unsortedletters" as="element(letter)+">
            <xsl:for-each select="$letter_tsv">
                <letter>
                    <xsl:variable name="letter_parts" as="xs:string+" select="tokenize(., '\t')"/>
                    <filename>
                        <xsl:value-of select="tokenize($letter_parts[2], '/')[last()]"/>
                    </filename>
                    <xsl:for-each select="3 to count($letter_parts)">
                        <topicValue n="{current() - 3}">
                            <xsl:value-of select="$letter_parts[current()]"/>
                        </topicValue>
                    </xsl:for-each>

                </letter>
            </xsl:for-each>
        </xsl:variable>
        <xsl:variable name="sortedLetters" as="element(letter)+">
            <xsl:perform-sort select="$unsortedletters">
                <xsl:sort select="filename"/>
            </xsl:perform-sort>
        </xsl:variable>
        <svg xmlns="http://www.w3.org/2000/svg" height="750" width="1000">
            <g transform = "translate(50,600)">
                <xsl:for-each select="0 to 9"><!-- create a polyline for each topic --><!-- if only want certain topics write "x,y,z,..." -->
                    <xsl:variable name="currentTopicNumber" as="xs:integer" select="current()"/>
                    <xsl:variable name="currentPoints" as ="xs:string+">
                        <xsl:for-each select="$sortedLetters"><!-- plot a point for each letter.  -->
                            <xsl:value-of
                                select="(position() * 4) || ',' || (current()/topicValue[@n = $currentTopicNumber]) * -500"
                            />                           
                        </xsl:for-each>
                    </xsl:variable>
                    <polyline points="{$currentPoints}" stroke="black" stroke-width="1" fill="none"/>
                </xsl:for-each>

            </g>
            <line x1="54" y1="600" x2="1000" y2="600" stroke="black" stroke-width="2" stroke-linecap="square"/>
            <line x1="54" y1="600" x2="50" y2="0" stroke="black" stroke-width="2" stroke-linecap="square"/>
            <text></text>
            
            <!-- <text x="54" y="625" text-anchor="center"></text> -->
            
        </svg>
    </xsl:template>
</xsl:stylesheet>
```


