---
main_topsize: 0.2 #percent coverage of the poster
main_bottomsize: 0.1
#ESSENTIALS
title: 'Målsyede kurser'
author:
  - name: '**Ene Rammer**'
    affil: 2
    main: true
    orcid: '0000-0001-6220-3709'
    twitter: 
    email: 'enrn@kb.dk'
  - name: '**Christian Knudsen**'
    affil: 1
    main: true
    orcid: '0000-0002-9816-768X'
    email: 'cbk@kb.dk'
  
affiliation:
  - num: 1
    address: Hvad stedet nu hedder for tiden.
  - num: 2
    address: Roskilde Universitetsbibliotek

main_findings:
  - "Made-to-Measure data kurser"
logoleft_name: Datalab_colours_clear.png
logoright_name: DKB_logo_expanded_black_RGB.png
# logocenter_name: http://raw.githubusercontent.com/brentthorne/posterdown/master/images/qr-code-black.png
output: 
  posterdown::posterdown_betterport:
    self_contained: true
    pandoc_args: --mathjax
    number_sections: false
bibliography: poster_refs.bib
link-citations: true
knit: (function(inputFile, encoding) { rmarkdown::render(inputFile, encoding = encoding, output_file = file.path(dirname(inputFile), 'poster.html')) })

---



# Introduktion


KUB Datalab får regelmæssigt forespørgsler fra studerende med ønske om kurser
med _meget_ specifikt indhold. Det er for omkostningsfuldt at skulle udvikle
enkeltstående kurser hvis egentlig indhold er en gentagelse af den undervisning
de har fået i et kursus på universitetet, men som har voldt dem problemer. 

Vi har derfor udviklet et generelt "værktøjskassekursus", med elementer der hyppigt
er efterspørgsel på. På baggrund af disse lego-klodser kan vi hurtigt sammensætte
et tilrettet kursus der matcher de specifikke ønsker i en given situation.




# Infrastruktur

Kurset er opbygget i Workbench infrastrukturen fra Carpentries [@TheCarpentries] 
med brug af sandpaper [@sandpaper] pakken, og tilgængeliggjort på GitHub.


<!-- pagedown	pagedown::chrome_print("myfile.Rmd") -->

Hvordan bygger vi så hurtigt et kursus?

klon siden, rediger config.yaml, PR - og så er den der.


# Methods

Kursets didaktiske tilgang er baseret på teaching tech together. code-along
etc.

I will show here how to include poster elements that may be useful, such as an equation using mathjax:

$$
E = mc^2
$$

``` error
Error in knitr::include_graphics("kursussiden.png"): Cannot find the file(s): "kursussiden.png"
```






