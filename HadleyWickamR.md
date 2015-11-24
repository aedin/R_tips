# Notes from HadleyWickham Talk
Aedin Culhane  
October 5, 2015  
In this talk Hadley wickham focussed on data manipulation mostly, for input (readr, readxl), initial manipulation using tidyr, dpylr (the next gen version of pylr), visualization with ggvis and model reporting (aka convert results to data frames) using broom.


see [tutorial](https://rpubs.com/bradleyboehmke/data_wrangling)


```r
install.packages("tidyr")
install.packages("dplyr")
install.packages("babynames")
install.packages("ggvis")
install.packages("broom")
```


```r
require(babynames)
```

```
## Loading required package: babynames
```

```r
library(dplyr)
```

```
## 
## Attaching package: 'dplyr'
## 
## The following objects are masked from 'package:stats':
## 
##     filter, lag
## 
## The following objects are masked from 'package:base':
## 
##     intersect, setdiff, setequal, union
```

```r
babynames %>% filter(year ==2013& prop>0.01)
```

```
## Source: local data frame [2 x 5]
## 
##    year   sex   name     n       prop
##   (dbl) (chr)  (chr) (int)      (dbl)
## 1  2013     F Sophia 21075 0.01103863
## 2  2013     F   Emma 20788 0.01088830
```

```r
babynames %>% filter(name%in%c("John", "Mary"))%>% group_by(name, sex)%>% summarise(n=sum(n))
```

```
## Source: local data frame [4 x 3]
## Groups: name [?]
## 
##    name   sex       n
##   (chr) (chr)   (int)
## 1  John     F   21632
## 2  John     M 5073958
## 3  Mary     F 4112464
## 4  Mary     M   15151
```


```r
require(ggplot2)
```

```
## Loading required package: ggplot2
```

```r
require(ggvis)
```

```
## Loading required package: ggvis
## 
## Attaching package: 'ggvis'
## 
## The following object is masked from 'package:ggplot2':
## 
##     resolution
```

```r
data(mpg)
data(mtcars)
mpg%>% ggvis(~displ, ~hwy)%>% layer_points()%>% layer_smooths()
```

<!--html_preserve--><div id="plot_id663023732-container" class="ggvis-output-container">
<div id="plot_id663023732" class="ggvis-output"></div>
<div class="plot-gear-icon">
<nav class="ggvis-control">
<a class="ggvis-dropdown-toggle" title="Controls" onclick="return false;"></a>
<ul class="ggvis-dropdown">
<li>
Renderer: 
<a id="plot_id663023732_renderer_svg" class="ggvis-renderer-button" onclick="return false;" data-plot-id="plot_id663023732" data-renderer="svg">SVG</a>
 | 
<a id="plot_id663023732_renderer_canvas" class="ggvis-renderer-button" onclick="return false;" data-plot-id="plot_id663023732" data-renderer="canvas">Canvas</a>
</li>
<li>
<a id="plot_id663023732_download" class="ggvis-download" data-plot-id="plot_id663023732">Download</a>
</li>
</ul>
</nav>
</div>
</div>
<script type="text/javascript">
var plot_id663023732_spec = {
  "data": [
    {
      "name": ".0",
      "format": {
        "type": "csv",
        "parse": {
          "displ": "number",
          "hwy": "number"
        }
      },
      "values": "\"displ\",\"hwy\"\n1.8,29\n1.8,29\n2,31\n2,30\n2.8,26\n2.8,26\n3.1,27\n1.8,26\n1.8,25\n2,28\n2,27\n2.8,25\n2.8,25\n3.1,25\n3.1,25\n2.8,24\n3.1,25\n4.2,23\n5.3,20\n5.3,15\n5.3,20\n5.7,17\n6,17\n5.7,26\n5.7,23\n6.2,26\n6.2,25\n7,24\n5.3,19\n5.3,14\n5.7,15\n6.5,17\n2.4,27\n2.4,30\n3.1,26\n3.5,29\n3.6,26\n2.4,24\n3,24\n3.3,22\n3.3,22\n3.3,24\n3.3,24\n3.3,17\n3.8,22\n3.8,21\n3.8,23\n4,23\n3.7,19\n3.7,18\n3.9,17\n3.9,17\n4.7,19\n4.7,19\n4.7,12\n5.2,17\n5.2,15\n3.9,17\n4.7,17\n4.7,12\n4.7,17\n5.2,16\n5.7,18\n5.9,15\n4.7,16\n4.7,12\n4.7,17\n4.7,17\n4.7,16\n4.7,12\n5.2,15\n5.2,16\n5.7,17\n5.9,15\n4.6,17\n5.4,17\n5.4,18\n4,17\n4,19\n4,17\n4,19\n4.6,19\n5,17\n4.2,17\n4.2,17\n4.6,16\n4.6,16\n4.6,17\n5.4,15\n5.4,17\n3.8,26\n3.8,25\n4,26\n4,24\n4.6,21\n4.6,22\n4.6,23\n4.6,22\n5.4,20\n1.6,33\n1.6,32\n1.6,32\n1.6,29\n1.6,32\n1.8,34\n1.8,36\n1.8,36\n2,29\n2.4,26\n2.4,27\n2.4,30\n2.4,31\n2.5,26\n2.5,26\n3.3,28\n2,26\n2,29\n2,28\n2,27\n2.7,24\n2.7,24\n2.7,24\n3,22\n3.7,19\n4,20\n4.7,17\n4.7,12\n4.7,19\n5.7,18\n6.1,14\n4,15\n4.2,18\n4.4,18\n4.6,15\n5.4,17\n5.4,16\n5.4,18\n4,17\n4,19\n4.6,19\n5,17\n2.4,29\n2.4,27\n2.5,31\n2.5,32\n3.5,27\n3.5,26\n3,26\n3,25\n3.5,25\n3.3,17\n3.3,17\n4,20\n5.6,18\n3.1,26\n3.8,26\n3.8,27\n3.8,28\n5.3,25\n2.5,25\n2.5,24\n2.5,27\n2.5,25\n2.5,26\n2.5,23\n2.2,26\n2.2,26\n2.5,26\n2.5,26\n2.5,25\n2.5,27\n2.5,25\n2.5,27\n2.7,20\n2.7,20\n3.4,19\n3.4,17\n4,20\n4.7,17\n2.2,29\n2.2,27\n2.4,31\n2.4,31\n3,26\n3,26\n3.5,28\n2.2,27\n2.2,29\n2.4,31\n2.4,31\n3,26\n3,26\n3.3,27\n1.8,30\n1.8,33\n1.8,35\n1.8,37\n1.8,35\n4.7,15\n5.7,18\n2.7,20\n2.7,20\n2.7,22\n3.4,17\n3.4,19\n4,18\n4,20\n2,29\n2,26\n2,29\n2,29\n2.8,24\n1.9,44\n2,29\n2,26\n2,29\n2,29\n2.5,29\n2.5,29\n2.8,23\n2.8,24\n1.9,44\n1.9,41\n2,29\n2,26\n2.5,28\n2.5,29\n1.8,29\n1.8,29\n2,28\n2,29\n2.8,26\n2.8,26\n3.6,26"
    },
    {
      "name": ".0/model_prediction1",
      "format": {
        "type": "csv",
        "parse": {
          "pred_": "number",
          "resp_": "number"
        }
      },
      "values": "\"pred_\",\"resp_\"\n1.6,33.0928566018538\n1.66835443037975,32.5107835503571\n1.73670886075949,31.942220282939\n1.80506329113924,31.3884848606776\n1.87341772151899,30.8508953446513\n1.94177215189873,30.3299957500339\n2.01012658227848,29.8238589188102\n2.07848101265823,29.3333742194063\n2.14683544303797,28.8583851390525\n2.21518987341772,28.3981429072318\n2.28354430379747,27.9518987534275\n2.35189873417722,27.5189039071225\n2.42025316455696,27.0987631133078\n2.48860759493671,26.6957836735878\n2.55696202531646,26.3090818821465\n2.6253164556962,25.9355884664112\n2.69367088607595,25.5722341538095\n2.7620253164557,25.2291795381194\n2.83037974683544,24.9181938113842\n2.89873417721519,24.6298749747969\n2.96708860759494,24.3546740169542\n3.03544303797468,24.0830419264527\n3.10379746835443,23.8054739954333\n3.17215189873418,23.5295892802633\n3.24050632911392,23.2646362481893\n3.30886075949367,23.0081062857482\n3.37721518987342,22.7574907794764\n3.44556962025316,22.5102811159107\n3.51392405063291,22.2639686815878\n3.58227848101266,22.0160448630443\n3.65063291139241,21.7640010468168\n3.71898734177215,21.5053286194421\n3.7873417721519,21.2375189674567\n3.85569620253165,20.9580634773974\n3.92405063291139,20.6636946027661\n3.99240506329114,20.3463825302921\n4.06075949367089,20.0114403884548\n4.12911392405063,19.667539399964\n4.19746835443038,19.3233507875295\n4.26582278481013,18.9875457738607\n4.33417721518987,18.6687955816675\n4.40253164556962,18.3757714336596\n4.47088607594937,18.1171445525467\n4.53924050632911,17.9015861610384\n4.60759493670886,17.7374782618847\n4.67594936708861,17.6038925094818\n4.74430379746835,17.4844691691521\n4.8126582278481,17.3803696350212\n4.88101265822785,17.2927553012146\n4.94936708860759,17.2227875618577\n5.01772151898734,17.171627811076\n5.08607594936709,17.140437442995\n5.15443037974684,17.1303778517403\n5.22278481012658,17.1426104314373\n5.29113924050633,17.1782965762116\n5.35949367088608,17.236490288008\n5.42784810126582,17.3142595889582\n5.49620253164557,17.4115496666741\n5.56455696202532,17.5283491704686\n5.63291139240506,17.6646467496544\n5.70126582278481,17.8204310535444\n5.76962025316456,17.9956907314514\n5.8379746835443,18.1904144326882\n5.90632911392405,18.4045908065676\n5.9746835443038,18.6382085024024\n6.04303797468354,18.8912561695054\n6.11139240506329,19.1637224571895\n6.17974683544304,19.4555960147675\n6.24810126582278,19.7668654915521\n6.31645569620253,20.0975195368563\n6.38481012658228,20.4475467999927\n6.45316455696203,20.8169359302743\n6.52151898734177,21.2056755770139\n6.58987341772152,21.6137543895241\n6.65822784810127,22.041161017118\n6.72658227848101,22.4878841091083\n6.79493670886076,22.9539123148077\n6.86329113924051,23.4392342835292\n6.93164556962025,23.9438386645854\n7,24.4677141072894"
    },
    {
      "name": "scale/x",
      "format": {
        "type": "csv",
        "parse": {
          "domain": "number"
        }
      },
      "values": "\"domain\"\n1.33\n7.27"
    },
    {
      "name": "scale/y",
      "format": {
        "type": "csv",
        "parse": {
          "domain": "number"
        }
      },
      "values": "\"domain\"\n10.4\n45.6"
    }
  ],
  "scales": [
    {
      "name": "x",
      "domain": {
        "data": "scale/x",
        "field": "data.domain"
      },
      "zero": false,
      "nice": false,
      "clamp": false,
      "range": "width"
    },
    {
      "name": "y",
      "domain": {
        "data": "scale/y",
        "field": "data.domain"
      },
      "zero": false,
      "nice": false,
      "clamp": false,
      "range": "height"
    }
  ],
  "marks": [
    {
      "type": "symbol",
      "properties": {
        "update": {
          "fill": {
            "value": "#000000"
          },
          "size": {
            "value": 50
          },
          "x": {
            "scale": "x",
            "field": "data.displ"
          },
          "y": {
            "scale": "y",
            "field": "data.hwy"
          }
        },
        "ggvis": {
          "data": {
            "value": ".0"
          }
        }
      },
      "from": {
        "data": ".0"
      }
    },
    {
      "type": "line",
      "properties": {
        "update": {
          "stroke": {
            "value": "#000000"
          },
          "strokeWidth": {
            "value": 2
          },
          "x": {
            "scale": "x",
            "field": "data.pred_"
          },
          "y": {
            "scale": "y",
            "field": "data.resp_"
          },
          "fill": {
            "value": "transparent"
          }
        },
        "ggvis": {
          "data": {
            "value": ".0/model_prediction1"
          }
        }
      },
      "from": {
        "data": ".0/model_prediction1"
      }
    }
  ],
  "legends": [],
  "axes": [
    {
      "type": "x",
      "scale": "x",
      "orient": "bottom",
      "layer": "back",
      "grid": true,
      "title": "displ"
    },
    {
      "type": "y",
      "scale": "y",
      "orient": "left",
      "layer": "back",
      "grid": true,
      "title": "hwy"
    }
  ],
  "padding": null,
  "ggvis_opts": {
    "keep_aspect": false,
    "resizable": true,
    "padding": {},
    "duration": 250,
    "renderer": "svg",
    "hover_duration": 0,
    "width": 672,
    "height": 480
  },
  "handlers": null
};
ggvis.getPlot("plot_id663023732").parseSpec(plot_id663023732_spec);
</script><!--/html_preserve-->



```r
library(broom)
lmfit <- lm(mpg ~ wt, mtcars)
lmfit
```

```
## 
## Call:
## lm(formula = mpg ~ wt, data = mtcars)
## 
## Coefficients:
## (Intercept)           wt  
##      37.285       -5.344
```

```r
tidy(lmfit)
```

```
##          term  estimate std.error statistic      p.value
## 1 (Intercept) 37.285126  1.877627 19.857575 8.241799e-19
## 2          wt -5.344472  0.559101 -9.559044 1.293959e-10
```


Checking if broom works with survival (coxph) 

```r
require(survival)
```

```
## Loading required package: survival
```

```r
data(lung)
xfit<-coxph(Surv(time, status) ~ ph.ecog + tt(age), data=lung)
xfit
```

```
## Call:
## coxph(formula = Surv(time, status) ~ ph.ecog + tt(age), data = lung)
## 
## 
##            coef exp(coef) se(coef)    z       p
## ph.ecog 0.46216   1.58750  0.11346 4.07 4.6e-05
## tt(age) 0.00521   1.00522  0.00250 2.08   0.038
## 
## Likelihood ratio test=20.6  on 2 df, p=3.3e-05
## n= 227, number of events= 164 
##    (1 observation deleted due to missingness)
```

```r
tidy(xfit)
```

```
##      term    estimate   std.error statistic      p.value     conf.low
## 1 ph.ecog 0.462163407 0.113455876  4.073508 4.631028e-05 0.2397939763
## 2 tt(age) 0.005210397 0.002504811  2.080156 3.751127e-02 0.0003010571
##    conf.high
## 1 0.68453284
## 2 0.01011974
```
