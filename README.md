# Table of Contents (ToC) in print layout generated with raw CSS and HTML  

In general, generating a Table of Contents (ToC) in HTML is not a straightforward task; however, it is not very hard either. The problem arises when you want to generate a print layout with ToCs referring to page numbers and, additionally, create a table of contents element where the titles referred to in the ToCs are nicely connected with dots (....) leading to the page numbers.

Since this is quite a challenging task, I decided to describe my own method of creating such ToCs with an example and accompanying HTML/CSS code. This method is far from being very simple (I propose to use this document as a 'framework' for the automatic generation of such documents). The result looks good.

This approach has been tested with the <b>weasyprint</b> tool for generating PDFs from HTML.

This ToC visualization is applied only to @media print (visible in PDFs, not in HTML).

## Approach

The approach is to make a special [CSS document](toc.css) (which need to be included in the HTML document) and to use specific classes in the HTML document.

The structure of the HTML should contain two parts:

## The ToC itself.
This is a div which contains all ToC elements.
 
    <div class="toc">
      HERE GO ToC ENTRIES
    </div>

### Elements within the ToC div

Each entry in the ToC div have the following structure:

    <div class='toc_container'>
        <div class="toc_left-column"><a href="#intro">1. Introduction</a></div>
        <div class="toc_middle-column"></div>
        <div class="toc_right-column"><a href="#intro"></a> </div>
    </div>

All three parts within the 'toc_container' class are required:

- left column contains the name of the section 
- right column is used by the system to display the page number correctly
- the middle column is needed to put the proper number of dots in between the two above
 
Note that the 'href' (which is '#intro' in the example above) needs to be referring to a real ID which is used in the main document content section (ref. below). 

Note also that the section/subsection level needs to be manually specified in the toc_container div, as an additional class toc_level2 or toc_level3 
(three levels are supported but more can be easily added if needed).

## The document sections 

Next, the sections of the document are included. The only requirement here is to use the ID which are referred to in the 'toc' div entries.
Example:

    <section id="intro">
        <h2>1. Introduction</h2>
        <div> SECTION CONTENT </div>
    </section>

# Examples 

The example article using this approach is [example.html](example.html).

The generated PDF is [example.pdf](example.pdf).
