---
title: "Open Exploration Intercepts"
date: 2020-02-24T15:36:28+01:00
draft: true
---

The mining industry is segmented in an interesting way that might surprise. 
Many junior companies are publicly listed and raise funds on 
This fact , cases of fraud, have lead to 

https://www.thebalance.com/what-is-a-ni-43-101-report-1979210

https://www.micon-international.com/ni-43-101-technical-reports-theyre-not/

When I first read about these a few years ago I imagined that there was a dictated format and schema. Unfortunately that is not the case. 
In fact, there is a huge variety in what the report can contain

From Micon:

>"An NI 43-101 Technical Report can be any of the following:
> 
> - A first time report on a mineral property (exploration or operating).
> - A summary of the exploration activities with inherent Quality Control/Quality Assurance (QA/QC) on a project.
> - A summary of the mineral resource estimate for a property.
> - A report outlining ownership of a non-operating interest in a property (Royalty or otherwise).
> - A report containing the results of a Preliminary Economic Assessment.
> - A report or summary of the results of a Pre-Feasibility Study, depending on the complexity of the project.
> - A summary of the results of a Feasibility Study on a mineral property.
> - A summary of work conducted on an operating project possibly containing updated resource and reserve estimates.
> 
> or any variation of the above."

So there is a huge variety in reporting standards, and the NI-43 101 is more of a guideline that requires.

All of thsese

I noticed a trend recently of companies releasing drill intercepts in conjunction 
This is the exception rather than the rule, 

It may be useful, it may not be useful, but it certainly makes me think much more of the commitment to openness, fair-dealing, and innovation. I applaud all of the companies that take this initiative .

https://www.visualcapitalist.com/mineral-exploration-roadmap/
https://www.visualcapitalist.com/equity-financing-mining-exploration-sector/




# Example 

## Data Extraction + Wrangling

https://www.oceanagold.com/investor-centre/filings/

This will be a multi step process:

- Download the collars, assays, and surveys 
- Run them through OCR to extract the text from the PDF (unless they are already in a convenient format, like CSV or text layer in a PDF). 
    - We could use Tesseract or Textract, I will use Textract for this project since it is more scalable and handles tables quite well. Read about the other advantages here.

- 

### Collars 

The collars are in UTM NAD83 
South Carolina is UTM Zone 17

## Load the Results


## Plot 


## Next steps

This data is too sparse for useful kriging interpolation, I might attempt to do some geostatistical simulation work to try and get a distribution for the size and grade of the deposit. Or, we could look at the drill results across multiple properties and determine favorability or do prediction. 