exam 1
================

### Econ B2000, Statistics and Introduction to Econometrics

### Kevin R Foster, Colin Powell School, the City College of New York, CUNY

### Oct 14 2021

*The questions are worth 120 points. You have 120 minutes to do the
exam, one point per minute.* *All answers should submitted
electronically. Please submit all relevant computer files as a Slack
message to me. I prefer .Rmd files **along with knit output,** md or
html is fine. Please no “pages” files, save output and code as pdf or
rtf if you must.* *You may refer to your books, notes, calculator,
computer, or astrology table. The exam is “open book.”* *However, you
must not refer to anyone else, either in person or electronically,
during the exam time. For instance, since these exam questions are newly
created, posting questions or copying answers on Discord or WhatsApp
groups or online homework helping sites or forums (such as Chegg, Yahoo
answers or others) is a violation. Don’t upload to public GitHub site
until end of exam.* *You must do all work on your own. Cheating is
harshly penalized.* *Good luck. Stay cool.*

For this exam we will use a new dataset, looking at household
experiences during pandemic. This collects data on economic distress
such as job loss, falling behind on rent or mortgage, and shortages of
food. This also has info on vaccination.

The first questions do not require any work in R (although you might
find it convenient, I’m not stopping you) – I will provide some summary
data and you can construct hypothesis tests on your own. Subsequent
questions require R coding.

1.  (20 points) I’ve run crosstabs on a subset of the data (so you
    cannot replicate, just use these data as provided). These give
    verbose summary of vaxx choice by educational qualification and
    region. Form a hypothesis test of the form, “people with *various*
    educational qualifications in *Region* have different fraction
    vaxxed compared with *other Region*.” I expect that you will choose
    different ways to operationalize educational qualification (compare
    above some level with below that level, but what level?) and
    different regions (Census provides 4 – Northeast, Midwest, South,
    West, you might combine them). You can choose how to deal with NA
    responses to vaxx – perhaps count them as ‘no’? I expect that
    different people may choose different levels of significance. Please
    provide estimate, standard error, t-stat and a p-value for the
    hypothesis test and a confidence interval. **Write a short
    paragraph** explaining the test (carefully noting what is the null
    hypothesis) and explaining the results of that test.

<!-- end list -->

``` r
> xtabs(~ EEDUC + RECVDVACC + REGION)
, , REGION = Northeast

              RECVDVACC
EEDUC         NA yes got vaxx no did not get vaxx
  less than hs    0           25                  15
  some hs         1           95                  17
  HS diploma     25          924                 174
  some coll      20         1407                 201
  assoc deg      15          834                 104
  bach deg       34         2603                 147
  adv deg        19         2680                  88

, , REGION = South

              RECVDVACC
EEDUC         NA yes got vaxx no did not get vaxx
  less than hs    0           92                  45
  some hs         4          192                 101
  HS diploma     31         1844                 585
  some coll      57         3498                 747
  assoc deg      28         1704                 360
  bach deg       59         5193                 498
  adv deg        62         5024                 284

, , REGION = Midwest

              RECVDVACC
EEDUC         NA yes got vaxx no did not get vaxx
  less than hs    3           38                  17
  some hs         5           95                  49
  HS diploma     25         1217                 329
  some coll      32         2093                 454
  assoc deg      26         1227                 245
  bach deg       56         3228                 311
  adv deg        39         2680                 143

, , REGION = West

              RECVDVACC
EEDUC         NA yes got vaxx no did not get vaxx
  less than hs    2          107                  28
  some hs         4          204                  75
  HS diploma     24         1532                 386
  some coll      55         3896                 716
  assoc deg      29         1870                 313
  bach deg       68         5397                 467
  adv deg        50         4676                 218
```

2.  (20 points) I’ve run crosstabs again, this time on vaxx choice by
    educational qualification and gender identification. Form a
    hypothesis test of the form, “people with *various* educational
    qualifications who are *one or more gender ID* have different
    fraction vaxxed compared with *another gender ID*.” I expect that
    you will choose different ways to operationalize educational
    qualification (as noted in Question 1) and different genders
    (including the NA response, perhaps it makes sense to combine some).
    Choose a level of significance. Please provide estimate, standard
    error, t-stat and a p-value for the hypothesis test and a confidence
    interval. **Write a short paragraph** explaining the test (carefully
    noting what is the null hypothesis) and explaining the results of
    that test.

<!-- end list -->

``` r
> xtabs(~EEDUC + RECVDVACC + GENID_DESCRIBE)
, , GENID_DESCRIBE = NA

              RECVDVACC
EEDUC         NA yes got vaxx no did not get vaxx
  less than hs    1            9                   2
  some hs         9            9                   2
  HS diploma     66           63                  14
  some coll      84           84                  20
  assoc deg      62           43                   7
  bach deg      148          126                  20
  adv deg       123          120                  16

, , GENID_DESCRIBE = male

              RECVDVACC
EEDUC         NA yes got vaxx no did not get vaxx
  less than hs    3          106                  29
  some hs         1          248                  91
  HS diploma     14         1992                 557
  some coll      21         4238                 783
  assoc deg       8         1902                 297
  bach deg       26         6773                 504
  adv deg        20         6271                 263

, , GENID_DESCRIBE = female

              RECVDVACC
EEDUC         NA yes got vaxx no did not get vaxx
  less than hs    0          131                  57
  some hs         3          309                 144
  HS diploma     25         3372                 876
  some coll      54         6411                1292
  assoc deg      28         3613                 703
  bach deg       39         9354                 873
  adv deg        22         8524                 413

, , GENID_DESCRIBE = transgender

              RECVDVACC
EEDUC         NA yes got vaxx no did not get vaxx
  less than hs    1            3                   6
  some hs         0            6                   1
  HS diploma      0           21                   4
  some coll       0           42                   5
  assoc deg       0           12                   3
  bach deg        1           42                   2
  adv deg         0           28                  10

, , GENID_DESCRIBE = other

              RECVDVACC
EEDUC         NA yes got vaxx no did not get vaxx
  less than hs    0           13                  11
  some hs         1           14                   4
  HS diploma      0           69                  23
  some coll       5          119                  18
  assoc deg       0           65                  12
  bach deg        3          126                  24
  adv deg         5          117                  31
```

3.  (80 points) Now do your own analysis using
    “Household\_Pulse\_data.RData”. Choose an interesting topic to
    explore, different from previous questions. The data includes
    information on housing (rent or own; whether behind on rent or
    mortgage), food shortage, whether work remote or in person, whether
    kids are in school in person or remote or homeschooled, how anxious
    or worried, vaxx status and plans, along with demographics like
    race/ethnicity, gender, marital status, and household income (as a
    factor).  

<!-- end list -->

  - Choose a subgroup of the sample to consider and provide summary
    statistics of that subgroup. Explain why this subgroup is
    interesting.
  - Form a hypothesis test about an interesting variable, explore
    whether your chosen subgroup differs from the rest of sample. Please
    provide both a p-value for the hypothesis test and a confidence
    interval. Write a short paragraph explaining the test (carefully
    noting what is the null hypothesis) and explaining the results of
    that test.
  - Using a k-nn classifier, can you find relevant information to
    predict an interesting outcome? How good is the classifier? Discuss.
  - Can you explain some other interesting information about this data?
    Some interesting crosstabs? Maybe regressions? Impress me.

Please sign this.  
*All of the work on this exam is my own, answered honestly as rules
state.*  
Name:  
Date:
