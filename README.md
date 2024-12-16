This is how the decline of the SPD sounds
================

`December 13, 2024`

Germany’s Social Democratic Party (SPD) still leads the current
government under Chancellor Olaf Scholz – but his governing coalition
has fallen apart and he’s called for snap elections. The SPD’s poll
numbers have been declining for years. We turned the figures into sound
– the lower the note, the worse the result.

*This story is inspired by the 2018 project [“Der Sound zum tiefen Fall
der SPD”](https://interaktiv.morgenpost.de/spd-absturz-sound/) by Funke
Interaktiv for Berliner Morgenpost.*

*Thank you to Moritz Klack, André Pätzold, Marie-Louise Timcke, Julius
Tröger and David Wendler for their great work and for making the [code
behind their
project](https://interaktiv.morgenpost.de/spd-absturz-sound/data/spd-absturz-sound-methodik.html)
publicly available.*

See the final result on our Instagram channel:
[@dw_news](https://www.instagram.com/dwnews)

**Story by:** [Kira Schacht](https://twitter.com/daten_drang) and
[Dustin
Hemmerlein](https://de.linkedin.com/in/dustin-hemmerlein-4671a8173)

## Analysis

You can find the code behind this analysis in the R Markdown file `SPD-polls-analysis.Rmd`. You will need the programming language R to run it.

### Scrape data

To analyze polling results, we extract data from
[wahlrecht.de](https://www.wahlrecht.de/umfragen/index.htm), which has
been documenting polling results in Germany going back to the 1990s.

This is an excerpt of the resulting dataset:

    ##        datum cdu_csu spd grune fdp linke af_d
    ## 1 2024-12-10      31  17    13   4     3   18
    ## 2 2024-12-06      33  15    14   4     3   17
    ## 3 2024-12-05      32  16    14   4     3   18
    ## 4 2024-12-05      30  18    13   4     3   19
    ## 5 2024-12-03      32  16    12   3     4   18
    ## 6 2024-12-03      34  15    13   4     3   17
    ##                                            pollster
    ## 1                                             Forsa
    ## 2                           Forschungsgruppe Wahlen
    ## 3                                   Infratest dimap
    ## 4                                            YouGov
    ## 5                                             Forsa
    ## 6 GMS (Gesellschaft für Markt- und Sozialforschung)

And this is what all of these polling results look like over time:

![](SPD-polls-analysis_files/figure-gfm/unnamed-chunk-2-1.png)<!-- -->

### Calculate smoothed average line

We include data from representative surveys from 8 different pollsters
in this analysis, which means there might be multiple results with
slight statistical variations for the same time period.

In order to show an average of these polls over time, we use a local
regression
([LOESS-smoothing](https://web.archive.org/web/20020416060643/https://www.itl.nist.gov/div898/handbook//pmd/section1/pmd144.htm))
algorithm.

For any given point in time, it considers the closest 2,5 percent of
survey values in our dataset and calculates a weighted average of those.
The closer to the group average a value is, the more it factors into the
calculation. This limits the effect of extreme outliers on our estimated
average.

In order to turn the polling average into distinct sounds, we show one
data point per month instead of a continuous daily curve. We show the
last 20 years, starting with the first month after the federal election
in 2005.

This is what the finished chart looks like:

![](SPD-polls-analysis_files/figure-gfm/unnamed-chunk-3-1.png)<!-- -->

### Sonify data

To turn the monthly local averages into sound, we use the free tool
[DataSonifyer](https://studio.datasonifyer.de/).

If you want to see which presets we used, you can import our
configuration file `data/spd-polls-DataSonifyerExport.json` into
DataSonifyer with the “Import preset” button at the bottom of the tool’s
page.
