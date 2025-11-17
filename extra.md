---
title: 'Extra'
teaching: 10
exercises: 2
---

:::::::::::::::::::::::::::::::::::::: questions 

- Spørgsmål I er kommet med

::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: objectives

- Annotering af ggplots
- Sankey-plots


::::::::::::::::::::::::::::::::::::::::::::::::

## Mysteriet om de forskellige histogrammer

Vi oplevede at der var forskelle på hvordan vores histogrammer så ud.

Årsagen er fundet. Med opgraderingen af ggplot2 til version 4.0.0 blev den måde "bins" beregnes på konsolideret.

Den var hidtil blevet foretaget lidt forskelligt afhængigt af hvilken type plot der blev lavet, og ved opgradringen blev 
det samlet til en og kun en måde. Med det resultat at beregningen af "bins" ændredede sig for `geom_histogram`. 
De af jer der havde den nyeste version fik derfor et histogram der så anderledes ud end de af jer (underviseren inklusive),
der havde den gamle version af ggplot2. 

For at komplicere det hele yderligere, gav en opdatering af tidyverse med "install.packages("tidyverse")" _ikke_ den nye version 4.0.0 af ggplot2. Der skulle en "install.packages("ggplot2")" til for at rette op på problemet.

## Annotering af ggplots

Hvordan tilføjer vi R^2 til vores plot med en lineær regression?

To måder.

### ggpmisc

En pakke der kan sådan noget findes, `ggpmisc`


``` r
# install.packages("ggpmisc")
library(ggpmisc)
```

``` output
Loading required package: ggpp
```

``` output
Loading required package: ggplot2
```

``` output
Registered S3 methods overwritten by 'ggpp':
  method                  from   
  heightDetails.titleGrob ggplot2
  widthDetails.titleGrob  ggplot2
```

``` output

Attaching package: 'ggpp'
```

``` output
The following object is masked from 'package:ggplot2':

    annotate
```

Her tager vi datasættet `mtcars`:


``` r
library(ggplot2)
mtcars |> 
   ggplot(aes(x = wt, y = mpg)) +
   geom_point() +
   geom_smooth(method = "lm") +
   stat_poly_eq(
      aes(label = after_stat(eq.label)),
      formula = y ~x,
      parse = TRUE) +
  stat_poly_eq(
    aes(label = after_stat(rr.label)),
    formula = y ~ x,
    parse = TRUE,
    vjust = 1.5
  )   
```

``` output
`geom_smooth()` using formula = 'y ~ x'
```

<img src="fig/extra-rendered-unnamed-chunk-2-1.png" style="display: block; margin: auto;" />


Det kontrollerer ikke positionen særlig godt.

### Den alternative 

Hvad der kan kontrollere position helt som vi vil, og kan bruges til at tilføje andet end R^2 er `annotate()` funktionen.

Det kræver at vi selv beregner R^2


``` r
lin_model <- lm(mpg ~ wt, data = mtcars)
lin_model <- summary(lin_model)
r2 <- lin_model$r.squared

mtcars |> 
   ggplot(aes(x = wt, y = mpg)) +
   geom_point() +
   geom_smooth(method = "lm") +
   annotate("text", x = 3, y = 25, label = r2)
```

``` output
`geom_smooth()` using formula = 'y ~ x'
```

<img src="fig/extra-rendered-unnamed-chunk-3-1.png" style="display: block; margin: auto;" />

Man kan med fordel afrunde r2, og sætte lidt tekst ind:


``` r
r2 <- paste0("R^2 = ", round(r2, 3))
r2
```

``` output
[1] "R^2 = 0.753"
```

Det er noget pilleri at få placeret annotationen præcist hvor man vil have den, så pas på med at blive for perfektionistisk!

## Sankey diagrammer

Flere pakker findes, den der er lettest at gå til er nok `ggalluvial`

Det tricky er at få formatteret data til det rette format, dernæst er det relativt enkelt.

Start med at loade pakken:


``` r
library(ggalluvial)
```

Få derefter formatteret data til at have formen:


``` r
df <- data.frame(
  from = c("A", "A", "B", "B"),
  to   = c("X", "Y", "X", "Y"),
  n    = c(10, 5, 3, 8)
)

df
```

``` output
  from to  n
1    A  X 10
2    A  Y  5
3    B  X  3
4    B  Y  8
```

Herefter laver vi det grundlæggende ggplot. Bemærk at de ting vi mapper til er specielle - for det er en speciel
geometri vi vil plotte:


``` r
sankey <- df |> 
   ggplot(aes(axis1 = from,
              axis2 = to,
              y = n)) +
   geom_alluvium(aes(fill = from),
   width = 0.1)
sankey
```

``` error
Error in gg_par(col = data$colour %||% NA, fill = fill_alpha(data$fill %||% : could not find function "gg_par"
```

Detaljer kan fyldes på:


``` r
sankey +
  geom_stratum(width = 1/10, fill = "grey80", colour = "grey20") +
    geom_label(
    stat = "stratum",
    aes(label = after_stat(stratum))
  ) +
  scale_x_discrete(
    limits = c("Fra", "Til"),
    expand = c(.05, .05)
  ) +
  labs(
    y    = "Antal",
    fill = "Fra"
  ) +
  theme_minimal()
```

``` error
Error in gg_par(col = data$colour %||% NA, fill = fill_alpha(data$fill %||% : could not find function "gg_par"
```

Der kan tilføjes flere trin i flowet - start med at få det i data framen:


``` r
df3 <- data.frame(
  step1 = c("A", "A", "B", "B"),
  step2 = c("X", "Y", "X", "Y"),
  step3 = c("K", "K", "L", "L"),
  n     = c(10, 5, 3, 8)
)
df3
```

``` output
  step1 step2 step3  n
1     A     X     K 10
2     A     Y     K  5
3     B     X     L  3
4     B     Y     L  8
```



``` r
df3 |> 
   ggplot(
  aes(
    axis1 = step1,
    axis2 = step2,
    axis3 = step3,
    y     = n
  )
) +
  geom_alluvium(aes(fill = step1), width = 1/12) +
  geom_stratum(width = 1/12, fill = "grey80", colour = "grey20")
```

``` error
Error in gg_par(col = data$colour %||% NA, fill = fill_alpha(data$fill %||% : could not find function "gg_par"
```


::::::::::::::::::::::::::::::::::::: keypoints 

- Use `.md` files for episodes when you want static content
- Use `.Rmd` files for episodes when you need to generate output
- Run `sandpaper::check_lesson()` to identify any issues with your lesson
- Run `sandpaper::build_lesson()` to preview your lesson locally

::::::::::::::::::::::::::::::::::::::::::::::::

