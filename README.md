Create weekly topical reading list PDF using rmarkdown, bib, and csv

The PDF produced creates 5-day work weeks for readings beginning at the first day chosen and ending for the number of weeks selected.
---

## Required 
- A bibfile with unique keys already generated
- A bibfile reader to extract the unique keys
- A csv file named ```topics.csv``` with three columns labeled ```cite```, ```type```, and ```week```
- An Rmarkdown editor such as [RStudio](https://www.rstudio.com/)
- A [LaTeX](https://www.latex-project.org/get/) distribution (to compile the PDF)
- The included ```svm-latex-syllabus.tex``` LaTex template

## Languages
If you are interested in more than light customization of the default output, the following languages will be helpful:
- [Rmarkdown](https://rmarkdown.rstudio.com/authoring_quick_tour.html) can be thought of as a mixture of basic markdown markup language and R.


## Steps

### Preparing the CSV

- In the ```cite``` column of the csv file, paste all the citekeys (unique bib file entry keys).
- The ```type``` column accepts two values, ```refs``` (for main readings) and ```sups``` (for supplementary readings) with all other values being ignored.
- The ```week``` column accepts any number along the range of weeks desired. The example file has 15 weeks.

#### Important! 
There must be a block of the following code (shown below) for each week. For example, included Rmd file has 13 of the code blocks, so 13 units/weeks are printed in the PDF, although labeling stops at 18 in the included csv file.

````

`r j = j+1`
##  `r advdate(mon, j)``r paste(topics[j],"|",length(refs[[j]]), "Readings")`
```{r, echo = FALSE, results="asis"}
if (length(refs[[j]])!=0) {
  bib[refs[[j]]]
}
```

### Supplementary `r paste("|",length(sups[[j]]), "Readings")`:
```{r, echo = FALSE, results="asis"}
if (length(sups[[j]])!=0) {
  bib[sups[[j]]]
}
```
````

## Included Customizations

The most common customizations are easily updated in lines 1-57. 

### Header Arguments (line 1-25)
- All the values enclosed with quotation marks can be edited and are self-explanatory.
- fonts can be updated with ```fontfamily``` and ```header-inludes``` has a default option for spacing, which is passed to LaTex for compilation.

### Other Options (line 34-57)
- ```bibloc``` is a string for the name of the .bib file.
- ```day0``` is the first Monday of the first week.
- ```unit``` may be changed from the default "Week " to something like "Section " or something else entirely.
- ```topicsIN``` is a string containing the name of the .csv file.
- ```topics``` contains a character vector of strings for topic for each week.

## Troubleshooting
You might need to use ```devtools``` to download the ```RefManageR``` package.

````
install.packages("devtools")
devtools::install_github("ropensci/RefManageR")
````