To get a better understanding of how to include features like these please refer to the {posterdown} [wiki](https://github.com/posterdown/wiki).

**_Now on to the results!_**

# Indhold

Tematiseret episodeliste


Here you may have some figures to show off, bellow I have made a scatterplot with the infamous Iris dataset and I can even reference to the figure automatically like this, `Figure \@ref(fig:irisfigure)`, Figure \@ref(fig:irisfigure).

<div class="figure" style="text-align: center">
<img src="fig/poster_dk-rendered-irisfigure-1.png" alt="Here is a caption for the figure. This can be added by using the "fig.cap" option in the r code chunk options, see this [link](https://yihui.name/knitr/options/#plots) from the legend himself, [Yihui Xie](https://twitter.com/xieyihui)." width="80%" />
<p class="caption">Here is a caption for the figure. This can be added by using the "fig.cap" option in the r code chunk options, see this [link](https://yihui.name/knitr/options/#plots) from the legend himself, [Yihui Xie](https://twitter.com/xieyihui).</p>
</div>

Maybe you want to show off some of that fancy code you spent so much time on to make that figure, well you can do that too! Just use the `echo=TRUE` option in the r code chunk options, Figure \@ref(fig:myprettycode)!


``` r
#trim whitespace
par(mar=c(2,2,0,0))
#plot boxplots
boxplot(iris$Sepal.Width~iris$Species,
        col = "#008080", 
        border = "#0b4545",
        ylab = "Sepal Width (cm)",
        xlab = "Species")
```

<div class="figure" style="text-align: center">
<img src="fig/poster_dk-rendered-myprettycode-1.png" alt="Boxplots, so hot right now!" width="80%" />
<p class="caption">Boxplots, so hot right now!</p>
</div>

How about a neat table of data? See, Table \@ref(tab:iristable):

<table>
<caption>A table made with the **knitr::kable** function.</caption>
 <thead>
  <tr>
   <th style="text-align:center;"> Sepal <br> Length </th>
   <th style="text-align:center;"> Sepal <br> Width </th>
   <th style="text-align:center;"> Petal <br> Length </th>
   <th style="text-align:center;"> Petal <br> Width </th>
   <th style="text-align:center;"> Species </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:center;"> 5.1 </td>
   <td style="text-align:center;"> 3.5 </td>
   <td style="text-align:center;"> 1.4 </td>
   <td style="text-align:center;"> 0.2 </td>
   <td style="text-align:center;"> setosa </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 4.9 </td>
   <td style="text-align:center;"> 3.0 </td>
   <td style="text-align:center;"> 1.4 </td>
   <td style="text-align:center;"> 0.2 </td>
   <td style="text-align:center;"> setosa </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 4.7 </td>
   <td style="text-align:center;"> 3.2 </td>
   <td style="text-align:center;"> 1.3 </td>
   <td style="text-align:center;"> 0.2 </td>
   <td style="text-align:center;"> setosa </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 4.6 </td>
   <td style="text-align:center;"> 3.1 </td>
   <td style="text-align:center;"> 1.5 </td>
   <td style="text-align:center;"> 0.2 </td>
   <td style="text-align:center;"> setosa </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 5.0 </td>
   <td style="text-align:center;"> 3.6 </td>
   <td style="text-align:center;"> 1.4 </td>
   <td style="text-align:center;"> 0.2 </td>
   <td style="text-align:center;"> setosa </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 5.4 </td>
   <td style="text-align:center;"> 3.9 </td>
   <td style="text-align:center;"> 1.7 </td>
   <td style="text-align:center;"> 0.4 </td>
   <td style="text-align:center;"> setosa </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 4.6 </td>
   <td style="text-align:center;"> 3.4 </td>
   <td style="text-align:center;"> 1.4 </td>
   <td style="text-align:center;"> 0.3 </td>
   <td style="text-align:center;"> setosa </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 5.0 </td>
   <td style="text-align:center;"> 3.4 </td>
   <td style="text-align:center;"> 1.5 </td>
   <td style="text-align:center;"> 0.2 </td>
   <td style="text-align:center;"> setosa </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 4.4 </td>
   <td style="text-align:center;"> 2.9 </td>
   <td style="text-align:center;"> 1.4 </td>
   <td style="text-align:center;"> 0.2 </td>
   <td style="text-align:center;"> setosa </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 4.9 </td>
   <td style="text-align:center;"> 3.1 </td>
   <td style="text-align:center;"> 1.5 </td>
   <td style="text-align:center;"> 0.1 </td>
   <td style="text-align:center;"> setosa </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 5.4 </td>
   <td style="text-align:center;"> 3.7 </td>
   <td style="text-align:center;"> 1.5 </td>
   <td style="text-align:center;"> 0.2 </td>
   <td style="text-align:center;"> setosa </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 4.8 </td>
   <td style="text-align:center;"> 3.4 </td>
   <td style="text-align:center;"> 1.6 </td>
   <td style="text-align:center;"> 0.2 </td>
   <td style="text-align:center;"> setosa </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 4.8 </td>
   <td style="text-align:center;"> 3.0 </td>
   <td style="text-align:center;"> 1.4 </td>
   <td style="text-align:center;"> 0.1 </td>
   <td style="text-align:center;"> setosa </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 4.3 </td>
   <td style="text-align:center;"> 3.0 </td>
   <td style="text-align:center;"> 1.1 </td>
   <td style="text-align:center;"> 0.1 </td>
   <td style="text-align:center;"> setosa </td>
  </tr>
  <tr>
   <td style="text-align:center;"> 5.8 </td>
   <td style="text-align:center;"> 4.0 </td>
   <td style="text-align:center;"> 1.2 </td>
   <td style="text-align:center;"> 0.2 </td>
   <td style="text-align:center;"> setosa </td>
  </tr>
</tbody>
</table>



``` error
Error in knitr::include_graphics("../figure/palmerpenguins.png"): Cannot find the file(s): "../figure/palmerpenguins.png"
```

## Et praktisk eksemepel

Panum UngdomsForsker Forening, PUFF, er en studenterforening drevet af frivillige
medicinstuderende på Københavns Universitet, der arbejder for at forbedre vilkårene
for medicinsk studenterforskning. 

PUFF har gennem flere år tilbudt et kursus i statistisk metode & det statistiske
programmeringssprog R. Kurset blev gennemført over 5 eftermiddage/aftener á 3 timer,
og med en professor i biomedicinsk statistik som underviser. Efter COVID-19 
pandemien oplevede de vanskeligheder med at tiltrække deltagere til det relativt
dyre kursus.
at tiltrække 

## Hvor finder du den?
https://github.com/kubdatalab/R-toolbox

https://kubdatalab.github.io/R-toolbox/

# Referencer
