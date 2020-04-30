Create a syllabus with weekly topical reading list (or just the reading list) PDF using rmarkdown, bibfile, and csv. Students and researchers can use the reading list for categorizing references for a paper or research project. 

The Latex templates and the genral idea for this repo are modifications of the syllabus code and steps produced by [svmiller](https://github.com/svmiller/svm-r-markdown-templates).

My Modifications:

- Introduce nameable sections for reading units, along with unit totals.
- Allow for both required and supplemental (or whatever second category you choose) readings.
- Simplify code to loop through reading list of any length.
- Incorporate the option to include sources that are not fully styled references.
- Provide an an option for custom dates (for complex weekly splits) in addition to the default setting of 5-day weeks.
- Allow for a modern header with optional quote.
- Produces optional grading scale and course components tables from csv files. (Great for users who like to update tables in Excel rather than markdown).

---

## Required 
- A bibfile with unique keys already generated.
- A bibfile reader to extract the unique citation keys.
- A file, ```topics.csv``` with atleast the ```topics``` column, and (optionally) the ```unit```,	```date_start```,	and ```date_end``` columns.
- A csv file named ```classify.csv``` with three columns labeled ```cite```, ```type```, and ```unit```
- An Rmarkdown compiler (I'm using [RStudio](https://www.rstudio.com/)).
- A [LaTeX](https://www.latex-project.org/get/) distribution (to compile the PDF).
- The LaTex template ```svm-latex-syllabus.tex``` is from  [svmiller](https://github.com/svmiller/). See [here](http://svmiller.com/blog/2016/07/r-markdown-syllabus/) for more on customizing the .tex file.

## Preparing Your Data

### classify.csv

- ```cite``` alphanumeric citekeys (unique bib file entry keys). When a non-citekey value is found among the citekeys, it is printed verbatim (as markdown) in the final document.
- ```type``` string values ```refs``` (for main readings) and ```sups``` (for supplementary readings). All other values being ignored. This is equivalent to 'commenting out' entries for future use.
- ```unit``` integer values for the course reading unit.

### topics.csv
- ```topics``` strings for unit titles.
- ```unit``` (optional and not used) integer values for the course reading unit.
- ```date_start``` (optional) date string indicating start of unit
- ```date_end``` (optional) date string indicating end of unit

### bibfile.bib
- citekeys must be unique and should be distinguishable from any title you might manually assign to a reading. Regex is used to identify citekeys (default "[A-Za-z]:[0-9]").

## In-code Customizations

The code chunk ```userinput``` contains almost all modifications to make your own version of the syllabus/reading list. You might need to tinker with the ```date``` code chunk if your custom dates follow a different format than those I have included compatibility for.
