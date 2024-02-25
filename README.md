# Tilburg Science Hub To Flask
This is the repository thats hosts the news flask application for Tilburg Science Hub

## Install Packages
```
pip install Flask-SQLAlchemy
pip install SQLAlchemy
pip install beautifulsoup4
pip install nltk
pip install markdown
pip install Flask-Assets
```

## Content To Database
To create the database with all necessary data, simply go to the root folder and run the following command:

```python3 content_to_db.py```

## Start Up Flask Application
After successfully creating the database, you are ready to start up the flask application. To do so run the following command in the root folder:

flask run

## Updated & Implemented
- [x] Fix Authors
- [x] Related Articles
- [x] Blogs
    - [x] List
    - [x] Add to db
    - [x] Single
- [x] Breadcrumbs
- [x] In text links with {{% cta-primary-center .. %}} do not render -> shortcode added to parser
- [x] Header does not display BB's when hovering over it -> first item added classes active
- [x] urls on homepage cards dont work -> removed backslash at the end
- [x] Edit page url doesn't work -> url fixed
- [x] ODCM tutorial does not work (specific) -> pagination problem (empty weight), issue solved
- [x] formatting does not render in {{% blocks %}} (e.g. Learn R BB/ set up docker) -> adjust formatting in tips, example, warning.
- [x] {{% example }} block does not render (e.g. use Scrum in your team BB) -> implemented example
- [x] under automate and execute your work there is a "new" category called error handling? -> this is an error in the index.md of that file. For some reason it contains 2 draft parameters, which ofcourse results in problems. 
- [x] videos are not able to play (BB configuring git) -> corrected video parsing and move video files to img
- [x] symbols (e.g. $\alpha$) do not render -> issue with katex, fixed, stil a problem in content, documented in section "Issues related to content".
- [x] formulas in {{}} {{}} also do not render (both in BB on fixed effects) -> issue with katex, fixed.
- [x] << katex >> also does not render (BB sample size on webscrapers) -> issue with katex, fixed.
- [x] external youtube link does not render {{< youtube DK7TYR68kqc iframe-video-margins >}} (BB practicing pipeline automation > verify)
- [x] Text out of line (e.g. BB on cars/ interactive Interactive shiny COVID-19)
- [x] #'s in a ``` block get converted to headers instead of to just small text within the block (BB configure git/ reschedule tasks) -> created a fallback codeblock such as in the current website
- [x] remove google console bugs (js bugs mainly)
- [x] make slider on mobile only move when clicked/touched -> implemented from main
- [x] Most read tutorials - duplicates -> implemented from main
- [x] scaling of tilburg science hub image on landing page off -> implemented from main
- [x] bug w/ slider on mobile -> implemented from main
- [x] About page in footer -> implemented from main
- [x] Recently updated/published settings -> works now with date and date_modified.
- [x] About menu in header -> Added al necessary pages
- [x] add reading time estimate -> implemented
- [x] Cookies -> Fixed, we only need a basic analytics script.
- [x] Code Block -> Added
- [x] Apply Restructuring
- [x] Added first, second and third level category structure
- [x] Applied new Layout to website
- [x] Link (How to install LateX) does not work (set up LaTeX)
- [x] Create route for single article -> Route Created
- [x] Fix Hashtags when browsing via header bar -> Checked, is not necessary anymore
- [x] Email does not display properly & multiple "parts" of text (About TSH) -> Fixed the mail
- [x] Use 'X' button instead of Twitter? -> Updated
- [x] Buttons (Twitter, FB etc) are spread out, when there is no date (Download Data Programmatically) -> Checked and fixed
- [x] Bullet points do not render correctly (e.g., Random Effects Model) -> fixed, issue with markdown library. standard set to 4 spaces for list levels, adjusted this to 2 (= tab, just like Github).
- [x] Contributors links of people that do not do have a contributors page result in an error -> Added 404 page to display when errors happen or certain pages do not exist yet.
- [x] PDF-file download button does not render (Bookdown Thesis Template) -> added a new function for cta secondary center
- [x] MetaData -> Fixed for most pages. Topic lists still need to get meta data.

## Features/Issues to Update/Implement
- [ ] Copy Button in Codeblock
- [ ] Dual Code Blocks -> Added, but having problems (displays language twice and switching does not work)
- [ ] Implement New Basic Web Analytics Cookies
- [ ] Reproducible Research (homepage) link does not work
- [ ] {{< katex }} does not display correctly (Calculate Sample Sizes for web scrapers)
- [ ] Presentation slides are not available (Blog - Introducing TSH at the Open to Complexity Symposium)
 
## Issues related to content
- [ ] The way people use katex is inconsistent which gives problems during rendering. Some people forget to add the $ sign in front and at the end of a variable, which was not really an issue for some reason in Hugo, but in Flask this makes applying these Katex Formulas why harder. We should fix the katex boxes in content and make sure it is used correctly in all content.
- [ ] Tables currently to complex to parse to html by hardcoding. The most effective way would be to convert them all to html with ChatGPT (tried it, is very easy and quickly done) and add context to the styleguide on how people can add a html table (very easy and logical). Another option would to self design a new structure for a table. We should discuss this with Hannes.
    - [ ] tables do not display correctly (e.g., Random Effects Model, Configure Python virtual environments)
- [] Some articles have lists without an enter (break) in front of it. The markdown package then cannot convert them to html lists.
- [ ] In Task Scheduling BB: someone wrote the following:

```
# e.g., * * * * * /usr/bin/python3 /script.py
<CRON CODE> <PATH OF YOUR PYTHON INSTALLATION> <PATH TO PYTHON FILE>
```

and also in a codeblock. It would be more efficient to change this since html sees < > as tag elements, which it now tries to autocomplete, instead as interpreting it as a string. The autocomplete process is something outside of my control (happens by browser).
- [ ] All Codeblock languages should be shown as follows ```Stata, so in the same line straight after the three signs, without any other signs such as - or others.
- [ ] Codeblock structure needs to be consistent, quite some people do not use the {{% codeblock %}} signs which makes rendering structurized hard.
    - [ ] Codechunks not correctly displayed (No ```) (R Coding Style Guidelines)
    - [ ] code chunk without content (Run RStudio on AWS docker)
    - [ ] BASH not correctly specified in chunk (Debugging Makefiles with Remake)
- [ ] Title does not display properly (e.g., Confgure Python virtual environments) -> checked, it is a content error in the specific article that needs to be fixed)
- [ ] $ formulas do not render correctly (e.g., Random Effects Model) -> checked, refers to point 1 in content list. The formula used in the context does not use the $ signs at variables, which leads to flask not recognizing the item as a variable.
