
<!-- rnb-text-begin -->

---
title: "CTA1 promoter bashing"
author: "JY"
date: "2023-11-24 (updated 2024-05-17)"
output: 
  html_notebook:
    code_folding: hide
    toc: true
    toc_float: true
---


<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxubGlicmFyeSh0aWR5dmVyc2UpXG5gYGAifQ== -->

```r
library(tidyverse)
```

<!-- rnb-source-end -->

<!-- rnb-output-begin eyJkYXRhIjoi4pSA4pSAIEF0dGFjaGluZyBjb3JlIHRpZHl2ZXJzZSBwYWNrYWdlcyDilIDilIDilIDilIDilIDilIDilIDilIDilIDilIDilIDilIDilIDilIDilIDilIDilIDilIDilIDilIDilIDilIDilIDilIDilIDilIDilIDilIDilIDilIDilIDilIDilIDilIDilIDilIDilIDilIDilIDilIDilIDilIDilIDilIDilIDilIDilIDilIDilIDilIDilIDilIDilIDilIDilIDilIDilIDilIDilIDilIDilIDilIDilIDilIDilIDilIDilIAgdGlkeXZlcnNlIDIuMC4wIOKUgOKUgFxu4pyUIGRwbHlyICAgICAxLjEuNCAgICAg4pyUIHJlYWRyICAgICAyLjEuNVxu4pyUIGZvcmNhdHMgICAxLjAuMCAgICAg4pyUIHN0cmluZ3IgICAxLjUuMVxu4pyUIGdncGxvdDIgICAzLjUuMCAgICAg4pyUIHRpYmJsZSAgICAzLjIuMVxu4pyUIGx1YnJpZGF0ZSAxLjkuMyAgICAg4pyUIHRpZHlyICAgICAxLjMuMVxu4pyUIHB1cnJyICAgICAxLjAuMiAgICAg4pSA4pSAIENvbmZsaWN0cyDilIDilIDilIDilIDilIDilIDilIDilIDilIDilIDilIDilIDilIDilIDilIDilIDilIDilIDilIDilIDilIDilIDilIDilIDilIDilIDilIDilIDilIDilIDilIDilIDilIDilIDilIDilIDilIDilIDilIDilIDilIDilIDilIDilIDilIDilIDilIDilIDilIDilIDilIDilIDilIDilIDilIDilIDilIDilIDilIDilIDilIDilIDilIDilIDilIDilIDilIDilIDilIDilIDilIDilIDilIDilIDilIDilIDilIDilIDilIDilIDilIDilIDilIDilIDilIAgdGlkeXZlcnNlX2NvbmZsaWN0cygpIOKUgOKUgFxu4pyWIGRwbHlyOjpmaWx0ZXIoKSBtYXNrcyBzdGF0czo6ZmlsdGVyKClcbuKcliBkcGx5cjo6bGFnKCkgICAgbWFza3Mgc3RhdHM6OmxhZygpXG7ihLkgVXNlIHRoZSBcdTAwMWJdODs7aHR0cDovL2NvbmZsaWN0ZWQuci1saWIub3JnL1x1MDAwN2NvbmZsaWN0ZWQgcGFja2FnZVx1MDAxYl04OztcdTAwMDcgdG8gZm9yY2UgYWxsIGNvbmZsaWN0cyB0byBiZWNvbWUgZXJyb3JzXG4ifQ== -->

```
── Attaching core tidyverse packages ─────────────────────────────────────────────────────────────────── tidyverse 2.0.0 ──
✔ dplyr     1.1.4     ✔ readr     2.1.5
✔ forcats   1.0.0     ✔ stringr   1.5.1
✔ ggplot2   3.5.0     ✔ tibble    3.2.1
✔ lubridate 1.9.3     ✔ tidyr     1.3.1
✔ purrr     1.0.2     ── Conflicts ───────────────────────────────────────────────────────────────────────────────────── tidyverse_conflicts() ──
✖ dplyr::filter() masks stats::filter()
✖ dplyr::lag()    masks stats::lag()
ℹ Use the ]8;;http://conflicted.r-lib.org/conflicted package]8;; to force all conflicts to become errors
```



<!-- rnb-output-end -->

<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxubGlicmFyeShnZ3RleHQpXG4jbGlicmFyeShtZ2N2KVxuI2xpYnJhcnkoYnJvb20pXG5saWJyYXJ5KGNvd3Bsb3QpXG5gYGAifQ== -->

```r
library(ggtext)
#library(mgcv)
#library(broom)
library(cowplot)
```

<!-- rnb-source-end -->

<!-- rnb-output-begin eyJkYXRhIjoiXG5BdHRhY2hpbmcgcGFja2FnZTog4oCYY293cGxvdOKAmVxuXG5UaGUgZm9sbG93aW5nIG9iamVjdCBpcyBtYXNrZWQgZnJvbSDigJhwYWNrYWdlOmx1YnJpZGF0ZeKAmTpcblxuICAgIHN0YW1wXG4ifQ== -->

```

Attaching package: ‘cowplot’

The following object is masked from ‘package:lubridate’:

    stamp
```



<!-- rnb-output-end -->

<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxubGlicmFyeShnZ3BhdHRlcm4pXG4jU3lzLnNldGVudihMQU5HID0gXCJlblwiKVxuYGBgIn0= -->

```r
library(ggpattern)
#Sys.setenv(LANG = "en")
```

<!-- rnb-source-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->


## Goal
Plot the dynamics for CTA1 promoter bashing variants under - Pi and 2 mM H2O2 treatment

## Common plotting functions
**Update 2022-11-08** 
This list is used as a shared plotting set up.

<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxucC50aW1lY291cnNlIDwtIGxpc3QoXG4gIHN0YXRfc3VtbWFyeShmdW4gPSBcIm1lYW5cIiwgZ2VvbSA9IFwicG9pbnRcIiwgc2l6ZSA9IDMpLFxuICBzdGF0X3N1bW1hcnkoZnVuLmRhdGEgPSBcIm1lYW5fY2xfYm9vdFwiLCBnZW9tID0gXCJlcnJvcmJhclwiLCB3aWR0aCA9IDMpLFxuICBzdGF0X3Ntb290aChhZXMoc2l6ZSA9IEdlbm90eXBlID09IFwiV1RcIiksIG1ldGhvZCA9IFwibG9lc3NcIiwgXG4gICAgICAgICAgICAgIGZvcm11bGEgPSAneX54Jywgc2UgPSBGQUxTRSksXG4gIHNjYWxlX3hfY29udGludW91cyhicmVha3MgPSBzZXEoMCwyNDAsMzApKSxcbiAgc2NhbGVfc2l6ZV9tYW51YWwodmFsdWVzID0gYygwLjgsIDEuNSksIGd1aWRlID0gXCJub25lXCIpLFxuICBsYWJzKHggPSBcIlRpbWUgKG1pbilcIiwgeSA9IFwiQ3RhMS1HRlAgcHJvdGVpbiBsZXZlbCAoYS51LilcIiksXG4gIHRoZW1lX2Nvd3Bsb3QobGluZV9zaXplID0gMC43LCBmb250X3NpemUgPSAxNCksXG4gIHRoZW1lKGxlZ2VuZC5wb3NpdGlvbj1jKDAuMDUsMC43NSksIFxuICAgICAgICAjbGVnZW5kLmJveC5iYWNrZ3JvdW5kID0gZWxlbWVudF9yZWN0KGNvbG9yID0gXCJibGFja1wiKSxcbiAgICAgICAgI2xlZ2VuZC5ib3gubWFyZ2luID0gbWFyZ2luKDMsMywzLDMpLFxuICAgICAgICBsZWdlbmQudGV4dCA9IGVsZW1lbnRfdGV4dChmYWNlID0gMyksIFxuICAgICAgICBsZWdlbmQudGl0bGUgPSBlbGVtZW50X3RleHQoKSxcbiAgICAgICAgYXhpcy50aXRsZSA9IGVsZW1lbnRfdGV4dChzaXplID0gcmVsKDEpKSwgXG4gICAgICAgICNheGlzLnRpdGxlLnggPSBlbGVtZW50X2JsYW5rKCksXG4gICAgICAgIGF4aXMudGV4dC54ID0gZWxlbWVudF90ZXh0KGhqdXN0PTAuNSksIGF4aXMudGV4dCA9IGVsZW1lbnRfdGV4dChzaXplID0gcmVsKDEpKSxcbiAgKVxuKVxuYGBgIn0= -->

```r
p.timecourse <- list(
  stat_summary(fun = "mean", geom = "point", size = 3),
  stat_summary(fun.data = "mean_cl_boot", geom = "errorbar", width = 3),
  stat_smooth(aes(size = Genotype == "WT"), method = "loess", 
              formula = 'y~x', se = FALSE),
  scale_x_continuous(breaks = seq(0,240,30)),
  scale_size_manual(values = c(0.8, 1.5), guide = "none"),
  labs(x = "Time (min)", y = "Cta1-GFP protein level (a.u.)"),
  theme_cowplot(line_size = 0.7, font_size = 14),
  theme(legend.position=c(0.05,0.75), 
        #legend.box.background = element_rect(color = "black"),
        #legend.box.margin = margin(3,3,3,3),
        legend.text = element_text(face = 3), 
        legend.title = element_text(),
        axis.title = element_text(size = rel(1)), 
        #axis.title.x = element_blank(),
        axis.text.x = element_text(hjust=0.5), axis.text = element_text(size = rel(1)),
  )
)
```

<!-- rnb-source-end -->

<!-- rnb-output-begin eyJkYXRhIjoiV2FybmluZzogVXNpbmcgYHNpemVgIGFlc3RoZXRpYyBmb3IgbGluZXMgd2FzIGRlcHJlY2F0ZWQgaW4gZ2dwbG90MiAzLjQuMC5cblBsZWFzZSB1c2UgYGxpbmV3aWR0aGAgaW5zdGVhZC5XYXJuaW5nOiBBIG51bWVyaWMgYGxlZ2VuZC5wb3NpdGlvbmAgYXJndW1lbnQgaW4gYHRoZW1lKClgIHdhcyBkZXByZWNhdGVkIGluIGdncGxvdDIgMy41LjAuXG5QbGVhc2UgdXNlIHRoZSBgbGVnZW5kLnBvc2l0aW9uLmluc2lkZWAgYXJndW1lbnQgb2YgYHRoZW1lKClgIGluc3RlYWQuXG4ifQ== -->

```
Warning: Using `size` aesthetic for lines was deprecated in ggplot2 3.4.0.
Please use `linewidth` instead.Warning: A numeric `legend.position` argument in `theme()` was deprecated in ggplot2 3.5.0.
Please use the `legend.position.inside` argument of `theme()` instead.
```



<!-- rnb-output-end -->

<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxubWVhbi50aW1lY291cnNlIDwtIGxpc3QoXG4gIHN0YXRfc3VtbWFyeShmdW4gPSBcIm1lYW5cIiwgZ2VvbSA9IFwicG9pbnRcIiwgc2l6ZSA9IDMpLFxuICBzdGF0X3Ntb290aChhZXMoc2l6ZSA9IEdlbm90eXBlID09IFwiV1RcIiksIG1ldGhvZCA9IFwibG9lc3NcIiwgXG4gICAgICAgICAgICAgIGZvcm11bGEgPSAneX54Jywgc2UgPSBGQUxTRSksXG4gIHNjYWxlX3hfY29udGludW91cyhicmVha3MgPSBzZXEoMCwyNDAsMzApKSxcbiAgc2NhbGVfc2l6ZV9tYW51YWwodmFsdWVzID0gYygwLjgsIDEuNSksIGd1aWRlID0gXCJub25lXCIpLFxuICBsYWJzKHggPSBcIlRpbWUgKG1pbilcIiwgeSA9IFwiQ3RhMS1HRlAgcHJvdGVpbiBsZXZlbCAoYS51LilcIiksXG4gIHRoZW1lX2Nvd3Bsb3QobGluZV9zaXplID0gMC43LCBmb250X3NpemUgPSAxNCksXG4gIHRoZW1lKGxlZ2VuZC5wb3NpdGlvbj1jKDAuMDIsMC45KSxcbiAgICAgICAgI2xlZ2VuZC5kaXJlY3Rpb24gPSBcImhvcml6b250YWxcIixcbiAgICAgICAgI2xlZ2VuZC5ib3guYmFja2dyb3VuZCA9IGVsZW1lbnRfcmVjdChjb2xvciA9IFwiYmxhY2tcIiksXG4gICAgICAgICNsZWdlbmQuYm94Lm1hcmdpbiA9IG1hcmdpbigzLDMsMywzKSxcbiAgICAgICAgbGVnZW5kLnRleHQgPSBlbGVtZW50X3RleHQoZmFjZSA9IDMpLCBcbiAgICAgICAgbGVnZW5kLnRpdGxlID0gZWxlbWVudF90ZXh0KCksXG4gICAgICAgIGF4aXMudGl0bGUgPSBlbGVtZW50X3RleHQoc2l6ZSA9IHJlbCgxKSksIFxuICAgICAgICAjYXhpcy50aXRsZS54ID0gZWxlbWVudF9ibGFuaygpLFxuICAgICAgICBheGlzLnRleHQueCA9IGVsZW1lbnRfdGV4dChoanVzdD0wLjUpLCBheGlzLnRleHQgPSBlbGVtZW50X3RleHQoc2l6ZSA9IHJlbCgxKSksXG4gIClcbilcblxuXG5cbnNjYXR0ZXIgPC0gbGlzdChzdGF0X3N1bW1hcnkoZnVuID0gXCJtZWFuXCIsIGdlb20gPSBcInBvaW50XCIsIHNpemUgPSAzKSxcbiAgICAgICAgICAgICAgICBzY2FsZV95X2NvbnRpbnVvdXMoYnJlYWtzID0gc2VxKDAsMS4wLDAuMjUpKSxcbiAgICAgICAgICAgICAgICBzY2FsZV94X2NvbnRpbnVvdXMoYnJlYWtzID0gc2VxKDAsMS4wLDAuMjUpKSxcbiAgICAgICAgICAgICAgICBzY2FsZV9zaXplX21hbnVhbCh2YWx1ZXMgPSBjKDAuOCwgMS41KSwgZ3VpZGUgPSBcIm5vbmVcIiksXG4gICAgICAgICAgICAgICAgZXhwYW5kX2xpbWl0cyh4ID0gMCwgeSA9IDApLFxuICAgICAgICAgICAgICAgIHRoZW1lX2Nvd3Bsb3QobGluZV9zaXplID0gMC43LCBmb250X3NpemUgPSAxNCksXG4gICAgICAgICAgICAgICAgdGhlbWUobGVnZW5kLnBvc2l0aW9uPWMoMC4wMiwwLjgyKSxcbiAgICAgICAgICAgICAgICBsZWdlbmQudGV4dCA9IGVsZW1lbnRfdGV4dChmYWNlID0gMyksIFxuICAgICAgICAgICAgICAgIGxlZ2VuZC50aXRsZSA9IGVsZW1lbnRfdGV4dCgpLFxuICAgICAgICAgICAgICAgIGF4aXMudGl0bGUgPSBlbGVtZW50X3RleHQoc2l6ZSA9IHJlbCgxKSksIFxuICAgICAgICAgICAgICAgIGF4aXMudGV4dC54ID0gZWxlbWVudF90ZXh0KGhqdXN0PTAuNSksIGF4aXMudGV4dCA9IGVsZW1lbnRfdGV4dChzaXplID0gcmVsKDEpKSkpXG5cbmJhci5saXN0IDwtIGxpc3QoXG4gIHN0YXRfc3VtbWFyeShmdW4uZGF0YSA9IFwibWVhbl9jbF9ib290XCIsIGNvbmYuaW50ID0gLjk1LCBjb2xvdXIgPSBcInJlZFwiLCBsaW5ld2lkdGggPSAxLCBzaXplID0gMC44KSxcbiAgc2NhbGVfc2l6ZV9tYW51YWwodmFsdWVzID0gYygwLjgsIDEuNSksIGd1aWRlID0gXCJub25lXCIpLFxuICBsYWJzKHggPXBhc3RlMChcIjJtTSBIMk8yLCBPTCB2YXJpYW50cyBcIiwgZGVwYXJzZTEoc3Vic3RpdHV0ZShpbnB1dF90cCkpLCBcIiBtaW5cIiksIHkgPSBcIkN0YTEtR0ZQIHByb3RlaW4gbGV2ZWwgKGEudS4pXCIpLFxuICB0aGVtZV9jb3dwbG90KGxpbmVfc2l6ZSA9IDAuNywgZm9udF9zaXplID0gMTQpLFxuICB0aGVtZShsZWdlbmQucG9zaXRpb249YygwLjAyLDAuOSksXG4gICAgICAgICNsZWdlbmQuZGlyZWN0aW9uID0gXCJob3Jpem9udGFsXCIsXG4gICAgICAgICNsZWdlbmQuYm94LmJhY2tncm91bmQgPSBlbGVtZW50X3JlY3QoY29sb3IgPSBcImJsYWNrXCIpLFxuICAgICAgICAjbGVnZW5kLmJveC5tYXJnaW4gPSBtYXJnaW4oMywzLDMsMyksXG4gICAgICAgIGxlZ2VuZC50ZXh0ID0gZWxlbWVudF90ZXh0KGZhY2UgPSAzKSwgXG4gICAgICAgIGxlZ2VuZC50aXRsZSA9IGVsZW1lbnRfdGV4dCgpLFxuICAgICAgICBheGlzLnRpdGxlID0gZWxlbWVudF90ZXh0KHNpemUgPSByZWwoMSkpLCBcbiAgICAgICAgI2F4aXMudGl0bGUueCA9IGVsZW1lbnRfYmxhbmsoKSxcbiAgICAgICAgYXhpcy50ZXh0LnggPSBlbGVtZW50X3RleHQoaGp1c3Q9MC41KSwgYXhpcy50ZXh0ID0gZWxlbWVudF90ZXh0KHNpemUgPSByZWwoMSkpLFxuICApXG4pXG5gYGAifQ== -->

```r
mean.timecourse <- list(
  stat_summary(fun = "mean", geom = "point", size = 3),
  stat_smooth(aes(size = Genotype == "WT"), method = "loess", 
              formula = 'y~x', se = FALSE),
  scale_x_continuous(breaks = seq(0,240,30)),
  scale_size_manual(values = c(0.8, 1.5), guide = "none"),
  labs(x = "Time (min)", y = "Cta1-GFP protein level (a.u.)"),
  theme_cowplot(line_size = 0.7, font_size = 14),
  theme(legend.position=c(0.02,0.9),
        #legend.direction = "horizontal",
        #legend.box.background = element_rect(color = "black"),
        #legend.box.margin = margin(3,3,3,3),
        legend.text = element_text(face = 3), 
        legend.title = element_text(),
        axis.title = element_text(size = rel(1)), 
        #axis.title.x = element_blank(),
        axis.text.x = element_text(hjust=0.5), axis.text = element_text(size = rel(1)),
  )
)



scatter <- list(stat_summary(fun = "mean", geom = "point", size = 3),
                scale_y_continuous(breaks = seq(0,1.0,0.25)),
                scale_x_continuous(breaks = seq(0,1.0,0.25)),
                scale_size_manual(values = c(0.8, 1.5), guide = "none"),
                expand_limits(x = 0, y = 0),
                theme_cowplot(line_size = 0.7, font_size = 14),
                theme(legend.position=c(0.02,0.82),
                legend.text = element_text(face = 3), 
                legend.title = element_text(),
                axis.title = element_text(size = rel(1)), 
                axis.text.x = element_text(hjust=0.5), axis.text = element_text(size = rel(1))))

bar.list <- list(
  stat_summary(fun.data = "mean_cl_boot", conf.int = .95, colour = "red", linewidth = 1, size = 0.8),
  scale_size_manual(values = c(0.8, 1.5), guide = "none"),
  labs(x =paste0("2mM H2O2, OL variants ", deparse1(substitute(input_tp)), " min"), y = "Cta1-GFP protein level (a.u.)"),
  theme_cowplot(line_size = 0.7, font_size = 14),
  theme(legend.position=c(0.02,0.9),
        #legend.direction = "horizontal",
        #legend.box.background = element_rect(color = "black"),
        #legend.box.margin = margin(3,3,3,3),
        legend.text = element_text(face = 3), 
        legend.title = element_text(),
        axis.title = element_text(size = rel(1)), 
        #axis.title.x = element_blank(),
        axis.text.x = element_text(hjust=0.5), axis.text = element_text(size = rel(1)),
  )
)
```

<!-- rnb-source-end -->

<!-- rnb-output-begin eyJkYXRhIjoiV2FybmluZzogSWdub3JpbmcgdW5rbm93biBwYXJhbWV0ZXJzOiBgY29uZi5pbnRgXG4ifQ== -->

```
Warning: Ignoring unknown parameters: `conf.int`
```



<!-- rnb-output-end -->

<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuYmFyLmxpc3Qubm8uc3RhdCA8LSBsaXN0KFxuICAjc3RhdF9zdW1tYXJ5KGZ1bi5kYXRhID0gXCJtZWFuX2NsX2Jvb3RcIiwgY29uZi5pbnQgPSAuOTUsIGNvbG91ciA9IFwicmVkXCIsIGxpbmV3aWR0aCA9IDEsIHNpemUgPSAwLjgpLFxuICBzY2FsZV9zaXplX21hbnVhbCh2YWx1ZXMgPSBjKDAuOCwgMS41KSwgZ3VpZGUgPSBcIm5vbmVcIiksXG4gIHRoZW1lX2Nvd3Bsb3QobGluZV9zaXplID0gMC43LCBmb250X3NpemUgPSAxNCksXG4gIHRoZW1lKGxlZ2VuZC5wb3NpdGlvbj1jKDAuMDIsMC45KSxcbiAgICAgICAgI2xlZ2VuZC5kaXJlY3Rpb24gPSBcImhvcml6b250YWxcIixcbiAgICAgICAgI2xlZ2VuZC5ib3guYmFja2dyb3VuZCA9IGVsZW1lbnRfcmVjdChjb2xvciA9IFwiYmxhY2tcIiksXG4gICAgICAgICNsZWdlbmQuYm94Lm1hcmdpbiA9IG1hcmdpbigzLDMsMywzKSxcbiAgICAgICAgbGVnZW5kLnRleHQgPSBlbGVtZW50X3RleHQoZmFjZSA9IDMpLCBcbiAgICAgICAgbGVnZW5kLnRpdGxlID0gZWxlbWVudF90ZXh0KCksXG4gICAgICAgIGF4aXMudGl0bGUgPSBlbGVtZW50X3RleHQoc2l6ZSA9IHJlbCgxKSksIFxuICAgICAgICAjYXhpcy50aXRsZS54ID0gZWxlbWVudF9ibGFuaygpLFxuICAgICAgICBheGlzLnRleHQueCA9IGVsZW1lbnRfdGV4dChoanVzdD0wLjUpLCBheGlzLnRleHQgPSBlbGVtZW50X3RleHQoc2l6ZSA9IHJlbCgxKSksXG4gIClcbilcbiAgXG5cblxuYGBgIn0= -->

```r
bar.list.no.stat <- list(
  #stat_summary(fun.data = "mean_cl_boot", conf.int = .95, colour = "red", linewidth = 1, size = 0.8),
  scale_size_manual(values = c(0.8, 1.5), guide = "none"),
  theme_cowplot(line_size = 0.7, font_size = 14),
  theme(legend.position=c(0.02,0.9),
        #legend.direction = "horizontal",
        #legend.box.background = element_rect(color = "black"),
        #legend.box.margin = margin(3,3,3,3),
        legend.text = element_text(face = 3), 
        legend.title = element_text(),
        axis.title = element_text(size = rel(1)), 
        #axis.title.x = element_blank(),
        axis.text.x = element_text(hjust=0.5), axis.text = element_text(size = rel(1)),
  )
)
  

```

<!-- rnb-source-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->


## CTA1 induction in OL variants

#### -Pi Data
Import data and get the replicate, time and genotype info

<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuZmlsZXMgPC0gZGlyKFwiaW5wdXQvT0xfMFBpXCIsIHBhdHRlcm4gPSBcImQwMSpcIikgIyBnZXQgdGhlIGZpbGUgbmFtZXMgb2YgdGhlIG1lcmdlZFxuZmlsZXMgPC0gZmlsZS5wYXRoKFwiaW5wdXQvL09MXzBQaVwiLCBmaWxlcykgICAgICAgICAjIHRoaXMgYXBwZW5kcyB0aGUgZGlyZWN0b3J5IHRvIHRoZSBmaWxlIG5hbWVzXG5uYW1lcyhmaWxlcykgPC0gYyhcIlJlcDEtMFBpLUN0cmxcIixcIlJlcDItMFBpLUN0cmxcIiwgXCJSZXAzLTBQaS1DdHJsXCIpXG5cbnRwIDwtIGMoXCIwbWluXCIsICBcIjMwbWluXCIsIFwiNjBtaW5cIiwgXCI5MG1pblwiLCBcIjEyMG1pblwiLCBcIjE1MG1pblwiLCAgXCIxODBtaW5cIiwgXCIyMTBtaW5cIiwgXCIyNDBtaW5cIikgIyBvcmRlcmVkIHRpbWUgcG9pbnRzXG5cbiMgaW1wb3J0IGFuZCBwcm9jZXNzIHRoZSBkYXRhIHRvIHRoZSBmb3JtYXQgd2Ugd2FudFxuZGF0YS5vbC5waSA8LSBtYXBfZGZyKGZpbGVzLCB+cmVhZF9jc3YoLiwgbmEgPSBjKFwiXCIsIFwiTkFcIiwgXCJOL0FcIiksIGNvbF90eXBlcyA9IGNvbHMoKSksIC5pZCA9IFwiUmVwbGljYXRlXCIpICU+JSBcbiAgI2JpbmRfcm93cyguaWQgPSBcIlJlcGxpY2F0ZVwiKSAlPiUgXG4gIGZpbHRlcihgWCBQYXJhbWV0ZXJgID09IFwiQkwxLUhcIiwgaXMubmEoYFkgUGFyYW1ldGVyYCkpICU+JSBcbiAgc2VsZWN0KFJlcGxpY2F0ZSwgR3JvdXAsIFNhbXBsZSwgQ291bnQsIG1lZGlhbiA9IGBYIE1lZGlhbmAsIHBlYWsgPSBgWCBQZWFrYCxcbiAgICAgICAgIHNkID0gYFggU0RgLCBjdiA9IGBYICVDVmAsIHJDViA9IGBYICVyQ1ZgKSAlPiUgXG4gIHNlcGFyYXRlKEdyb3VwLCBpbnRvID0gYygnVGltZScsICdUcmVhdG1lbnQnKSwgc2VwID0gXCItXCIpICU+JSBcbiAgbXV0YXRlKFRpbWUgPSBvcmRlcmVkKFRpbWUsIGxldmVscyA9IHRwKSkgJT4lIFxuICBtdXRhdGUoU2FtcGxlID0gY2FzZV93aGVuKFNhbXBsZSA9PSBcIkNUQTEtR0ZQLXlIMjk4XCIgfiBcInlIMjk4LXd0XCIsXG4gICAgICAgICAgICBTYW1wbGUgPT0gXCJDVEExLUdGUC15SDI5OVwiIH4gXCJ5SDI5OS13dFwiLFxuICAgICAgICAgICAgU2FtcGxlID09IFwieUgzNDMtd3RcIiB+IFwieUgzNDMtcmVzY3VlXCIsXG4gICAgICAgICAgICBTYW1wbGUgPT0gXCJ5SDM0NC13dFwiIH4gXCJ5SDM0NC1yZXNjdWVcIixcbiAgICAgICAgICAgIFRSVUUgfiBTYW1wbGUpKSAlPiUgXG4gIG11dGF0ZShSZXBsaWNhdGUgPSBnc3ViKFwiXFxcXC0uKlwiLFwiXCIsIFJlcGxpY2F0ZSkpICU+JSAjIFxuICBzZXBhcmF0ZShTYW1wbGUsIGludG8gPSBjKFwiU3RyYWluXCIsIFwiZ2Vub3R5cGVcIiksIHNlcCA9IFwiLVwiKSAlPiUgXG4gIGFycmFuZ2UoVGltZSlcbiMgVG8gcmVwbGFjZSB0aGUgdmFsdWU6IGlmZWxzZSgpIGZvciBhIHNpbmdsZSB0ZXN0LCBjYXNlX3doZW4oKSBmb3IgbXVsdGlwbGUgdGVzdFxuIyBcXFxcLTogZXNjYXBlIGNoYXJhY3RlciBcIlxcXFxcIiB1c2VkIHRvIGVzY2FwZSB0aGUgc3BlY2lhbCBtZWFuaW5nIG9mIC0sIGluc3RlYWQgdGFrZSAtIGFzIGEgY29tbW9uIHJlZ2V4IHBhdHRlcm4uIE9yIHdlIGNhbiBzcGVjaWZ5IHRoZSAtIGFzIGEgcmVnZXggcGF0dGVybiB3aXRoaW4gYSBzcXVhcmUgYnJhY2tldCBjbGFzcyBbLV1cbiMuKjogVGhpcyBwYXJ0IG1hdGNoZXMgYW55IHNlcXVlbmNlIG9mIGNoYXJhY3RlcnMgKC4qIGlzIGEgY29tbW9uIHJlZ2V4IHBhdHRlcm4gZm9yIFwiYW55IGNoYXJhY3RlciwgemVybyBvciBtb3JlIHRpbWVzXCIpLiBtZXRhY2hhcmFjdGVyXG5gYGAifQ== -->

```r
files <- dir("input/OL_0Pi", pattern = "d01*") # get the file names of the merged
files <- file.path("input//OL_0Pi", files)         # this appends the directory to the file names
names(files) <- c("Rep1-0Pi-Ctrl","Rep2-0Pi-Ctrl", "Rep3-0Pi-Ctrl")

tp <- c("0min",  "30min", "60min", "90min", "120min", "150min",  "180min", "210min", "240min") # ordered time points

# import and process the data to the format we want
data.ol.pi <- map_dfr(files, ~read_csv(., na = c("", "NA", "N/A"), col_types = cols()), .id = "Replicate") %>% 
  #bind_rows(.id = "Replicate") %>% 
  filter(`X Parameter` == "BL1-H", is.na(`Y Parameter`)) %>% 
  select(Replicate, Group, Sample, Count, median = `X Median`, peak = `X Peak`,
         sd = `X SD`, cv = `X %CV`, rCV = `X %rCV`) %>% 
  separate(Group, into = c('Time', 'Treatment'), sep = "-") %>% 
  mutate(Time = ordered(Time, levels = tp)) %>% 
  mutate(Sample = case_when(Sample == "CTA1-GFP-yH298" ~ "yH298-wt",
            Sample == "CTA1-GFP-yH299" ~ "yH299-wt",
            Sample == "yH343-wt" ~ "yH343-rescue",
            Sample == "yH344-wt" ~ "yH344-rescue",
            TRUE ~ Sample)) %>% 
  mutate(Replicate = gsub("\\-.*","", Replicate)) %>% # 
  separate(Sample, into = c("Strain", "genotype"), sep = "-") %>% 
  arrange(Time)
# To replace the value: ifelse() for a single test, case_when() for multiple test
# \\-: escape character "\\" used to escape the special meaning of -, instead take - as a common regex pattern. Or we can specify the - as a regex pattern within a square bracket class [-]
#.*: This part matches any sequence of characters (.* is a common regex pattern for "any character, zero or more times"). metacharacter
```

<!-- rnb-source-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->



#### under -Pi
Plot the internal removal variants data(OL)

<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuIyByZWNvZGUgdGhlIGdlbm90eXBlXG5sZXZlbHMgPC0gYyhgV1RgID0gXCJ3dFwiLCBgUENgPSBcInJlc2N1ZVwiLGBJUl8yLjRgID0gXCI0T0xcIiwgYElSXzQuNmAgPSBcIjZPTFwiLCBgSVJfNi44YCA9IFwiOE9MXCIsIGBJUl84LjEwYCA9IFwiMTBPTFwiKVxubGV2ZWxzLm5vcmVzY3VlIDwtIGMoYFdUYCA9IFwid3RcIixgSVJfMi40YCA9IFwiNE9MXCIsIGBJUl80LjZgID0gXCI2T0xcIiwgYElSXzYuOGAgPSBcIjhPTFwiLCBgSVJfOC4xMGAgPSBcIjEwT0xcIilcbkcubGV2ZWxzIDwtIGMoXCJXVFwiLCBcIlBDXCIsIFwiSVJfOC4xMFwiLCBcIklSXzYuOFwiLCBcIklSXzQuNlwiLCBcIklSXzIuNFwiKVxuXG5waS5vbC5kYXQgPC0gZGF0YS5vbC5waSAlPiUgXG4gIGZpbHRlcihnZW5vdHlwZSAlaW4lIGMoXCJ3dFwiLCBcIjRPTFwiLCBcIjZPTFwiLCBcIjhPTFwiLCBcIjEwT0xcIixcInJlc2N1ZVwiKSkgJT4lICBcbiAgc2VsZWN0KFRpbWUsIHJlcGxpY2F0ZSA9IFJlcGxpY2F0ZSwgZ2Vub3R5cGUsIFN0cmFpbiwgbWVkaWFuKSAlPiVcbiAgbXV0YXRlKEdlbm90eXBlID0gZmN0X3JlY29kZShnZW5vdHlwZSwgISEhbGV2ZWxzKSkgJT4lIFxuICBtdXRhdGUobmV3X21lZGlhbiA9bWVkaWFuLzEwMDApICU+JSBcbiAgbXV0YXRlKG5ld190aW1lID0gYXMubnVtZXJpYyhnc3ViKFwibWluXCIsXCJcIixUaW1lKSkpJT4lIFxuICBhcnJhbmdlKG5ld190aW1lLCBnZW5vdHlwZSwgcmVwbGljYXRlKSU+JSBcbiAgbXV0YXRlKGdlbm90eXBlID0gZmFjdG9yKGdlbm90eXBlLCBsZXZlbHMgPSBsZXZlbHMpKSAlPiUgXG4gIG11dGF0ZShHZW5vdHlwZSA9IGZhY3RvcihHZW5vdHlwZSwgbGV2ZWxzID0gRy5sZXZlbHMpKVxuXG5waS5vbC5kYXQgJT4lXG4gIGZpbHRlcighaXMubmEobmV3X21lZGlhbiksIGdlbm90eXBlICE9IFwicmVzY3VlXCIpICU+JSBcbiAgZ2dwbG90KGFlcyh4ID0gbmV3X3RpbWUsIHkgPSBuZXdfbWVkaWFuLCBjb2xvciA9IEdlbm90eXBlKSkgKyBwLnRpbWVjb3Vyc2UgK1xuICBzY2FsZV9jb2xvcl92aXJpZGlzX2QobGltaXRzID0gbmFtZXMobGV2ZWxzLm5vcmVzY3VlKSkgICtcbiAgbGFicyh4ID0gXCJQaG9zcGhhdGUgc3RhcnZhdGlvbiwgVGltZSAobWluKVwiKVxuYGBgIn0= -->

```r
# recode the genotype
levels <- c(`WT` = "wt", `PC`= "rescue",`IR_2.4` = "4OL", `IR_4.6` = "6OL", `IR_6.8` = "8OL", `IR_8.10` = "10OL")
levels.norescue <- c(`WT` = "wt",`IR_2.4` = "4OL", `IR_4.6` = "6OL", `IR_6.8` = "8OL", `IR_8.10` = "10OL")
G.levels <- c("WT", "PC", "IR_8.10", "IR_6.8", "IR_4.6", "IR_2.4")

pi.ol.dat <- data.ol.pi %>% 
  filter(genotype %in% c("wt", "4OL", "6OL", "8OL", "10OL","rescue")) %>%  
  select(Time, replicate = Replicate, genotype, Strain, median) %>%
  mutate(Genotype = fct_recode(genotype, !!!levels)) %>% 
  mutate(new_median =median/1000) %>% 
  mutate(new_time = as.numeric(gsub("min","",Time)))%>% 
  arrange(new_time, genotype, replicate)%>% 
  mutate(genotype = factor(genotype, levels = levels)) %>% 
  mutate(Genotype = factor(Genotype, levels = G.levels))

pi.ol.dat %>%
  filter(!is.na(new_median), genotype != "rescue") %>% 
  ggplot(aes(x = new_time, y = new_median, color = Genotype)) + p.timecourse +
  scale_color_viridis_d(limits = names(levels.norescue))  +
  labs(x = "Phosphate starvation, Time (min)")
```

<!-- rnb-source-end -->

<!-- rnb-plot-begin eyJoZWlnaHQiOjQzMi42MzI5LCJ3aWR0aCI6NzAwLCJzaXplX2JlaGF2aW9yIjowLCJjb25kaXRpb25zIjpbXX0= -->

<img src="data:image/png;base64,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" />

<!-- rnb-plot-end -->

<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuI2dnc2F2ZShcIm91dHB1dC9PTF8wUGlfbm9yZXNjdWUucG5nXCIsIHdpZHRoID0gNiwgaGVpZ2h0ID0gOClcbmBgYCJ9 -->

```r
#ggsave("output/OL_0Pi_norescue.png", width = 6, height = 8)
```

<!-- rnb-source-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->

#### 2mM H2O2 Data
Import 2mM H2O2 OL data and get the replicate, time and genotype info

<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuZmlsZXMgPC0gZGlyKFwiaW5wdXQvT0xfMm1NSDJPMlwiLCBwYXR0ZXJuID0gXCJkKlwiKSAjIGdldCB0aGUgZmlsZSBuYW1lcyBvZiB0aGUgbWVyZ2VkXG5maWxlcyA8LSBmaWxlLnBhdGgoXCJpbnB1dC8vT0xfMm1NSDJPMlwiLCBmaWxlcykgICAgICAjIHRoaXMgYXBwZW5kcyB0aGUgZGlyZWN0b3J5IHRvIHRoZSBmaWxlIG5hbWVzXG5uYW1lcyhmaWxlcykgPC0gYyhcIlJlcDEtMm1NSDJPMlwiLFwiUmVwMi0ybU1IMk8yXCIsIFwiUmVwMy0ybU1IMk8yXCIsIFwiUmVwNC0ybU1IMk8yXCIpXG5cbnRwIDwtIGMoXCIwbWluXCIsICBcIjMwbWluXCIsIFwiNjBtaW5cIiwgXCI5MG1pblwiLCBcIjEyMG1pblwiLCBcIjE1MG1pblwiLCAgXCIxODBtaW5cIiwgXCIyMTBtaW5cIiwgXCIyNDBtaW5cIikgIyBvcmRlcmVkIHRpbWUgcG9pbnRzXG5cbiMgaW1wb3J0IGFuZCBwcm9jZXNzIHRoZSBkYXRhIHRvIHRoZSBmb3JtYXQgd2Ugd2FudFxuZGF0YS5vbC5veGkgPC0gbWFwX2RmcihmaWxlcywgfnJlYWRfY3N2KC4sIG5hID0gYyhcIlwiLCBcIk5BXCIsIFwiTi9BXCIpLCBjb2xfdHlwZXMgPSBjb2xzKCkpLCAuaWQgPSBcIlJlcGxpY2F0ZVwiKSAlPiUgXG4gICNiaW5kX3Jvd3MoLmlkID0gXCJSZXBsaWNhdGVcIikgJT4lIFxuICBmaWx0ZXIoYFggUGFyYW1ldGVyYCA9PSBcIkJMMS1IXCIsIGlzLm5hKGBZIFBhcmFtZXRlcmApKSAlPiUgXG4gIHNlbGVjdChSZXBsaWNhdGUsIEdyb3VwLCBTYW1wbGUsIENvdW50LCBtZWRpYW4gPSBgWCBNZWRpYW5gLCBwZWFrID0gYFggUGVha2AsXG4gICAgICAgICBzZCA9IGBYIFNEYCwgY3YgPSBgWCAlQ1ZgLCByQ1YgPSBgWCAlckNWYCkgJT4lIFxuICBzZXBhcmF0ZShHcm91cCwgaW50byA9IGMoJ1RpbWUnLCAnVHJlYXRtZW50JyksIHNlcCA9IFwiLVwiKSAlPiUgXG4gIG11dGF0ZShUaW1lID0gb3JkZXJlZChUaW1lLCBsZXZlbHMgPSB0cCkpICU+JSBcbiAgbXV0YXRlKFNhbXBsZSA9IGNhc2Vfd2hlbihTYW1wbGUgPT0gXCJDVEExLUdGUC15SDI5OFwiIH4gXCJ5SDI5OC13dFwiLFxuICAgICAgICAgICAgU2FtcGxlID09IFwiQ1RBMS1HRlAteUgyOTlcIiB+IFwieUgyOTktd3RcIixcbiAgICAgICAgICAgIFNhbXBsZSA9PSBcInlIMzQzLXd0XCIgfiBcInlIMzQzLXJlc2N1ZVwiLFxuICAgICAgICAgICAgU2FtcGxlID09IFwieUgzNDQtd3RcIiB+IFwieUgzNDQtcmVzY3VlXCIsXG4gICAgICAgICAgICBUUlVFIH4gU2FtcGxlKSkgJT4lIFxuICBtdXRhdGUoUmVwbGljYXRlID0gZ3N1YihcIlxcXFwtLipcIixcIlwiLCBSZXBsaWNhdGUpKSAlPiUgIyBcbiAgc2VwYXJhdGUoU2FtcGxlLCBpbnRvID0gYyhcIlN0cmFpblwiLCBcImdlbm90eXBlXCIpLCBzZXAgPSBcIi1cIikgJT4lIFxuICBhcnJhbmdlKFRpbWUpXG5gYGAifQ== -->

```r
files <- dir("input/OL_2mMH2O2", pattern = "d*") # get the file names of the merged
files <- file.path("input//OL_2mMH2O2", files)      # this appends the directory to the file names
names(files) <- c("Rep1-2mMH2O2","Rep2-2mMH2O2", "Rep3-2mMH2O2", "Rep4-2mMH2O2")

tp <- c("0min",  "30min", "60min", "90min", "120min", "150min",  "180min", "210min", "240min") # ordered time points

# import and process the data to the format we want
data.ol.oxi <- map_dfr(files, ~read_csv(., na = c("", "NA", "N/A"), col_types = cols()), .id = "Replicate") %>% 
  #bind_rows(.id = "Replicate") %>% 
  filter(`X Parameter` == "BL1-H", is.na(`Y Parameter`)) %>% 
  select(Replicate, Group, Sample, Count, median = `X Median`, peak = `X Peak`,
         sd = `X SD`, cv = `X %CV`, rCV = `X %rCV`) %>% 
  separate(Group, into = c('Time', 'Treatment'), sep = "-") %>% 
  mutate(Time = ordered(Time, levels = tp)) %>% 
  mutate(Sample = case_when(Sample == "CTA1-GFP-yH298" ~ "yH298-wt",
            Sample == "CTA1-GFP-yH299" ~ "yH299-wt",
            Sample == "yH343-wt" ~ "yH343-rescue",
            Sample == "yH344-wt" ~ "yH344-rescue",
            TRUE ~ Sample)) %>% 
  mutate(Replicate = gsub("\\-.*","", Replicate)) %>% # 
  separate(Sample, into = c("Strain", "genotype"), sep = "-") %>% 
  arrange(Time)
```

<!-- rnb-source-end -->

<!-- rnb-output-begin eyJkYXRhIjoiV2FybmluZzogRXhwZWN0ZWQgMiBwaWVjZXMuIEFkZGl0aW9uYWwgcGllY2VzIGRpc2NhcmRlZCBpbiA1NDAgcm93cyBbMSwgMiwgMywgNCwgNSwgNiwgNywgOCwgOSwgMTAsIDExLCAxMiwgMTMsIDE0LCAxNSwgMTYsIDE3LCAxOCwgMTksIDIwLCAuLi5dLlxuIn0= -->

```
Warning: Expected 2 pieces. Additional pieces discarded in 540 rows [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20, ...].
```



<!-- rnb-output-end -->

<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuIyBUbyByZXBsYWNlIHRoZSB2YWx1ZTogaWZlbHNlKCkgZm9yIGEgc2luZ2xlIHRlc3QsIGNhc2Vfd2hlbigpIGZvciBtdWx0aXBsZSB0ZXN0XG4jIFxcXFwtOiBlc2NhcGUgY2hhcmFjdGVyIFwiXFxcXFwiIHVzZWQgdG8gZXNjYXBlIHRoZSBzcGVjaWFsIG1lYW5pbmcgb2YgLSwgaW5zdGVhZCB0YWtlIC0gYXMgYSBjb21tb24gcmVnZXggcGF0dGVybi4gT3Igd2UgY2FuIHNwZWNpZnkgdGhlIC0gYXMgYSByZWdleCBwYXR0ZXJuIHdpdGhpbiBhIHNxdWFyZSBicmFja2V0IGNsYXNzIFstXVxuIy4qOiBUaGlzIHBhcnQgbWF0Y2hlcyBhbnkgc2VxdWVuY2Ugb2YgY2hhcmFjdGVycyAoLiogaXMgYSBjb21tb24gcmVnZXggcGF0dGVybiBmb3IgXCJhbnkgY2hhcmFjdGVyLCB6ZXJvIG9yIG1vcmUgdGltZXNcIikuIG1ldGFjaGFyYWN0ZXJcbmBgYCJ9 -->

```r
# To replace the value: ifelse() for a single test, case_when() for multiple test
# \\-: escape character "\\" used to escape the special meaning of -, instead take - as a common regex pattern. Or we can specify the - as a regex pattern within a square bracket class [-]
#.*: This part matches any sequence of characters (.* is a common regex pattern for "any character, zero or more times"). metacharacter
```

<!-- rnb-source-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->



#### under 2mM H2O2
Plot the internal removal variants data(OL)

<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuXG5veGkub2wuZGF0IDwtIGRhdGEub2wub3hpICU+JSBcbiAgZmlsdGVyKGdlbm90eXBlICVpbiUgYyhcInd0XCIsIFwiNE9MXCIsIFwiNk9MXCIsIFwiOE9MXCIsIFwiMTBPTFwiLFwicmVzY3VlXCIpKSAlPiUgIFxuICBzZWxlY3QoVGltZSwgcmVwbGljYXRlID0gUmVwbGljYXRlLCBnZW5vdHlwZSwgbWVkaWFuLCBTdHJhaW4pICU+JVxuICBtdXRhdGUoR2Vub3R5cGUgPSBmY3RfcmVjb2RlKGdlbm90eXBlLCAhISFsZXZlbHMpKSAlPiUgXG4gIG11dGF0ZShuZXdfbWVkaWFuID1tZWRpYW4vMTAwMCkgJT4lIFxuICBtdXRhdGUobmV3X3RpbWUgPSBhcy5udW1lcmljKGdzdWIoXCJtaW5cIixcIlwiLFRpbWUpKSklPiUgXG4gIGFycmFuZ2UobmV3X3RpbWUsIGdlbm90eXBlLCByZXBsaWNhdGUpJT4lIFxuICBtdXRhdGUoZ2Vub3R5cGUgPSBmYWN0b3IoZ2Vub3R5cGUsIGxldmVscyA9IGxldmVscykpJT4lIFxuICBtdXRhdGUoR2Vub3R5cGUgPSBmYWN0b3IoR2Vub3R5cGUsIGxldmVscyA9IEcubGV2ZWxzKSlcblxuXG5veGkub2wuZGF0ICU+JVxuICBmaWx0ZXIoIWlzLm5hKG5ld19tZWRpYW4pLCBnZW5vdHlwZSAhPSBcInJlc2N1ZVwiKSAlPiUgXG4gIGdncGxvdChhZXMoeCA9IG5ld190aW1lLCB5ID0gbmV3X21lZGlhbiwgY29sb3IgPSBHZW5vdHlwZSkpICsgcC50aW1lY291cnNlICtcbiAgc2NhbGVfY29sb3JfdmlyaWRpc19kKGxpbWl0cyA9IG5hbWVzKGxldmVscy5ub3Jlc2N1ZSkpICtcbiAgeGxhYihcIjJtTSBIMk8yLCB0aW1lIChtaW4pXCIpXG5gYGAifQ== -->

```r

oxi.ol.dat <- data.ol.oxi %>% 
  filter(genotype %in% c("wt", "4OL", "6OL", "8OL", "10OL","rescue")) %>%  
  select(Time, replicate = Replicate, genotype, median, Strain) %>%
  mutate(Genotype = fct_recode(genotype, !!!levels)) %>% 
  mutate(new_median =median/1000) %>% 
  mutate(new_time = as.numeric(gsub("min","",Time)))%>% 
  arrange(new_time, genotype, replicate)%>% 
  mutate(genotype = factor(genotype, levels = levels))%>% 
  mutate(Genotype = factor(Genotype, levels = G.levels))


oxi.ol.dat %>%
  filter(!is.na(new_median), genotype != "rescue") %>% 
  ggplot(aes(x = new_time, y = new_median, color = Genotype)) + p.timecourse +
  scale_color_viridis_d(limits = names(levels.norescue)) +
  xlab("2mM H2O2, time (min)")
```

<!-- rnb-source-end -->

<!-- rnb-plot-begin eyJoZWlnaHQiOjQzMi42MzI5LCJ3aWR0aCI6NzAwLCJzaXplX2JlaGF2aW9yIjowLCJjb25kaXRpb25zIjpbXX0= -->

<img src="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAArwAAAGwCAMAAAB8TkaXAAABHVBMVEUAAAAAADoAAGYAOjoAOmYAOpAAZpAAZrYhkIw6AAA6ADo6AGY6OgA6Ojo6OmY6OpA6ZmY6ZpA6ZrY6kJA6kLY6kNs7UotEAVRdyGNmAABmADpmAGZmOgBmOjpmZgBmZjpmZmZmZpBmkGZmkJBmkLZmkNtmtrZmtttmtv+QOgCQOjqQZgCQZjqQZmaQZpCQZraQkDqQkGaQkLaQtpCQtraQttuQ29uQ2/+2ZgC2Zjq2ZpC2kDq2kGa2kJC2tma2tpC2tra2ttu225C227a229u22/+2/7a2/9u2///bkDrbkGbbkJDbtmbbtpDbtrbbttvb25Db27bb29vb2//b/7bb/9vb///95yX/tmb/25D/27b/29v//7b//9v///9gsz75AAAACXBIWXMAAA7DAAAOwwHHb6hkAAAgAElEQVR4nO2dDXsbx3HHD5RYArGlWopFginV2I1di4ncNGlcQbVbO60YC66o2nJCghRx3/9j9Pbl7vb9Zt/uBZj/84gEcdjF4e6nwezuzGxRolATVTH0CaBQoUJ4UZMVwouarBBe1GSF8KImK4QXNVkhvKjJCuFFTVax8CL8qMGE8KImK4QXNVkhvKjJCuFFTVYIL2qyQnhRkxXCi5qsEF7UZIXwoiYrhBc1WSG8qMkKAN/25aKYfXZFH37TPIS3R6HyqBu+7XlBdEQer9qH4PYoVCZ1w7cpDi/K29PZC/LwfvXwrHjm0x6FyqRu+NYE24rbJ5XhpQ9vFoLpRXhRg8kH3u35IXF3+S9o+93SnGno00ARdcN3syBuw1mF8N0pM7mrg9e0KVXe0xujkNyxCADfm0XF6KzycxV4oe13TQjvWASYbXhOLezjK4SXCeEdi7rhWxUfX5Xbl5XPi/BSIbxjUSd8nNjt+cFrHLBRJYAXh31J5AMvTpVRJWIO0Y1WJ3zbc+LuVm7DES5SMCG8YxFkqowO2KjRxeXhEuEdjwDw3ZLphkcX5OH2awzMQXhHIwyJ9BbCOxYhvN5CeMcihNdbCO9Y1AO8Pz2vhnz3JE/ZrveR59ODEN6xKDu825csgIdNV3Tphw9ed79oYCG8Y1F2eFfFvS8qo/v+ZXEA4HIFedHAQnjHotzw3izucxzX4tqGTQgvCq7c8LbI3v3Lv5ds0pjOFG/PD388K2afl/TJBZ1JpulyRzRpgy5Lrw6+r5yOhxel2HBwIbxjUWZ4pSCeslmuO2ryOgmo/EkS+UOOsWiKTUX96uAfa2+5bTi0UgXUILzRygxvHUVZq46vfEbgPbqqDPMRebKJnqBuQ/NjVcy+qg80DYdVungwhDda/cB7d0rM5uEVD0jbnh+xMLXqwOEV+VfWcWvkSWJ0aUMWxUYOCA2HlQneMKAR3mj14za08PJ5s8MrdoT8vFk8oa8lmZ4rRvQRBbgevlUHhIaRJxyn+VwkdW4SuKtsJ7k3yj1gWzXTu4xTzmAd2W6Et1wfvG79BxnegWcjBEQ1XD0BRnijlX+qrLaVIqdlbZPJT81tqBr9M3U3RLfhian33gUwslCAEd5o9bBIMfvs54rAyzPqK8w+vyL5yEcCvNKAjeN6b/GMtr1/wQ4IDYcVzLpC3AiEN1r5Yxvq5WECohDZLsArhLuv2WzYmrkHq9mHtasghsQPKbhf0IUvwhutHgJz6BLE7NEr/gePbBfgZQsQjyv7XN6d0SEZn1xYHXxfHXl0JTUcWL7zClZ+Ed5ojTMkcsPmc8e3WBw0J6Y3Oqk0PzlJd177qVHCe8vX5UYHL6UwwGSazC9a3miNEF4yKczmFkYGLwGQmUx/m6m7vwhvtEYIL0m2Z4/GBW8NXzB18hAO4Y3WCOEdp1q7GUNd0FocyiKEFyZxJS1Nb4hvtBBekETQkoSUIb4JhPACJFMGBO4EIOQ3Sghvt/ymCSDQKvxmPfsdFsLbJY0uG2ue1EoA5/8YuyiEt0Ow1YVwcJHfcCG8bulf6idzZYnCgqOrV+bszj1aoAxCeJ3S2D1RV9j8qBV6oeyqzZOe/M4L4XXJYHdleEPJk7oJxnffp9sQXrsMYJxw6k7qPwJNpmrAw/n1fOOdEsJrlcmoCfBGftlrrnPY/wWEV9T27ZeffPLpn6FJunHw3tBsn3LNosjWLHFizMVFGnjj/dSOSYuIXvZGCnxvGnzufxXS3i7j/bg7fUZ/8gJPdZmnMcjiS2rwhr+B8VnfnhHeWpdnxf0/vvq5LN//9M2HMHyB8FruB4N3zeJ31zxzeOiiOFS2cZAMb9Q7WJ736x3hZdq+lArZvX+5eNztPMTC+4T8+DtSCIcZ3nIzeI4lkWMMnwZdJ3Ye74DwMt39/mf52PY/umPBO+E9USUepMCuD74n8K55hZExBKC75p/SoNuBHRhfhDdneye82/MnJaknsjqqDa9aVjKZfOZEu9lNcUIdxwH4ngTmJO2K+pkqsxkSUjiPloM8vOIWlzOcR1Az1eUz9FMlct5NL1pek7ZvgZNlcT5vBS8t5LQ6/CuHNut4DXinrWzyT7FcLiNP5OQElPoOwBfh1XV3CnQ94+Ct/AWaZLk+/C/+flnHa5FOQ81ufycz78QX4dWV2vJa5nnL1T1aQW89+5B7C6ucNUxh1Rvd7JZlj/C2xteGL8I7XPsVK7i7rkuX5q0eDSwxZj7QMNQrvF3GF+Edrv2qENeHM4/XIHe6m92e4S3nTnwRXkHv33H9bHx5Z/tRq/tOA9jtG143vghvK1Z/36ME+W7B61gUbtnpHV6BXg1fhLfV9u13lb799eyz1AO2MajrTgPYJbMN/SxSqGdmnitHeHWtZ8Dp1l2CF2J3l0yl+If0HEjk5XOvFnMLvgivLr5PRHD7ccp9p93s8j+WnUpzMsbTM+CL8OpKvUgxDjnvdAC78gs9IfbGTko3Du5ll2SGb/s1dMOznYEXxG4JQBMKcGCNagVfhLdVO9uwZz4vjF0IvMpLQ07GLg1fhLfV9stPqD59FdZ+3LLfaU+7C3VsXa8Ow46FdTb46mmc+6TeVtiOj48Nz5IVtXr/97+XvOw3i2L2ufB3ioVjF7zGp63+Lvw9rQ1CbaaMr33heA/UE7zHTNrzJAKS7265/Z3oZm+KL8pbca14VcQvHFt5gbLLf/u+rxHg4C98HlOP8PYVVWaDl0RA8n2ryo0wwcHsrJAStAZ74Q7ZeLFnCrfLai18QStsOr8R3qqKb3hP01b2qbJjVdJRgufaEMq7/U/yuMV5M/tDgkBfCy9+7IYvD8sAxwy10HWgym55nfCyrYe5u6CF8rb5bJV3sU4Q6GuF1/SssqzWHoiJbeD8xhcZ04tMRnQ2VfXj85rNLqswwkdi2681v2BdG9tqWJck0NdMiye70YE5QeM+TfWmFvvM77ADNjZeY5MND5V9hbcv6/gKAm6SQF8jpV3sapAliCpLAG+L7/7yq8P37jsaWPZp0uVhC7zNeE3PeN+eN04u8SdufpEgt82EqWuigTwwLAPHn0ha4yu7v/FnNxmp8NV2MHk8r3Getx2vqSXK7s4adutVvyzzvB3smvBKC28EwNJ+WPuIrwrfqni4mH30tICO7ePcjlU7XltL73h3enChvTJaJniNL3SxmxTe+mFQL8pmbvtHrxbbMHuxqjBaQ5cEouAVxmuK6V0p/3nSJGbqpDodXgtVKTIpJJMbzO9cwXffZn41eA9erwsyiuojqkxYX5N3yeaewsHrugYJKycZK43UEHbTwxuM73y+3/ga4N1UVnc/4nld7NppSpPDps1hBPHLqZVmjfcHX83nnb24WRxV9nAP4A1hN8UcF+/J3LVnL/VHMOK76/yq8G2Kg+/Pi1+eC2P77TeLonh0VT+UivimhNc7lthbMqzmJa6G3Uzn0MjoTnvz236EPcRXg+/NB69vzorifmN4ecQi9YFX2pzVdC2vK6KhB3Yt3ocvvuJnkFac9wFfM3zvhZIj6+L+RXl7TqYfNvThmWgZpwSvhOvQ7NpdZy96tS8TbeS2w/SKldH/qE4wvL0ihrddRGATWMQnNrUfuZRgGCe7fZxPRxocsBfNjd8n30Hck+Jc3kLl8oy4Cs1UVrOGKy3lThVe52Ctl/NxvQvcdzDM/u0PvhJ8Pyxmv2HJa9ufni/YyGxTPLusfOBHF+06Ap+RZYOrns83WPKEqHOw1s8Jud8Giq9xxVv8cLuMrwzf9iUJbbhHNmOb8a2ANsWDOtZBgdfQ3iEzLvYctlJaVvthUdyPi8yR4HU6vFFvA1fX+wDoPbHsSWHE1/sExy8NvrdfPn3w4GGbPbwpio+vyvfPi6MYeG3R19YcNvo+zRr1+uBi+3XcNkEivGNgF7DWATG+thBlD3xt92b86oRvU/Bdeg5eZ4DXlsNG1Kat0QSh2KDIkbELWagD+A6OtDzxUIf1nSK5JQC+OrqgIjZowDZXJR215bCVUtraKklUTv32LnZ7/HIF/TfpxNdZigLm+tqcj/GrEz5ubumMWchUmRNeRw6bkLZ2d/rorJh90f1huk+ltLJb9u0YAm18B70Om2k2vsbPuKuWt/I8q6HbLV0vDl6kMJtdVw6bmLa2KQ4uynWi1PdRsOsVIeEIEaKFUh0VpaD47iy8d2dtZkXw8rDF57XmsElpazROPVHFnFGw6ykX6G7s1Gtuw3dn4WXzZ2zibPt1YGCOBV5rDpuUtsb8iUjH94S6dk52xwqvC98u7Myer/pRdxfeNO2N2Nhy2OS0NQpvEss7UXZLu+/QiR3I+E4f3jYksbcNVaw5bPVBKjqHlmJfV+ts5ujZLW34ArAD4Dt9eOvyprzIaQ9pQPYctlI0tXenH1/dqod9taR1aszfvVNg1+I7QLDTPTYV3+nD2397aw4bEU1bY/b29kzxtIM0abtLZcAXhl0Xvgjv2DVdh7eVRi8UO93dF/HdHXjf/uHTv/1fRPuRqrp5xnu0nBC7pYYvHDsXvrsC75tFNVj7C3Qnq+nksM0t8E6MXdV38MBO8x3aibMdgXdT3P+f04PX4DrkU7G8LKpBf34Ydq+ZAluL9UosQ1CzrJ7vtP77NlI3VDmfvSA1G/opOtKfeFiD9vxyuDsXii4Rp7dreVjXbuFrKDpS/wtpP1KxW6abqQHZjYKX4+sPr8PznSC+ewEvvWGGO70c0uGNg7epse5dqGSHjK9eJfIZK/kEXBOYArzc7mrwDspuLLwcX394TStuli3lxy69Pu/so8Xsnxb9lDh15bCJaWu3Z9XhC705SA27yp0elt14eH2245Ql4XsiwTspfDX4bmgEJDjbEQyv+Rrbc9jEtLWbxcdXW3UFDip+ozR4l0M6vGUKeMN3BxDpbeCdXqKxAb7tT69+1p+FtzfJdpWtOWxS2tqaFZAImv6tb5MK73Jgw5sI3nk0vi28k6vz0NPysA1eaw6bFL1L/whLwGxNjOzzhrIbN0Mr9RTfBY+SDnYd2KU5EXPYJoWvNtsgV83xba9rqUo8aM1hk9PWNrOvylttyxWIhK9HCd4Yu5uCXPq/IEU37PNE4XsiJ2BOCF91kYJkTTyCbvmut9flhNeawyanrb0nQ7rHceyW4jzvMsbhTWJ2Uxlw4RNF4CvuHT+hoZsO30/PSbkcqNcLcxts42JrDpuUtnZ3enhRvglwedUZTcGDiLg9CZC7Tg5vHL62dYvo08srI3ykONlh0kUKi8/rzGFrHF/mFPvnsGmLSfPmZGLuTQxy1yZF9FfK89YB/JqTC6eBrxm+n36bOA3IAq91HzYpbY1hGwKv+kR9LlE3Jgg2I7UJGE6wsYWR3klU6DPAd0v8hkfAJYG4eV5rDpuUtkax9d8PSL8j9YRv3F3xo8wIqPx3DMDmnS28urBkdk+gQp8K33uyAcVD+IxDphw2KW1tU3wRMNlguB98pS0y7wdImNOsmp4NAtjAqS+9loIwRCPHV5sqK+594UNJrhw2nrbGjO/lh/6TDaa7MU/BLgTeTltqO+gNsHXLInAP81aGo6PGV4X39/DFNVP78ch0K+Yp2O2CF8if/RVeADu2ZQG1V4rJ6YfH7PruagKm0YzMG3ZzwevBnfNF4G5siMLxbcGdnPEdUQJmyhw2c6JwGnZ9XQFbP93vA+jNDqgvvfVDwyvGiu+IEjATyngLlinY7XBWfXoCvpf7NV3bsgBORPQYpuX67mQCppXd+HvgmCbw7Qn8dtajtnAn6TjgXURgp+T67mQCpoXdOuY6omfDJELgBK3fjJvzbBytIfieKJXR3cZ3TPjuYg6b6dpTszuPvvoqvKHklh5rHc736HaKIcZXXUYPwHcItHcQXiu7CS6vDG8Eun4Ldfb3AfQCwFdbRw+zvn1b5d1LwLSwW92NFLZBYDeC3GMm7/c1PA9o2+07GNZzjPienLitL+BkUqq3BEzzjbYnYKo5lxu2E9HLonjk9sbN7KaKk2rgjTG6VD7otu+sPQtq24WvcVLcP9xsaHgzJWDahhbWBEw155K9iERObt3hZQZ7wW5cKqeMfYxYdP3hLY3/YaAn4abXXKvMG9/B4c2TgGmD15qAqeRc3izoi2j4pDOZrYvd2OvLvu/j0Q2C12B+PaIgHPhaC+354TsCeNO2v1YlHXUnYNaYbr9ZfEgOsv2BXGnE2e1upeNoj4FelOOwPuSL6HMiDt/BUSXSZ9p3QHjz7EnhhNe+iaCUc/nDw1fUEm/4JoZWePtgNx5dKr/xmn4G16X9+8wmK77OEqfwYN8B4c24J4XZ7Lo2EVRzLqklZjZ6Yx9MutlNcnGToes53aCdhOW7zC0Lve76vOBY9Z1zG5gsl9magKnmXG7PnzRpQWvrl4J+iSV2E1xc+n3vZu5YlvNFsafiT68Z367i0kB89wteawKmmnNJXQVKsCOZrYvd+IvL2LVQdwyQ+tLos/F3Yky+Qxe8QNd3R+G1DC3sCZhKziWdiWDwWpPZOtmNvbgNugp0TlMLgjn8fEKN71L6E1Llt8P42pMx8mnYYHRrAqaac7luU+HXtpChTnYj4RXYFajzAzEtvs6JHJdU4wtirtt36BfdgeG1J2AqOZf8RcTLeGMbrmkXVmM3Cl4Gh8xcOH9p+BWYjcMXSF0XvnsFryMBk+dc8mmxegP4Nwvr2h+A3Rh4ORkCcFHktY3jAJZ49eJX8h3A1LlDHuY9O707k8MGYDcC3gaKZF/5QvOY3kxh8cCmQiS7h8kMitjJJB2+9++ogCvEY4FXvaD8tiSaymmJSDTWKtXl4dBO9UgdD34bfL2+7934+vQUKxW+u7M+d32X3zoiARPEbii8Eg1pyC0NsQ1B/y1MUZI+/i/j19NZNeE7hOnV43lnn31H9OcppQHB2A2EVwSB0ZWktK5rrhjei+VMvPGFvyOVTu/JAJ6DlkkBDeQ1tx9IDnaj4VXRDQsH02XtxotfO6CZ+VXxZQO2fuk1pAHFtB9GuuElP/ULGXJVFXe3DIxl1OXoxgNfF51gfIN2tlB9h5P+d8QyZA/HtB9EUHZD4JXZZQ/8ezEJECEB6KWDTQi+y2Zblih8Obx9ZmLqaUCHXvudjQJe+U/TJBmT9xVtb73AUi/wQs1vp2HtNr/N8nCs78DnefuzvnqVyMFmG0KlGF47u97wGtntC14YvgCvoAPf5bLd4ysS3/pRX/SqbsOXWeJ5c8rIrrkUpOflNKLbI7wlwHuAjchc+Irwhpamrh83z/aD7/RX2ODs+sFrMbtJ5nk9eul4JXTSzm5+lzwerN3kKxhfZfyWHd/JwysbXie7XvA29zrRmkS47Ph6ReNYX6uO1fyHbk2RSfHJHlxfKYeNVMqZmM9rZzcOXovLMJASreqZ8dUnGkLxNa9bhJwpTFIO26dXU/N5NYeX/LReM/h1HI3ZrZXoRMzm10CqL77OGg+eJwnWxN0GL3bh8I6O3TIjvtWfSzPR/vuyaM9mxXfa8JqcBsfVgl5DfivHhG6ZzHcw8Wvf2cKnX6P1zen6jqisv7882YXCO052Sx3f4KkPNfDMwqiX79DsbdEfvpMu6291Giyvh12/Nmci5tzySKM1SQ6RfXMAD3zn897xnXJZf9Xwkp/OiwS6emNmt9TwTZDAWTp3toDOPLTgusqbRZysQRMu6+/NLgjeht2oc8sqkd/Y02T8OuGE4XvCAnPoTXFF+0adraIJV0a3sRsF73WdIxx5cnnV5lzEnydkoQOAr+QyGHyHHPROF17p6oDYBcA7DXapQpKGLALwC6ZX/Et+QXp8gWX9eQ3d7TcLuiWwvX1vUpwG+rPr0nRetprduFPrTWnw5fO8sfiqY7UeBm6wsv68tnOFNpHI9VDw+ju8JQjeKbGbyPjy5eFOfjt9B5VW+8gt7EQ1gcr6k10jCLyb4v4F2SxCyO4dDF7xD9BgDXDZJspuHL/1nO91d9px19BNRdWxZBx6tpJAZf3Xsz9QYFe8uLNgegeCN8Dh7Ra5bxNiVy98FtTLtcRsFL766rB91tfWhU+9PnXA9vQhHahtz4UBW+XwinVIpXKkw8Ab4vB26prV0Yvpol+J0Ibje60a3HB+TczZXV/bG8CLSEjwvXv30+nBK1Iv53LRwktK4FF461p4YlWxgeAV/wA6vF2aHLsasYH86s5CKL5m7HzxDYNX2pSita6EVRO87HXgd0oom9MQ0ydjN+q0epdmboPwNXq6HaM3M70W7BzTZsaXu05WkgTf7XffLmZ/UgrmrAm3o7K8ORzeKbJbmoaXgfgan+wyv+pzVuwMjqyd3kB4WUC6/AwrQToueIXH+82ucYUtwPyaGXXja/AdHNh54BsMr6517UfMXoxkwCYbXvpzb9l1VTzz6MVKKBxfnoTseBOdXzO+MfBe/vrBg4++av4U4B3HVFkGh3d6Q7VGtrP2w9fh3TrNrzJ068JOw1d3fU943R2QVPjIesRsIY7XqDajWaRAdiXZT9vH/DoXhuH4AmwmwPiGW9414ZMAKsfzbkazPJze4Z2sy0DkOnE4vl3Z80DvAYRdJ77hAzZeaE+N560Dc74eOjAnvcM7aXa7QiKB/HaXfug0v+Q3DDuL69seB/VCZClxOtaQyPROw7TZ7Y7nBS0dQ+qWAPCFYmd2fZujwF6sxaVvFiOFV3iM7ELXhDtfFlt0h/sOcOxcxjfc5+XJa+vCtkdqR/u8Ej/xMoXTMOGhmp/c/ALh7cYXfkJW4+uxIZYez1s8/NO3Twtojele4UV2I+TCFwxvaed3qZeNckrxHU4ahU+VkYkGEs8LrTDdJ7zJB2tTdhlCZMa3K4rX0kB9drn03R3Agm84vG9/Lrfv3gGLNhja51TqWbJ9Y7dMtxGXzi/5e359HYBvc1tPBIGaT2hDldROwx6yW+bDl0eRVzfGi18bvqDG04E3kl31y3Gf3F1FifCVly6Wgs8b7j1QtwHsN2gVcxZ/B9y41dw+nxI4vIKh2GN2S8X8hidhSOZXHq9549s8PIlIA1qMtLh0rNNwrN2wlGc3OSk5GMH9tPiqkw1eM2cNsDE5bKMtLp3E4ZUSZtKc14Ql8Btf8Yw8UGkN8B2kujudmkh93jSDNcHupjmtieu4VVQ/3PxeL5X5s8ASqTsHb/tQZDcIXjS7olLiqxdYD8YX1MAcjP7oFfQN+4FXMrz0Z9AML71ByK6iJPRa1zoCJs5Cfd4mGP3xmIpLJ5rhJTeI3CWfxdDdVyLfQSv/0MgH3zh4VwXZe/j2fFTFpdM4vLWQXUnHkoK7qd0GR9wDpBsyURa6PNyGRI6ouLTwHzHO7lJ0kV1ZLbdR/ArwxuG7W8HoFnbDDC+yq0liNhjgutZkV9hZd08R8bzjs7wiu7GG9/oaB2uqVF4DPQjB6MbhGw7v9pxEQ1Y/gSEO+eFN4zSwkRrJm0h3ZjsjndRQfMXH1o2OO7oJdxuePiiKex/Cl4h7gLd5hOzmkumqBPCrxUjazK+zlxh4BT0cAbyt4V2Gx/A26CK8Rpmvije+pmJ9lqkzRy8Jyz1lbt+lxOzieM0oK6F+/OoX1xtfno8Be7/Rw1s/CB+scXQJvV7ZLnskB54+wzfTxfVfd9sZyysaXvorhl0KL9JrUJrSJV7FJu347gq88ezW6JYIr0MJSj8QuYtNmvnVX7wz8NYPQh1ezm5ZIrxWAf0CwKu8i00aze+OwBtteGuzS4Q+b7S6+HVfXCO/Bnx3A95Ydo9FdhHeFHIP30DFJru8h+UcHAAsw3f55SefgkN5De3TKg277RPXGFCWQmaArSE5ppcpTwrmNzgkksTyFlpdaXj7xBIML/3p6fCSyytcp6iQKZSiwPgHIje+ahqnUyJ8axLLCw/l1donlmJ449ilQsObUuHWwDF4W/rQK8DHC0uDA8rU9onVGN4gp8HELsKbWgK/fqbYYX7D4OUxvH5Fc7LBG8XusZFdhDe9JGS94iBs+NKQ9qnDWz9Ixy7Cm0Utv54+hAFfL8M7WngVw+vj8LJLaRr5Irx5VLsM3g6wlV5Y89HCy3+nZBfhzajA6QcjvtDGMrxkx3e+8Tuw3F4meFvDS3/6sVta2EV4c6qePYv2HeAVziR4hU3fhy20Z3IaYC1rs2vkFOHNqGNRPg1VfIPg3b79TtCfYfNlmeDlvym7c8ouaNHl2MkuwptRLbf+AEszD1rFM7tGGdsQ6jQ43F0qhDefZKMbjO+1qeKZTeOEl//2dBpc7i4VwptPmscQxG8wvNsvgTV5Le2TqTa8qdlFeHNKdxbCzC+ruwNqoE2VeSKcAV7ZaQDPknWzi/DmlNHT9eSX07sEur0avJ5bquSAl/8WDC9gtAZgF+HNKyOmITEPwZZ3cHgNhrc7uP4Ywi7Cm1k2RD0A9mF3jPDy39Twcp+hC14Au15XBRWkBBn004bXOFrrgJdfFGRzYIEy6LsA9riL44OX/5ZmGtzwIrsjEcAxAPALv4tabAMPbRgqtkEyvM1EgxNeZHcM8vBrXS/1Gt+NLLbBPMXrzMhDdicoJ7/gXkYW22ByGpwJpe1QDdmdmGwAB8EbpLTwGp0GF7zI7qRlGsJ5LGqMDF72q2W3NbxGetFlmL5MERH+Pi/R+5/Z9sOfQmccksLbGF7yozG8vGSrAV5kdzckAOtV10iCb/u8OOLjtiPg+6aE1zLTYLW8yO7OqMZXi01zSoSvwvbRBZ3o5SUcPNvHShytCeE4yO5e6FgSqIlcMYfYW7pKsYaa3oTwmg2vDd5jZHfXFAMvN7cU3iH2YbOwWxrneZHd3VT4IkWb+j7ADpjiaE1i17THhuDfJzsB1AgUCS+ZcRgEXvZLN7wGeJHd3VXYPK84SuvfbeCG18guhVegF9ndZYWtsK2KZ/XD3gdsVqfBAC+yu9MKg3fTROPcnfY9VSY4DSdueI+R3d1WYGzDqiC7Zpfl7VnfixRWp6FUfV5kd6cVvjy8fVkUs4dPF0XxGC2kykgAAA0XSURBVJpBnApe9svErgxv88GQXZQC3+3zitzZo4vQ9oESDK+e6U6yh+vnkF1Uq1FEldlHa/UL+G9kFyXIAN/d04fSHO/t08oYMz9i+82imH0muhRp4GW/zIa3fcExsosSZYJXXqC4WdC0oPvkuVWhRpylgNfpNLSxDcguSlYnvNvz4ouSb3C1IbMRt2ftdHAieNkvq9PADrVjUGQXRdUJ793pUfNrxfe6EkxvAng7DC/bpuAY2UWp6nYb6iePKiNM14z5L2t7X3WwW5LnkV2ULgN827eGzOFN5TZwI1yuGNwsRT76DGrDay0IeULZrZ9HdlG1gPDRQB0FXp/2DnUaXsYuP4DsohrB4LtZEG83C7zM8LrYPabsskPILqoVCL41i3nIAa/iNBheUbNLjiG7KEEA+LbnBRuh5RiwdToNNbrkGLKLEtVdq2xLp3ip0k+VdRpeZBdllQjf5aL46JNazc4UQoh6+kUK2fDqx8kMGYcXSzqhFEnwmZJ/+OowM8Wpl4fl0Zp+nM/ukmPILkqVDN+m8RCEpwR4t1+nDcxxOw3tysQJugwoXQp8K6+y6Hp7P7kNr7CqdoLsonQNGs8rGV71oJgMguyiDBoSXqfhRXZRXRoQXii7xGcwr1+g9ls6fO9oVf9vgRV6Y+ClP82jNbS7qG6p8EkzYwHt4XIZXmQXBZAK36p4uJh99LTIXnRk7hitIbsoiBT4SKkcsgi81id8Qe3hatbWdKcB2UWBpMF78HpdPMtfaM/hNCC7KJgM8LKkibw+r8NpQHZRQGk+7+wFiRq7WWSGl/40OQ3ILgoqFb5NcfD9efHL87wlTu2GF9lFgaXB9+aD1zdnvMZISHuI5pLhFQ4cI7souMzwvQfu+R4KL/2pj9aQXZSP1AEbr1O2Pc/o89qcBqkuK7KL6pIE37t3P50evHpX6TLngM0yWrOz67HHBmqPpOyA2SrfPK9litfKrlexbNQeSYLv9rtvF7M/0cAcQ9Gc7vYwmZ0Gp91FeFEGKfBtv/wUSK25PUCN4ZWchk52kV6Uqv7jeT3ZLY/5LvYIL0qRDN/2klTG2Z4/zjdVxg2vXFXPNc+AlhdlkZL6ToPJbk+L2TPL653tITIZXvccGbKLMkuEr2L3Y+bxvskWz0sNrxe7CC/KInn71iaIN9v2raLTwJ/qWptAeFFm9bxxtsHwdq6rXTP5vRFqDyQV2mtX1XLF8+qGt3tNGOFFmdUvvNzwhrCL9KJUSW6DWA8yi9vADK8wSwaIxUF4URaJ8LXECjV5Pdp3SjO8kDgyhBdlkQgfKYFOt8y+PYcaXk94S3920edF2STBV9Fb3Hv4dAGOKfODlxne0pNdhBdlkQLfJSF39uhVaHunWsNL/4THniO6KJN6DMxhhrdxGnzyJpBdlEGZ4Z3zlJ9SGq2VSroagdfZDcKLMigrvHMm/gf5EcIu+rwos3qDVzK8SqgCookKUU5453OBXtHwIruoFOoLXnG0huyikqg3eMkTS2QXlVA9+byt4UV2UanUF7xl7TQgu6hUyjzPy1FtDS+yi0qmrPA2CTzILiqDeoGXGl7uNIjHkV1UjHLC21RcEAyveBzZRUWpD3iJ4UV2UcnVC7xlDa94FNlFRSonvEum1vCKB5FdVKz6gNe0vTCyi4pWZnipx7ssl8guKr2yTpVJhlc8gOyiEig7vMTwqk4DsotKoczLwxW8pWZ4kV1UEuVOwCRTDcguKouyw6vNNCC7qETKn/p+jOyi8ig7vMguKpdyw3ssw4vsotIpM7zXyC4qm7LCW7EqjdaQXVRK9QGv8Gfku6FQgnLCy9mtkUV2UWmVGd7rFl5kF5VYueFta+Qhu6jEyu3zIruobOoLXnQaUMmVe54XHV5UNvVT1h/ZRWWQH7zbbxbF7DNxpyBQe2QXlUN+8K4KInFDeEh7ZBeVRV7wbor7F+XtWbvLK6g9sovKIy94V7MX1c+bhWB6u9sju6hM8oF3e043xuS/gO2RXVQu+cB7d8pM7urgNW1K1dEG2UVlUwS8oPbILiqbcsOLQmUTwouarLIP2FCoXMo/VYZCZVIPixQoVB71sTyMQmWRZ2DO10GBOShUDvUTEolCZRDCi5qsEF7UZIXwoiYrhBc1WSG8qMkK4UVNVggvarJCeFGTVTS8KFTPSgZvJ9wj6gVPJm8vvZ8MwjtQL6M6mYl+JIR3oF5GdTIT/UgI70C9jOpkJvqRcLYANVkhvKjJCuFFTVYIL2qyQnhRkxXCi5qscsKr11H37eB5UXcQ0xdpWzyK7YaezBdNh0G93J2yqgG3T6u+HoeeUd3Lmq2WPovrZftyEXyRhc8h9ujZjdxLuWGlFQC95IRXT5T3091Z20FEX9tz2paW+Qnv5u40/mTueMmLmwXt4P7roL7qXnhT+kd4L/zqBH0u8XNo5wXuRu6F/PkM2EtGeA0lSvy0Lqr/jrdnpExPTF9r2va8eBLVzao4vKisFGka2svlgpvJ86Ky4KFnVPcilt2K6GVDPtftachFFj+H1KNXN3Iv9D/TM2AvGeE1FIfyEr85a3L+EX1tz2ldQFolMLybu1Nepy24l+1vi/t/oPeCFywMOqO2l6buYRnVy5o23RB0fHsRP4fQo2c3Yi/0fFg3kF7ywWsqyxegH08r9mL6ulk8SXBKTYXMw6vAXu5+9dnVRjQkpEvvvoRe2g8W00sLb+jVoZem7TH08rALXPVBuwH1kg9eU0FUb1VjkupbLaqv6lpcVs7zo7huGst78DqiFwleAkxQX5v66/mzpxGfq/kvQNwG4puFfq4N/8LnPQZ2w3ohjWk3oF5GDu/qAR1pxcH7gLr+VdOYblbEAa983mTwVtQEfrDaZrLxWih29bm8IeOlGZQXXfRzCD2GdcN7IY12Bt6S3KOjSHiLj6/K988ju2Fj4tmHqeC9WZDv6xjsVuRzVf+dAj9XPSP1nP4XeBxqIdjnEHoM6ob3smbj4d2BN/Kbuv5Wi+2GzkY+vFglgpdOgcTByxT8uZT/AoEuDP8cQo8h3fBemBc/BngTDdjo+ccN2J6l6IaJNI3opcZue86mncMukgRv8OeSUCP/BQJ6aT6H0KN/N00v6zpLbfZi4AFb9FQZHyPdkemGiL6E2xPTDTMBQVNKreqv6npSM6yvGrv29sb0EnF1hM/R9ug/b9f0IsA78FRZ/CIFHSNFry403RxFdVO53lfl5SJuxaT5qn7WPuPfV9NL1OWp7SQfiIZcnZX80mYWxK8bpRfezcCLFPHLw6cp1nXrVeaDsMVY5WSojQjuhd0Xvh7KTimgr029SBF1eZqpstrWha7r8kvbujN+3ai9tP83h1weNtRR9+1ACMyJ6IuEnhSPY7shJ3OPB+aE9lIbFeF2BfRVQ3L7vA3vieuFzhZ79yJ9DqFHv27UXhrfqrsXDIlETVYIL2qyQnhRkxXCi5qsEF7UZIXwoiYrhBc1WSG8qMkK4UVNVgivQ0pOtqDVwz+yp7f/+7SOTVnzwFYWTCK1vaz+KB5+5ej1PTgO6+5XL9SnlJarJ+oLdlQIr11KTraoFc+UJYubRnjFttuXfAGU1o4w9vrDB6+h8K705X6l5c0vNLx3UwivVUpOtqTV7EMeLH1vYYJXarsq7n9VwXV5RsJMzL3CI7c3s24yDXzvpBBeq5ScbEmrg3/lCfW/McIrtm2SvCpun1l6hcMLARMC+C4I4e0SK69w+LfnxexzGlpG3NXVwX/TBI1N9dvs8wptG5TUI7Vo1ZojFlauvBELHWuDq1heiPIqnt/x4xl5Tu18h4XwdoklTxz+jjiqX5zzmN7VwV9OqUdw+KMLXqEcApFU40ZwGyR45TfiHnLTI3sT5VUM3kIIOI7MG5yIEN4OsS99WuzpckF+viHh3xUdK5q5/qQt/dEksTSoSdntRA1Ubb54e4DBq74Rz498JvWgvIrDe3RFU63L9v/RjgvhdYvnZNOvflY4ijF28Jo4ltU/B7xydjtRDa+QL94eaLPR2jfiVpxWmWIPWOKE/Cr2j/zFE9s24blXUxLC61Sd2b1qsG3grawuKf50Y3UbeFuD2yDmizO18Mpv1OTINGO+pjaH8Ko2p5kfR3hRbWa3Ad7q918rfm3wCm2VAZucL142/Tvh5SYb4RWF8NolZqjr8Faw/tsvXtjgFdrKU2Vqvnjbvxle+bUIryiE1y4hJ9sE783iAf1phFfM5yaLFGW9SKFlerOXVG1N8G7PZ59fkXpitd/MB2wd8OKAbd8lfmWb4N3SUhBmeKWve2l5WDzSMrZupsqUNxIz09s36YJ3FVulaBpCeK0Sc7JN8DIbaoZXyecWAnPEIy28d2fF4d9M8IqZ6axzOr3shvfudD9CcxDeIfXS/9sdYlRxeRiVXXf/EFD0EgNzGiG8A2rzeUCjbjIxJBI1UhmC0RVhMDoKNXYhvKjJCuFFTVYIL2qyQnhRkxXCi5qsEF7UZIXwoiYrhBc1Wf0/9Aa7V2JAR+AAAAAASUVORK5CYII=" />

<!-- rnb-plot-end -->

<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuI2dnc2F2ZShcIm91dHB1dC9PTF9veGkucG5nXCIsIHdpZHRoID0gNiwgaGVpZ2h0ID0gOClcbmBgYCJ9 -->

```r
#ggsave("output/OL_oxi.png", width = 6, height = 8)
```

<!-- rnb-source-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->

## Basal expression level of OL variants

<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-plot-begin eyJoZWlnaHQiOjQzMi42MzI5LCJ3aWR0aCI6NzAwLCJzaXplX2JlaGF2aW9yIjowLCJjb25kaXRpb25zIjpbXX0= -->

<img src="data:image/png;base64,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" />

<!-- rnb-plot-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->

## Plateau/maximum expression Level of OL variants (V1)
The logic is cancel out the impact of basal expression level of each variants. To do so, minus the 0 min basal expression level from each variants, then plot the deduced data at all tp and the selected tp.

<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-plot-begin eyJoZWlnaHQiOjQzMi42MzI5LCJ3aWR0aCI6NzAwLCJzaXplX2JlaGF2aW9yIjowLCJjb25kaXRpb25zIjpbXX0= -->

<img src="data:image/png;base64,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" />

<!-- rnb-plot-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->


## Induction Rate of OL variants (V2)
The logic is get the median value of each variants at 0 minutes, then calculate the relative induction rate = Vartp/Var0min

<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuIyBjYWxjdWxhdGUgYmFzYWwgbWVhblxuZGF0YS5iYXNhbF9tZWFuLnBpIDwtIGRhdGEub2wgJT4lIGZpbHRlcighaXMubmEobmV3X21lZGlhbiksIFRpbWUgPT0gXCIwbWluXCIsIFRyZWF0bWVudCA9PSBcIjBQaVwiKSAlPiUgZ3JvdXBfYnkoR2Vub3R5cGUpICU+JSBtdXRhdGUoYmFzYWxfbWVhbiA9IG1lYW4obmV3X21lZGlhbikpICU+JSBzZWxlY3QoYmFzYWxfbWVhbiwgZ2Vub3R5cGUpXG5gYGAifQ== -->

```r
# calculate basal mean
data.basal_mean.pi <- data.ol %>% filter(!is.na(new_median), Time == "0min", Treatment == "0Pi") %>% group_by(Genotype) %>% mutate(basal_mean = mean(new_median)) %>% select(basal_mean, genotype)
```

<!-- rnb-source-end -->

<!-- rnb-output-begin eyJkYXRhIjoiQWRkaW5nIG1pc3NpbmcgZ3JvdXBpbmcgdmFyaWFibGVzOiBgR2Vub3R5cGVgXG4ifQ== -->

```
Adding missing grouping variables: `Genotype`
```



<!-- rnb-output-end -->

<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuZGF0YS5iYXNhbF9tZWFuLmgybzIgPC0gZGF0YS5vbCAlPiUgZmlsdGVyKCFpcy5uYShuZXdfbWVkaWFuKSwgVGltZSA9PSBcIjBtaW5cIiwgVHJlYXRtZW50ID09IFwiMm1NXCIpICU+JSBncm91cF9ieShHZW5vdHlwZSkgJT4lIG11dGF0ZShiYXNhbF9tZWFuID0gbWVhbihuZXdfbWVkaWFuKSkgJT4lIHNlbGVjdChiYXNhbF9tZWFuLCBnZW5vdHlwZSlcbmBgYCJ9 -->

```r
data.basal_mean.h2o2 <- data.ol %>% filter(!is.na(new_median), Time == "0min", Treatment == "2mM") %>% group_by(Genotype) %>% mutate(basal_mean = mean(new_median)) %>% select(basal_mean, genotype)
```

<!-- rnb-source-end -->

<!-- rnb-output-begin eyJkYXRhIjoiQWRkaW5nIG1pc3NpbmcgZ3JvdXBpbmcgdmFyaWFibGVzOiBgR2Vub3R5cGVgXG4ifQ== -->

```
Adding missing grouping variables: `Genotype`
```



<!-- rnb-output-end -->

<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuIyBjYWxjdWxhdGUgdGhlIHJlbGF0aXZlIGluZHVjdGlvbiByYXRlIFxuaW5kLm9sLnBpIDwtIGxlZnRfam9pbihwaS5vbC5kYXQsIGRhdGEuYmFzYWxfbWVhbi5waSwgYnkgPSBcImdlbm90eXBlXCIpICU+JSB1bmlxdWUoKSAlPiUgXG4gIG11dGF0ZShpbmRfcmF0ZSA9IG5ld19tZWRpYW4vYmFzYWxfbWVhbikgJT4lIHNlbGVjdCgtYyhcIkdlbm90eXBlLnlcIikpICU+JSBtdXRhdGUoZ2Vub3R5cGUgPSBmYWN0b3IoZ2Vub3R5cGUsIGxldmVscyA9IGxldmVscykpXG5gYGAifQ== -->

```r
# calculate the relative induction rate 
ind.ol.pi <- left_join(pi.ol.dat, data.basal_mean.pi, by = "genotype") %>% unique() %>% 
  mutate(ind_rate = new_median/basal_mean) %>% select(-c("Genotype.y")) %>% mutate(genotype = factor(genotype, levels = levels))
```

<!-- rnb-source-end -->

<!-- rnb-output-begin eyJkYXRhIjoiV2FybmluZzogRGV0ZWN0ZWQgYW4gdW5leHBlY3RlZCBtYW55LXRvLW1hbnkgcmVsYXRpb25zaGlwIGJldHdlZW4gYHhgIGFuZCBgeWAuXG4ifQ== -->

```
Warning: Detected an unexpected many-to-many relationship between `x` and `y`.
```



<!-- rnb-output-end -->

<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuY29sbmFtZXMoaW5kLm9sLnBpKVtjb2xuYW1lcyhpbmQub2wucGkpID09ICdHZW5vdHlwZS54J10gPC0gJ0dlbm90eXBlJ1xuXG5pbmQub2wuaDJvMiA8LSBsZWZ0X2pvaW4ob3hpLm9sLmRhdCwgZGF0YS5iYXNhbF9tZWFuLmgybzIsIGJ5ID0gXCJnZW5vdHlwZVwiKSAlPiUgdW5pcXVlKCkgJT4lIFxuICBtdXRhdGUoaW5kX3JhdGUgPSBuZXdfbWVkaWFuL2Jhc2FsX21lYW4pICU+JSBzZWxlY3QoLWMoXCJHZW5vdHlwZS55XCIpKSAlPiUgbXV0YXRlKGdlbm90eXBlID0gZmFjdG9yKGdlbm90eXBlLCBsZXZlbHMgPSBsZXZlbHMpKVxuYGBgIn0= -->

```r
colnames(ind.ol.pi)[colnames(ind.ol.pi) == 'Genotype.x'] <- 'Genotype'

ind.ol.h2o2 <- left_join(oxi.ol.dat, data.basal_mean.h2o2, by = "genotype") %>% unique() %>% 
  mutate(ind_rate = new_median/basal_mean) %>% select(-c("Genotype.y")) %>% mutate(genotype = factor(genotype, levels = levels))
```

<!-- rnb-source-end -->

<!-- rnb-output-begin eyJkYXRhIjoiV2FybmluZzogRGV0ZWN0ZWQgYW4gdW5leHBlY3RlZCBtYW55LXRvLW1hbnkgcmVsYXRpb25zaGlwIGJldHdlZW4gYHhgIGFuZCBgeWAuXG4ifQ== -->

```
Warning: Detected an unexpected many-to-many relationship between `x` and `y`.
```



<!-- rnb-output-end -->

<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuY29sbmFtZXMoaW5kLm9sLmgybzIpW2NvbG5hbWVzKGluZC5vbC5oMm8yKSA9PSAnR2Vub3R5cGUueCddIDwtICdHZW5vdHlwZSdcblxuIyAtIFBpOiBhdCAxODBtaW5cbmluZC5vbC5waSAlPiUgXG4gIGZpbHRlcighaXMubmEobmV3X21lZGlhbiksIGdlbm90eXBlICE9IFwicmVzY3VlXCIsIFRpbWUgPT0gXCIxODBtaW5cIikgJT4lIFxuICBnZ3Bsb3QoYWVzKHggPSBnZW5vdHlwZSwgeSA9IGluZF9yYXRlLCBjb2xvciA9IEdlbm90eXBlKSkgKyBiYXIubGlzdCArXG4gIGdlb21fYm94cGxvdCgpICtcbiAgc3RhdF9zdW1tYXJ5KGZ1bi5kYXRhID0gXCJtZWFuX2NsX2Jvb3RcIiwgY29sb3IgPSBcIlJlZFwiLCBsaW5ld2lkdGggPSAxLCBzaXplID0gMC44KSArXG4gIGdlb21faml0dGVyKHdpZHRoID0gMC4yKSArXG4gIHNjYWxlX2NvbG9yX3ZpcmlkaXNfZChsaW1pdHMgPSBuYW1lcyhsZXZlbHMubm9yZXNjdWUpKSArXG4gIHlsYWIoXCJSZWxhdGl2ZSBJbmR1Y3Rpb24gUmF0ZVwiKSArXG4gIHhsYWIoXCJJbnRlcm5hbCBSZW1vdmFsIChJUikgVmFyaWFudHMsIDBtTSBQaSwgMTgwIG1pblwiKVxuYGBgIn0= -->

```r
colnames(ind.ol.h2o2)[colnames(ind.ol.h2o2) == 'Genotype.x'] <- 'Genotype'

# - Pi: at 180min
ind.ol.pi %>% 
  filter(!is.na(new_median), genotype != "rescue", Time == "180min") %>% 
  ggplot(aes(x = genotype, y = ind_rate, color = Genotype)) + bar.list +
  geom_boxplot() +
  stat_summary(fun.data = "mean_cl_boot", color = "Red", linewidth = 1, size = 0.8) +
  geom_jitter(width = 0.2) +
  scale_color_viridis_d(limits = names(levels.norescue)) +
  ylab("Relative Induction Rate") +
  xlab("Internal Removal (IR) Variants, 0mM Pi, 180 min")
```

<!-- rnb-source-end -->

<!-- rnb-plot-begin eyJoZWlnaHQiOjQzMi42MzI5LCJ3aWR0aCI6NzAwLCJzaXplX2JlaGF2aW9yIjowLCJjb25kaXRpb25zIjpbXX0= -->

<img src="data:image/png;base64,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" />

<!-- rnb-plot-end -->

<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuI2dnc2F2ZShcIm91dHB1dC9PTF9pbmRfMFBpXzE4MC5wbmdcIiwgd2lkdGggPSA2LCBoZWlnaHQgPSA4KVxuXG4jIGNhbGN1bGF0ZSB0aGUgcmF3IG1heCBDVEExLUdGcFxuaW5kLm9sLnBpICU+JSBcbiAgZmlsdGVyKCFpcy5uYShuZXdfbWVkaWFuKSwgZ2Vub3R5cGUgIT0gXCJyZXNjdWVcIiwgVGltZSA9PSBcIjE4MG1pblwiKSAlPiUgXG4gIGdncGxvdChhZXMoeCA9IGdlbm90eXBlLCB5ID0gbmV3X21lZGlhbiwgY29sb3IgPSBHZW5vdHlwZSkpICsgYmFyLmxpc3QgK1xuICBnZW9tX2JveHBsb3QoKSArXG4gIHN0YXRfc3VtbWFyeShmdW4uZGF0YSA9IFwibWVhbl9jbF9ib290XCIsIGNvbG9yID0gXCJSZWRcIiwgbGluZXdpZHRoID0gMSwgc2l6ZSA9IDAuOCkgK1xuICBnZW9tX2ppdHRlcih3aWR0aCA9IDAuMikgK1xuICBzY2FsZV9jb2xvcl92aXJpZGlzX2QobGltaXRzID0gbmFtZXMobGV2ZWxzLm5vcmVzY3VlKSkgK1xuICB4bGFiKFwiSW50ZXJuYWwgUmVtb3ZhbCAoSVIpIFZhcmlhbnRzLCAwbU0gUGksIDE4MCBtaW5cIilcbmBgYCJ9 -->

```r
#ggsave("output/OL_ind_0Pi_180.png", width = 6, height = 8)

# calculate the raw max CTA1-GFp
ind.ol.pi %>% 
  filter(!is.na(new_median), genotype != "rescue", Time == "180min") %>% 
  ggplot(aes(x = genotype, y = new_median, color = Genotype)) + bar.list +
  geom_boxplot() +
  stat_summary(fun.data = "mean_cl_boot", color = "Red", linewidth = 1, size = 0.8) +
  geom_jitter(width = 0.2) +
  scale_color_viridis_d(limits = names(levels.norescue)) +
  xlab("Internal Removal (IR) Variants, 0mM Pi, 180 min")
```

<!-- rnb-source-end -->

<!-- rnb-plot-begin eyJoZWlnaHQiOjQzMi42MzI5LCJ3aWR0aCI6NzAwLCJzaXplX2JlaGF2aW9yIjowLCJjb25kaXRpb25zIjpbXX0= -->

<img src="data:image/png;base64,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" />

<!-- rnb-plot-end -->

<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuI2dnc2F2ZShcIm91dHB1dC9PTF9yYXdfMFBpXzE4MC5wbmdcIiwgd2lkdGggPSA2LCBoZWlnaHQgPSA4KVxuXG5cbiMgMm1NIEgyTzI6IGF0IDkwbWluXG5pbmQub2wuaDJvMiAlPiUgXG4gIGZpbHRlcighaXMubmEobmV3X21lZGlhbiksIGdlbm90eXBlICE9IFwicmVzY3VlXCIsIFRpbWUgPT0gXCI5MG1pblwiKSAlPiUgXG4gIGdncGxvdChhZXMoeCA9IGdlbm90eXBlLCB5ID0gaW5kX3JhdGUsIGNvbG9yID0gR2Vub3R5cGUpKSArIGJhci5saXN0ICtcbiAgZ2VvbV9ib3hwbG90KCkgK1xuICBzdGF0X3N1bW1hcnkoZnVuLmRhdGEgPSBcIm1lYW5fY2xfYm9vdFwiLCBjb2xvciA9IFwiUmVkXCIsIGxpbmV3aWR0aCA9IDEsIHNpemUgPSAwLjgpICtcbiAgZ2VvbV9qaXR0ZXIod2lkdGggPSAwLjIpICtcbiAgc2NhbGVfY29sb3JfdmlyaWRpc19kKGxpbWl0cyA9IG5hbWVzKGxldmVscy5ub3Jlc2N1ZSkpICtcbiAgeWxhYihcIlJlbGF0aXZlIEluZHVjdGlvbiBSYXRlXCIpICtcbiAgeGxhYihcIkludGVybmFsIFJlbW92YWwgKElSKSBWYXJpYW50cywgMm1NIEgyTzIsIDkwIG1pblwiKVxuYGBgIn0= -->

```r
#ggsave("output/OL_raw_0Pi_180.png", width = 6, height = 8)


# 2mM H2O2: at 90min
ind.ol.h2o2 %>% 
  filter(!is.na(new_median), genotype != "rescue", Time == "90min") %>% 
  ggplot(aes(x = genotype, y = ind_rate, color = Genotype)) + bar.list +
  geom_boxplot() +
  stat_summary(fun.data = "mean_cl_boot", color = "Red", linewidth = 1, size = 0.8) +
  geom_jitter(width = 0.2) +
  scale_color_viridis_d(limits = names(levels.norescue)) +
  ylab("Relative Induction Rate") +
  xlab("Internal Removal (IR) Variants, 2mM H2O2, 90 min")
```

<!-- rnb-source-end -->

<!-- rnb-plot-begin eyJoZWlnaHQiOjQzMi42MzI5LCJ3aWR0aCI6NzAwLCJzaXplX2JlaGF2aW9yIjowLCJjb25kaXRpb25zIjpbXX0= -->

<img src="data:image/png;base64,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" />

<!-- rnb-plot-end -->

<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuI2dnc2F2ZShcIm91dHB1dC9PTF9pbmRfSDJPMl85MC5wbmdcIiwgd2lkdGggPSA2LCBoZWlnaHQgPSA4KVxuXG4jIGNhbGN1bGF0ZSB0aGUgcmF3IG1heCBDVEExLUdGcFxuaW5kLm9sLmgybzIgJT4lIFxuICBmaWx0ZXIoIWlzLm5hKG5ld19tZWRpYW4pLCBnZW5vdHlwZSAhPSBcInJlc2N1ZVwiLCBUaW1lID09IFwiOTBtaW5cIikgJT4lIFxuICBnZ3Bsb3QoYWVzKHggPSBnZW5vdHlwZSwgeSA9IG5ld19tZWRpYW4sIGNvbG9yID0gR2Vub3R5cGUpKSArIGJhci5saXN0ICtcbiAgZ2VvbV9ib3hwbG90KCkgK1xuICBzdGF0X3N1bW1hcnkoZnVuLmRhdGEgPSBcIm1lYW5fY2xfYm9vdFwiLCBjb2xvciA9IFwiUmVkXCIsIGxpbmV3aWR0aCA9IDEsIHNpemUgPSAwLjgpICtcbiAgZ2VvbV9qaXR0ZXIod2lkdGggPSAwLjIpICtcbiAgc2NhbGVfY29sb3JfdmlyaWRpc19kKGxpbWl0cyA9IG5hbWVzKGxldmVscy5ub3Jlc2N1ZSkpICtcbiAgeGxhYihcIkludGVybmFsIFJlbW92YWwgKElSKSBWYXJpYW50cywgMm1NIEgyTzIsIDkwIG1pblwiKVxuYGBgIn0= -->

```r
#ggsave("output/OL_ind_H2O2_90.png", width = 6, height = 8)

# calculate the raw max CTA1-GFp
ind.ol.h2o2 %>% 
  filter(!is.na(new_median), genotype != "rescue", Time == "90min") %>% 
  ggplot(aes(x = genotype, y = new_median, color = Genotype)) + bar.list +
  geom_boxplot() +
  stat_summary(fun.data = "mean_cl_boot", color = "Red", linewidth = 1, size = 0.8) +
  geom_jitter(width = 0.2) +
  scale_color_viridis_d(limits = names(levels.norescue)) +
  xlab("Internal Removal (IR) Variants, 2mM H2O2, 90 min")
```

<!-- rnb-source-end -->

<!-- rnb-plot-begin eyJoZWlnaHQiOjQzMi42MzI5LCJ3aWR0aCI6NzAwLCJzaXplX2JlaGF2aW9yIjowLCJjb25kaXRpb25zIjpbXX0= -->

<img src="data:image/png;base64,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" />

<!-- rnb-plot-end -->

<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuI2dnc2F2ZShcIm91dHB1dC9PTF9yYXdfSDJPMl85MC5wbmdcIiwgd2lkdGggPSA2LCBoZWlnaHQgPSA4KVxuXG5gYGAifQ== -->

```r
#ggsave("output/OL_raw_H2O2_90.png", width = 6, height = 8)

```

<!-- rnb-source-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->


##### 2mM H2O2 OL timepoint plot function

<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxudHBfR0ZQIDwtIGZ1bmN0aW9uKC4uLil7XG4gIFxuICBhbGxfdHAgPC0gbGlzdCguLi4pXG4gIGZvciAoaW5wdXRfdHAgaW4gYWxsX3RwKSB7ICAgXG4gIFxuICAgIGRmX3RwIDwtIG94aS5vbC5kYXQgJT4lIGZpbHRlcihuZXdfdGltZSA9PSBpbnB1dF90cCkgJT4lIG11dGF0ZShnZW5vdHlwZSA9IGZhY3RvcihnZW5vdHlwZSwgbGV2ZWxzID0gbGV2ZWxzKSlcbiAgICBcbiAgICBwcmludChnZ3Bsb3QoZGZfdHAsIGFlcyh4ID0gZ2Vub3R5cGUsIHkgPSBuZXdfbWVkaWFuLCBmaWxsID0gR2Vub3R5cGUpKSArIFxuICAgIGdlb21fcG9pbnQoKSArXG4gICAgc3RhdF9zdW1tYXJ5KGZ1bi5kYXRhID0gXCJtZWFuX2NsX2Jvb3RcIiwgY29uZi5pbnQgPSAuOTUsIGNvbG9yID0gXCJSZWRcIiwgbGluZXdpZHRoID0gMSwgc2l6ZSA9IDAuOCkgK1xuICAgIGxhYnMoeCA9cGFzdGUwKFwiMm1NIEgyTzIsIE9MIHZhcmlhbnRzIFwiLCBkZXBhcnNlMShzdWJzdGl0dXRlKGlucHV0X3RwKSksIFwiIG1pblwiKSwgeSA9IFwiQ3RhMS1HRlAgcHJvdGVpbiBsZXZlbCAoYS51LilcIikgK1xuICAgIHRoZW1lX2Nvd3Bsb3QobGluZV9zaXplID0gMC43LCBmb250X3NpemUgPSAxNCkgK1xuICAgIHRoZW1lKGxlZ2VuZC5wb3NpdGlvbiA9IFwibm9uZVwiLFxuICAgICAgICAgIGF4aXMudGl0bGUgPSBlbGVtZW50X3RleHQoc2l6ZSA9IHJlbCgxKSksIFxuICAgICAgICAgIGF4aXMudGV4dC54ID0gZWxlbWVudF90ZXh0KGhqdXN0PTAuNSksIGF4aXMudGV4dCA9IGVsZW1lbnRfdGV4dChzaXplID0gcmVsKDEpKSwpKVxuICB9XG59XG5cbiMgcGxvdCB0aGUgMm1NIEgyTzIgT0wgdmFyaWFudHMgYXQgMG1pbiwgOTBtaW4sIDEyMG1pbiB0aW1lcG9pbnRzXG5cbnRwX0dGUCgwLDkwLDEyMCwyNDApXG5gYGAifQ== -->

```r
tp_GFP <- function(...){
  
  all_tp <- list(...)
  for (input_tp in all_tp) {   
  
    df_tp <- oxi.ol.dat %>% filter(new_time == input_tp) %>% mutate(genotype = factor(genotype, levels = levels))
    
    print(ggplot(df_tp, aes(x = genotype, y = new_median, fill = Genotype)) + 
    geom_point() +
    stat_summary(fun.data = "mean_cl_boot", conf.int = .95, color = "Red", linewidth = 1, size = 0.8) +
    labs(x =paste0("2mM H2O2, OL variants ", deparse1(substitute(input_tp)), " min"), y = "Cta1-GFP protein level (a.u.)") +
    theme_cowplot(line_size = 0.7, font_size = 14) +
    theme(legend.position = "none",
          axis.title = element_text(size = rel(1)), 
          axis.text.x = element_text(hjust=0.5), axis.text = element_text(size = rel(1)),))
  }
}

# plot the 2mM H2O2 OL variants at 0min, 90min, 120min timepoints

tp_GFP(0,90,120,240)
```

<!-- rnb-source-end -->

<!-- rnb-output-begin eyJkYXRhIjoiV2FybmluZzogSWdub3JpbmcgdW5rbm93biBwYXJhbWV0ZXJzOiBgY29uZi5pbnRgXG4ifQ== -->

```
Warning: Ignoring unknown parameters: `conf.int`
```



<!-- rnb-output-end -->

<!-- rnb-plot-begin eyJoZWlnaHQiOjQzMi42MzI5LCJ3aWR0aCI6NzAwLCJzaXplX2JlaGF2aW9yIjowLCJjb25kaXRpb25zIjpbWzEsIldhcm5pbmc6IFx1MDAxYlszODs1OzIzMm1JZ25vcmluZyB1bmtub3duIHBhcmFtZXRlcnM6IGBjb25mLmludGBcdTAwMWJbMzltIl0sWzEsIldhcm5pbmc6IFx1MDAxYlszODs1OzIzMm1JZ25vcmluZyB1bmtub3duIHBhcmFtZXRlcnM6IGBjb25mLmludGBcdTAwMWJbMzltIl0sWzEsIldhcm5pbmc6IFx1MDAxYlszODs1OzIzMm1JZ25vcmluZyB1bmtub3duIHBhcmFtZXRlcnM6IGBjb25mLmludGBcdTAwMWJbMzltIl0sWzEsIldhcm5pbmc6IFx1MDAxYlszODs1OzIzMm1SZW1vdmVkIDEgcm93IGNvbnRhaW5pbmcgbm9uLWZpbml0ZSBvdXRzaWRlIHRoZSBzY2FsZSByYW5nZSAoYHN0YXRfc3VtbWFyeSgpYCkuXHUwMDFiWzM5bSJdLFsxLCJXYXJuaW5nOiBcdTAwMWJbMzg7NTsyMzJtUmVtb3ZlZCAxIHJvdyBjb250YWluaW5nIG1pc3NpbmcgdmFsdWVzIG9yIHZhbHVlcyBvdXRzaWRlIHRoZSBzY2FsZSByYW5nZSAoYGdlb21fcG9pbnQoKWApLlx1MDAxYlszOW0iXV19 -->

<img src="data:image/png;base64,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" />

<!-- rnb-plot-end -->

<!-- rnb-plot-begin eyJoZWlnaHQiOjQzMi42MzI5LCJ3aWR0aCI6NzAwLCJzaXplX2JlaGF2aW9yIjowLCJjb25kaXRpb25zIjpbXX0= -->

<img src="data:image/png;base64,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" />

<!-- rnb-plot-end -->

<!-- rnb-plot-begin eyJoZWlnaHQiOjQzMi42MzI5LCJ3aWR0aCI6NzAwLCJzaXplX2JlaGF2aW9yIjowLCJjb25kaXRpb25zIjpbXX0= -->

<img src="data:image/png;base64,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" />

<!-- rnb-plot-end -->

<!-- rnb-plot-begin eyJoZWlnaHQiOjQzMi42MzI5LCJ3aWR0aCI6NzAwLCJzaXplX2JlaGF2aW9yIjowLCJjb25kaXRpb25zIjpbXX0= -->

<img src="data:image/png;base64,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" />

<!-- rnb-plot-end -->

<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuTkFcbk5BXG5gYGAifQ== -->

```r
NA
NA
```

<!-- rnb-source-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->



**Overlapping variants**
### slope/differetiation of the loess curve

<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-plot-begin eyJoZWlnaHQiOjQzMi42MzI5LCJ3aWR0aCI6NzAwLCJzaXplX2JlaGF2aW9yIjowLCJjb25kaXRpb25zIjpbXX0= -->

<img src="data:image/png;base64,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" />

<!-- rnb-plot-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->


#### Get the loess curve fitting for the timecourse data

<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuIyBuZWVkIG5hbWVzX2NvbG9yc1xuZ2Vub3R5cGVfY29sb3IgPC0gUkNvbG9yQnJld2VyOjpicmV3ZXIucGFsKDgsIFwiRGFyazJcIilbYyg4LCA3LCA2LCAxLCA1LCA0KV0gXG5uYW1lcyhnZW5vdHlwZV9jb2xvcikgPC0gbmFtZXMobGV2ZWxzKVxuXG4jIGNoZWNrIGZvciB0aGUgbG9zcyBmaXQgY3VydmVcbnBpLm9sLmRhdCAlPiUgZ2dwbG90KGFlcyh4ID0gbmV3X3RpbWUsIHkgPSBuZXdfbWVkaWFuLCBjb2xvciA9IEdlbm90eXBlKSkgKyBtZWFuLnRpbWVjb3Vyc2UgKyBzY2FsZV9jb2xvcl9tYW51YWwodmFsdWVzPSBnZW5vdHlwZV9jb2xvciwgbGltaXRzID0gbmFtZXMoZ2Vub3R5cGVfY29sb3IpKSArXG4gIGxhYnMoeCA9IFwiUGhvc3BoYXRlIHN0YXJ2YXRpb24sIFRpbWUgKG1pbilcIilcbmBgYCJ9 -->

```r
# need names_colors
genotype_color <- RColorBrewer::brewer.pal(8, "Dark2")[c(8, 7, 6, 1, 5, 4)] 
names(genotype_color) <- names(levels)

# check for the loss fit curve
pi.ol.dat %>% ggplot(aes(x = new_time, y = new_median, color = Genotype)) + mean.timecourse + scale_color_manual(values= genotype_color, limits = names(genotype_color)) +
  labs(x = "Phosphate starvation, Time (min)")
```

<!-- rnb-source-end -->

<!-- rnb-plot-begin eyJoZWlnaHQiOjQzMi42MzI5LCJ3aWR0aCI6NzAwLCJzaXplX2JlaGF2aW9yIjowLCJjb25kaXRpb25zIjpbXX0= -->

<img src="data:image/png;base64,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" />

<!-- rnb-plot-end -->

<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuI2dnc2F2ZShcIm91dHB1dC9sb2Vzc19PbF8wUGkucG5nXCIsIHdpZHRoID0gNi4zLCBoZWlnaHQgPSA4KVxuXG5veGkub2wuZGF0ICU+JSBnZ3Bsb3QoYWVzKHggPSBuZXdfdGltZSwgeSA9IG5ld19tZWRpYW4sIGNvbG9yID0gR2Vub3R5cGUpKSArIG1lYW4udGltZWNvdXJzZSArIHNjYWxlX2NvbG9yX21hbnVhbCh2YWx1ZXM9IGdlbm90eXBlX2NvbG9yLCBsaW1pdHMgPSBuYW1lcyhnZW5vdHlwZV9jb2xvcikpICtcbmxhYnMoeCA9IFwiMm1NIEgyTzIsIFRpbWUgKG1pbilcIilcbmBgYCJ9 -->

```r
#ggsave("output/loess_Ol_0Pi.png", width = 6.3, height = 8)

oxi.ol.dat %>% ggplot(aes(x = new_time, y = new_median, color = Genotype)) + mean.timecourse + scale_color_manual(values= genotype_color, limits = names(genotype_color)) +
labs(x = "2mM H2O2, Time (min)")
```

<!-- rnb-source-end -->

<!-- rnb-plot-begin eyJoZWlnaHQiOjQzMi42MzI5LCJ3aWR0aCI6NzAwLCJzaXplX2JlaGF2aW9yIjowLCJjb25kaXRpb25zIjpbWzEsIldhcm5pbmc6IFx1MDAxYlszODs1OzIzMm1SZW1vdmVkIDEgcm93IGNvbnRhaW5pbmcgbm9uLWZpbml0ZSBvdXRzaWRlIHRoZSBzY2FsZSByYW5nZSAoYHN0YXRfc3VtbWFyeSgpYCkuXHUwMDFiWzM5bSJdLFsxLCJXYXJuaW5nOiBcdTAwMWJbMzg7NTsyMzJtUmVtb3ZlZCAxIHJvdyBjb250YWluaW5nIG5vbi1maW5pdGUgb3V0c2lkZSB0aGUgc2NhbGUgcmFuZ2UgKGBzdGF0X3Ntb290aCgpYCkuXHUwMDFiWzM5bSJdXX0= -->

<img src="data:image/png;base64,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" />

<!-- rnb-plot-end -->

<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuI2dnc2F2ZShcIm91dHB1dC9sb2Vzc19PbF8ybU1IMk8yLnBuZ1wiLCB3aWR0aCA9IDYuMywgaGVpZ2h0ID0gOClcblxuXG4jIyBnZXQgQVVDIGZvciAtIFBpIGRhdGEgaW50byBhIGRhdGFmcmFtZVxucGkuYXJlYSA8LSBkYXRhLmZyYW1lKG1hdHJpeChuY29sPTIsbnJvdz0wLCBkaW1uYW1lcz1saXN0KE5VTEwsIGMoXCJwaS5hcmVhXCIsIFwiR2Vub3R5cGVcIikpKSlcbnJvd19jbnQgPSAxXG5jb2xfY250ID0gMVxuZm9yICh4IGluIG5hbWVzKGdlbm90eXBlX2NvbG9yKSkge1xuIyBjYWxjdWxhdGUgQVVDICBcbm1hZGV1cC5waSA8LSBwaS5vbC5kYXQgJT4lIGZpbHRlcihHZW5vdHlwZSA9PSB4KSAlPiUgbG9lc3MoZm9ybXVsYSA9IG5ld19tZWRpYW4gfiBuZXdfdGltZSwgc3BhbiA9IDAuNzUsIGRlZ3JlZSA9IDIpIFxuZiA8LSBmdW5jdGlvbih4KSBwcmVkaWN0KG1hZGV1cC5waSxuZXdkYXRhPXgpXG4jIHBlcmZvcm0gaW50ZWdyYXRpb25cbnRtcCA8LSBpbnRlZ3JhdGUoZiwwLDI0MCkkdmFsdWVcbmd0X3RtcCA8LSB4XG5waS5hcmVhW3Jvd19jbnQsY29sX2NudF0gPC0gdG1wXG5jb2xfY250ID0gY29sX2NudCArIDFcbnBpLmFyZWFbcm93X2NudCxjb2xfY250XSA8LSBndF90bXBcbmNvbF9jbnQgPSAxXG5yb3dfY250ID0gcm93X2NudCArIDFcbn1cblxuXG4jIGdldCBBVUMgZm9yIDJtTSBIMk8yIGRhdGFcbmgybzIuYXJlYSA8LSBkYXRhLmZyYW1lKG1hdHJpeChuY29sPTIsbnJvdz0wLCBkaW1uYW1lcz1saXN0KE5VTEwsIGMoXCJoMm8yLmFyZWFcIiwgXCJHZW5vdHlwZVwiKSkpKVxucm93X2NudCA9IDFcbmNvbF9jbnQgPSAxXG5mb3IgKHggaW4gbmFtZXMoZ2Vub3R5cGVfY29sb3IpKSB7XG4jIGNhbGN1bGF0ZSBBVUMgIFxubWFkZXVwLmgybzIgPC0gb3hpLm9sLmRhdCAlPiUgZmlsdGVyKEdlbm90eXBlID09IHgpICU+JSBsb2Vzcyhmb3JtdWxhID0gbmV3X21lZGlhbiB+IG5ld190aW1lLCBzcGFuID0gMC43NSwgZGVncmVlID0gMikgXG5mIDwtIGZ1bmN0aW9uKHgpIHByZWRpY3QobWFkZXVwLmgybzIsbmV3ZGF0YT14KVxuIyBwZXJmb3JtIGludGVncmF0aW9uXG50bXAgPC0gaW50ZWdyYXRlKGYsMCwyNDApJHZhbHVlXG5ndF90bXAgPC0geFxuaDJvMi5hcmVhW3Jvd19jbnQsY29sX2NudF0gPC0gdG1wXG5jb2xfY250ID0gY29sX2NudCArIDFcbmgybzIuYXJlYVtyb3dfY250LGNvbF9jbnRdIDwtIGd0X3RtcFxuY29sX2NudCA9IDFcbnJvd19jbnQgPSByb3dfY250ICsgMVxufVxuXG4jIGNvbWJpbmQgYXJlYSBkYXRhXG5hcmVhLm9sIDwtIG1lcmdlKHBpLmFyZWEsaDJvMi5hcmVhKVxuYGBgIn0= -->

```r
#ggsave("output/loess_Ol_2mMH2O2.png", width = 6.3, height = 8)


## get AUC for - Pi data into a dataframe
pi.area <- data.frame(matrix(ncol=2,nrow=0, dimnames=list(NULL, c("pi.area", "Genotype"))))
row_cnt = 1
col_cnt = 1
for (x in names(genotype_color)) {
# calculate AUC  
madeup.pi <- pi.ol.dat %>% filter(Genotype == x) %>% loess(formula = new_median ~ new_time, span = 0.75, degree = 2) 
f <- function(x) predict(madeup.pi,newdata=x)
# perform integration
tmp <- integrate(f,0,240)$value
gt_tmp <- x
pi.area[row_cnt,col_cnt] <- tmp
col_cnt = col_cnt + 1
pi.area[row_cnt,col_cnt] <- gt_tmp
col_cnt = 1
row_cnt = row_cnt + 1
}


# get AUC for 2mM H2O2 data
h2o2.area <- data.frame(matrix(ncol=2,nrow=0, dimnames=list(NULL, c("h2o2.area", "Genotype"))))
row_cnt = 1
col_cnt = 1
for (x in names(genotype_color)) {
# calculate AUC  
madeup.h2o2 <- oxi.ol.dat %>% filter(Genotype == x) %>% loess(formula = new_median ~ new_time, span = 0.75, degree = 2) 
f <- function(x) predict(madeup.h2o2,newdata=x)
# perform integration
tmp <- integrate(f,0,240)$value
gt_tmp <- x
h2o2.area[row_cnt,col_cnt] <- tmp
col_cnt = col_cnt + 1
h2o2.area[row_cnt,col_cnt] <- gt_tmp
col_cnt = 1
row_cnt = row_cnt + 1
}

# combind area data
area.ol <- merge(pi.area,h2o2.area)
```

<!-- rnb-source-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->


#### Check the loess fitting assumption: normality and curve fitting

<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->



<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->


### regulatory information map

<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuIyBjYWxjdWxhdGUgdGhlIHJlbGF0aXZlIGluZm9ybWF0aW9uIHJldGFpbmluZyB3aXRoaW4gZWFjaCBnZW5vdHlwZVxucmVnX2luZm8ub2wgPC0gYXJlYS5vbCAlPiUgXG4gIG11dGF0ZShwaV9wY250ID0gcGkuYXJlYS8oLlsuJEdlbm90eXBlID09IFwiV1RcIixdJHBpLmFyZWEpKSAlPiUgXG4gIG11dGF0ZShoMm8yX3BjbnQgPSBoMm8yLmFyZWEvKCguWy4kR2Vub3R5cGUgPT0gXCJXVFwiLF0kaDJvMi5hcmVhKSkpXG5cbnJlZ19pbmZvLm9sICU+JSBcbiAgZ2dwbG90KGFlcyh4ID0gcGlfcGNudCwgeSA9IGgybzJfcGNudCksIGNvbG9yID0gR2Vub3R5cGUpICtcbiAgc2NhdHRlciArIFxuICBnZW9tX3BvaW50KHNpemUgPSAzLCBhZXMoY29sb3IgPSBHZW5vdHlwZSkpICtcbiAgZ2VvbV9hYmxpbmUoc2xvcGUgPSAxLCBpbnRlcmNlcHQgPSAwLCBsaW5ldHlwZSA9IFwiZGFzaGVkXCIsIGNvbG9yID0gXCIjNjY2NjY2XCIpICtcbiAgbGFicyh4ID0gXCJQaSAocmVsYXRpdmUgdG8gd3QpXCIsIHkgPSBcIkgyTzIgKHJlbGF0aXZlIHRvIHd0KVwiKSArXG4gIHNjYWxlX2NvbG9yX21hbnVhbCh2YWx1ZXMgPSBnZW5vdHlwZV9jb2xvciwgbGltaXRzID0gbmFtZXMoZ2Vub3R5cGVfY29sb3IpKVxuYGBgIn0= -->

```r
# calculate the relative information retaining within each genotype
reg_info.ol <- area.ol %>% 
  mutate(pi_pcnt = pi.area/(.[.$Genotype == "WT",]$pi.area)) %>% 
  mutate(h2o2_pcnt = h2o2.area/((.[.$Genotype == "WT",]$h2o2.area)))

reg_info.ol %>% 
  ggplot(aes(x = pi_pcnt, y = h2o2_pcnt), color = Genotype) +
  scatter + 
  geom_point(size = 3, aes(color = Genotype)) +
  geom_abline(slope = 1, intercept = 0, linetype = "dashed", color = "#666666") +
  labs(x = "Pi (relative to wt)", y = "H2O2 (relative to wt)") +
  scale_color_manual(values = genotype_color, limits = names(genotype_color))
```

<!-- rnb-source-end -->

<!-- rnb-plot-begin eyJoZWlnaHQiOjQzMi42MzI5LCJ3aWR0aCI6NzAwLCJzaXplX2JlaGF2aW9yIjowLCJjb25kaXRpb25zIjpbXX0= -->

<img src="data:image/png;base64,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" />

<!-- rnb-plot-end -->

<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuI2dnc2F2ZShcIm91dHB1dC9PbHZzd3RfMHBpdnNoMm8yX3NjYXR0ZXIucG5nXCIsIHdpZHRoID0gNi4zLCBoZWlnaHQgPSA2LjMpXG5cbiMgc2F2ZSB0aGUgcmVnX2luZm8ub2wgXG4jd3JpdGUuY3N2KHJlZ19pbmZvLm9sLCBmaWxlID0gXCJvdXRwdXQvb2xfcGN0LmNzdlwiLCByb3cubmFtZXMgPSBGKVxuI3dyaXRlLmNzdihyZWdfaW5mby5vbCwgZmlsZSA9IFwiLi4vUlNfVHJ1blYvaW5wdXQvb2xfcGN0LmNzdlwiLCByb3cubmFtZXMgPSBGKVxuYGBgIn0= -->

```r
#ggsave("output/Olvswt_0pivsh2o2_scatter.png", width = 6.3, height = 6.3)

# save the reg_info.ol 
#write.csv(reg_info.ol, file = "output/ol_pct.csv", row.names = F)
#write.csv(reg_info.ol, file = "../RS_TrunV/input/ol_pct.csv", row.names = F)
```

<!-- rnb-source-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->






### Import TrunV data and get the replicate, time and genotype info

<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuZmlsZXMgPC0gZGlyKFwiaW5wdXQvVHJ1blZfMFBpXCIsIHBhdHRlcm4gPSBcImQwMSpcIikgIyBnZXQgdGhlIGZpbGUgbmFtZXMgb2YgdGhlIG1lcmdlZFxuZmlsZXMgPC0gZmlsZS5wYXRoKFwiaW5wdXQvL1RydW5WXzBQaVwiLCBmaWxlcykgICAgICAgICAjIHRoaXMgYXBwZW5kcyB0aGUgZGlyZWN0b3J5IHRvIHRoZSBmaWxlIG5hbWVzXG5uYW1lcyhmaWxlcykgPC0gYyhcIlJlcDEtMFBpLUN0cmxcIixcIlJlcDItMFBpLUN0cmxcIiwgXCJSZXAzLTBQaS1DdHJsXCIpXG5cbnRwIDwtIGMoXCIwbWluXCIsICBcIjMwbWluXCIsIFwiNjBtaW5cIiwgXCI5MG1pblwiLCBcIjEyMG1pblwiLCBcIjE1MG1pblwiLCAgXCIxODBtaW5cIiwgXCIyMTBtaW5cIiwgXCIyNDBtaW5cIikgIyBvcmRlcmVkIHRpbWUgcG9pbnRzXG5cbiMgaW1wb3J0IGFuZCBwcm9jZXNzIHRoZSBkYXRhIHRvIHRoZSBmb3JtYXQgd2Ugd2FudFxuZGF0YS5UcnVuVi5waSA8LSBtYXBfZGZyKGZpbGVzLCB+cmVhZF9jc3YoLiwgbmEgPSBjKFwiXCIsIFwiTkFcIiwgXCJOL0FcIiksIGNvbF90eXBlcyA9IGNvbHMoKSksIC5pZCA9IFwiUmVwbGljYXRlXCIpICU+JSBcbiAgI2JpbmRfcm93cyguaWQgPSBcIlJlcGxpY2F0ZVwiKSAlPiUgXG4gIGZpbHRlcighaXMubmEobWVkaWFuKSxgWCBQYXJhbWV0ZXJgID09IFwiQkwxLUhcIiwgaXMubmEoYFkgUGFyYW1ldGVyYCkpICU+JSBcbiAgc2VsZWN0KFJlcGxpY2F0ZSwgR3JvdXAsIFNhbXBsZSwgQ291bnQsIG1lZGlhbiA9IGBYIE1lZGlhbmAsIHBlYWsgPSBgWCBQZWFrYCxcbiAgICAgICAgIHNkID0gYFggU0RgLCBjdiA9IGBYICVDVmAsIHJDViA9IGBYICVyQ1ZgKSAlPiUgXG4gIHNlcGFyYXRlKEdyb3VwLCBpbnRvID0gYygnVGltZScsICdUcmVhdG1lbnQnKSwgc2VwID0gXCItXCIpICU+JSBcbiAgbXV0YXRlKFRpbWUgPSBvcmRlcmVkKFRpbWUsIGxldmVscyA9IHRwKSkgJT4lIFxuICBtdXRhdGUoU2FtcGxlID0gY2FzZV93aGVuKFNhbXBsZSA9PSBcIkNUQTEtR0ZQLXlIMjk4XCIgfiBcInlIMjk4LXd0XCIsXG4gICAgICAgICAgICBTYW1wbGUgPT0gXCJDVEExLUdGUC15SDI5OVwiIH4gXCJ5SDI5OS13dFwiLFxuICAgICAgICAgICAgU2FtcGxlID09IFwieUgzNDMtd3RcIiB+IFwieUgzNDMtcmVzY3VlXCIsXG4gICAgICAgICAgICBTYW1wbGUgPT0gXCJ5SDM0NC13dFwiIH4gXCJ5SDM0NC1yZXNjdWVcIixcbiAgICAgICAgICAgIFRSVUUgfiBTYW1wbGUpKSAlPiUgXG4gIG11dGF0ZShSZXBsaWNhdGUgPSBnc3ViKFwiXFxcXC0uKlwiLFwiXCIsIFJlcGxpY2F0ZSkpICU+JSAgXG4gIHNlcGFyYXRlKFNhbXBsZSwgaW50byA9IGMoXCJTdHJhaW5cIiwgXCJnZW5vdHlwZVwiKSwgc2VwID0gXCItXCIpICU+JSBcbiAgZmlsdGVyKCFpcy5uYShtZWRpYW4pKSAlPiUgXG4gIGFycmFuZ2UoVGltZSkgXG5gYGAifQ== -->

```r
files <- dir("input/TrunV_0Pi", pattern = "d01*") # get the file names of the merged
files <- file.path("input//TrunV_0Pi", files)         # this appends the directory to the file names
names(files) <- c("Rep1-0Pi-Ctrl","Rep2-0Pi-Ctrl", "Rep3-0Pi-Ctrl")

tp <- c("0min",  "30min", "60min", "90min", "120min", "150min",  "180min", "210min", "240min") # ordered time points

# import and process the data to the format we want
data.TrunV.pi <- map_dfr(files, ~read_csv(., na = c("", "NA", "N/A"), col_types = cols()), .id = "Replicate") %>% 
  #bind_rows(.id = "Replicate") %>% 
  filter(!is.na(median),`X Parameter` == "BL1-H", is.na(`Y Parameter`)) %>% 
  select(Replicate, Group, Sample, Count, median = `X Median`, peak = `X Peak`,
         sd = `X SD`, cv = `X %CV`, rCV = `X %rCV`) %>% 
  separate(Group, into = c('Time', 'Treatment'), sep = "-") %>% 
  mutate(Time = ordered(Time, levels = tp)) %>% 
  mutate(Sample = case_when(Sample == "CTA1-GFP-yH298" ~ "yH298-wt",
            Sample == "CTA1-GFP-yH299" ~ "yH299-wt",
            Sample == "yH343-wt" ~ "yH343-rescue",
            Sample == "yH344-wt" ~ "yH344-rescue",
            TRUE ~ Sample)) %>% 
  mutate(Replicate = gsub("\\-.*","", Replicate)) %>%  
  separate(Sample, into = c("Strain", "genotype"), sep = "-") %>% 
  filter(!is.na(median)) %>% 
  arrange(Time) 
```

<!-- rnb-source-end -->

<!-- rnb-output-begin eyJkYXRhIjoiV2FybmluZzogVGhlcmUgd2FzIDEgd2FybmluZyBpbiBgZmlsdGVyKClgLlxu4oS5IEluIGFyZ3VtZW50OiBgIWlzLm5hKG1lZGlhbilgLlxuQ2F1c2VkIGJ5IHdhcm5pbmcgaW4gYGlzLm5hKClgOlxuISBpcy5uYSgpIGFwcGxpZWQgdG8gbm9uLShsaXN0IG9yIHZlY3Rvcikgb2YgdHlwZSAnY2xvc3VyZSdXYXJuaW5nOiBFeHBlY3RlZCAyIHBpZWNlcy4gQWRkaXRpb25hbCBwaWVjZXMgZGlzY2FyZGVkIGluIDEgcm93cyBbMTUzXS5XYXJuaW5nOiBFeHBlY3RlZCAyIHBpZWNlcy4gTWlzc2luZyBwaWVjZXMgZmlsbGVkIHdpdGggYE5BYCBpbiAxIHJvd3MgWzE1MV0uXG4ifQ== -->

```
Warning: There was 1 warning in `filter()`.
ℹ In argument: `!is.na(median)`.
Caused by warning in `is.na()`:
! is.na() applied to non-(list or vector) of type 'closure'Warning: Expected 2 pieces. Additional pieces discarded in 1 rows [153].Warning: Expected 2 pieces. Missing pieces filled with `NA` in 1 rows [151].
```



<!-- rnb-output-end -->

<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuIyBUbyByZXBsYWNlIHRoZSB2YWx1ZTogaWZlbHNlKCkgZm9yIGEgc2luZ2xlIHRlc3QsIGNhc2Vfd2hlbigpIGZvciBtdWx0aXBsZSB0ZXN0XG4jIFxcXFwtOiBlc2NhcGUgY2hhcmFjdGVyIFwiXFxcXFwiIHVzZWQgdG8gZXNjYXBlIHRoZSBzcGVjaWFsIG1lYW5pbmcgb2YgLSwgaW5zdGVhZCB0YWtlIC0gYXMgYSBjb21tb24gcmVnZXggcGF0dGVybi4gT3Igd2UgY2FuIHNwZWNpZnkgdGhlIC0gYXMgYSByZWdleCBwYXR0ZXJuIHdpdGhpbiBhIHNxdWFyZSBicmFja2V0IGNsYXNzIFstXVxuIy4qOiBUaGlzIHBhcnQgbWF0Y2hlcyBhbnkgc2VxdWVuY2Ugb2YgY2hhcmFjdGVycyAoLiogaXMgYSBjb21tb24gcmVnZXggcGF0dGVybiBmb3IgXCJhbnkgY2hhcmFjdGVyLCB6ZXJvIG9yIG1vcmUgdGltZXNcIikuIG1ldGFjaGFyYWN0ZXJcbmBgYCJ9 -->

```r
# To replace the value: ifelse() for a single test, case_when() for multiple test
# \\-: escape character "\\" used to escape the special meaning of -, instead take - as a common regex pattern. Or we can specify the - as a regex pattern within a square bracket class [-]
#.*: This part matches any sequence of characters (.* is a common regex pattern for "any character, zero or more times"). metacharacter
```

<!-- rnb-source-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->




#### Plot the truncation variants data (TrunV)

<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuIyByZWNvZGUgdGhlIGdlbm90eXBlXG5sZXZlbHMgPC0gYyhgV1RgID0gXCJ3dFwiLCBgUENgPSBcInJlc2N1ZVwiLCBgSVJfMi4xMGAgPSBcIjJWXCIsIGBJUl80LjEwYCA9IFwiNFZcIiwgYElSXzYuMTBgID0gXCI2VlwiLCBgSVJfOC4xMGAgPSBcIjhWXCIpXG5sZXZlbHMubm9yZXNjdWUgPC0gYyhgV1RgID0gXCJ3dFwiLGBJUl8yLjEwYCA9IFwiMlZcIiwgYElSXzQuMTBgID0gXCI0VlwiLCBgSVJfNi4xMGAgPSBcIjZWXCIsIGBJUl84LjEwYCA9IFwiOFZcIilcbkcubGV2ZWxzIDwtIGMoXCJXVFwiLCBcIlBDXCIsIFwiSVJfOC4xMFwiLCBcIklSXzYuMTBcIiwgXCJJUl80LjEwXCIsIFwiSVJfMi4xMFwiKVxuXG5cbnBpLlRydW5WLmRhdCA8LSBkYXRhLlRydW5WLnBpICU+JSBcbiAgZmlsdGVyKGdlbm90eXBlICVpbiUgYyhcInd0XCIsIFwiMlZcIiwgXCI0VlwiLCBcIjZWXCIsIFwiOFZcIixcInJlc2N1ZVwiKSkgJT4lICBcbiAgc2VsZWN0KFRpbWUsIHJlcGxpY2F0ZSA9IFJlcGxpY2F0ZSwgZ2Vub3R5cGUsIFN0cmFpbiwgbWVkaWFuKSAlPiVcbiAgbXV0YXRlKEdlbm90eXBlID0gZmN0X3JlY29kZShnZW5vdHlwZSwgISEhbGV2ZWxzKSkgJT4lIFxuICBtdXRhdGUobmV3X21lZGlhbiA9bWVkaWFuLzEwMDApICU+JSBcbiAgbXV0YXRlKG5ld190aW1lID0gYXMubnVtZXJpYyhnc3ViKFwibWluXCIsXCJcIixUaW1lKSkpJT4lIFxuICBhcnJhbmdlKG5ld190aW1lLCBnZW5vdHlwZSwgcmVwbGljYXRlKSAlPiUgXG4gIG11dGF0ZShHZW5vdHlwZSA9IGZhY3RvcihHZW5vdHlwZSwgbGV2ZWxzID0gRy5sZXZlbHMpKVxuXG5cbnBpLlRydW5WLmRhdCAlPiVcbiAgZmlsdGVyKCFpcy5uYShuZXdfbWVkaWFuKSwgZ2Vub3R5cGUgIT0gXCJyZXNjdWVcIikgJT4lIFxuICBnZ3Bsb3QoYWVzKHggPSBuZXdfdGltZSwgeSA9IG5ld19tZWRpYW4sIGNvbG9yID0gR2Vub3R5cGUpKSArIHAudGltZWNvdXJzZSArXG4gIHNjYWxlX2NvbG9yX3ZpcmlkaXNfZChsaW1pdHMgPSBuYW1lcyhsZXZlbHMubm9yZXNjdWUpLCBvcHRpb24gPSBcInBsYXNtYVwiKSAgK1xuICBsYWJzKHggPSBcIlBob3NwaGF0ZSBzdGFydmF0aW9uLCBUaW1lIChtaW4pXCIpXG5gYGAifQ== -->

```r
# recode the genotype
levels <- c(`WT` = "wt", `PC`= "rescue", `IR_2.10` = "2V", `IR_4.10` = "4V", `IR_6.10` = "6V", `IR_8.10` = "8V")
levels.norescue <- c(`WT` = "wt",`IR_2.10` = "2V", `IR_4.10` = "4V", `IR_6.10` = "6V", `IR_8.10` = "8V")
G.levels <- c("WT", "PC", "IR_8.10", "IR_6.10", "IR_4.10", "IR_2.10")


pi.TrunV.dat <- data.TrunV.pi %>% 
  filter(genotype %in% c("wt", "2V", "4V", "6V", "8V","rescue")) %>%  
  select(Time, replicate = Replicate, genotype, Strain, median) %>%
  mutate(Genotype = fct_recode(genotype, !!!levels)) %>% 
  mutate(new_median =median/1000) %>% 
  mutate(new_time = as.numeric(gsub("min","",Time)))%>% 
  arrange(new_time, genotype, replicate) %>% 
  mutate(Genotype = factor(Genotype, levels = G.levels))


pi.TrunV.dat %>%
  filter(!is.na(new_median), genotype != "rescue") %>% 
  ggplot(aes(x = new_time, y = new_median, color = Genotype)) + p.timecourse +
  scale_color_viridis_d(limits = names(levels.norescue), option = "plasma")  +
  labs(x = "Phosphate starvation, Time (min)")
```

<!-- rnb-source-end -->

<!-- rnb-plot-begin eyJoZWlnaHQiOjQzMi42MzI5LCJ3aWR0aCI6NzAwLCJzaXplX2JlaGF2aW9yIjowLCJjb25kaXRpb25zIjpbXX0= -->

<img src="data:image/png;base64,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" />

<!-- rnb-plot-end -->

<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuI2dnc2F2ZShcIm91dHB1dC9UcnVuVl8wUGlfbm9yZXNjdWUucG5nXCIsIHdpZHRoID0gNiwgaGVpZ2h0ID0gOClcbmBgYCJ9 -->

```r
#ggsave("output/TrunV_0Pi_norescue.png", width = 6, height = 8)
```

<!-- rnb-source-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->

#### 2mM H2O2 Data
Import 2mM H2O2 TrunV data and get the replicate, time and genotype info

<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuZmlsZXMgPC0gZGlyKFwiaW5wdXQvVHJ1blZfMm1NSDJPMlwiLCBwYXR0ZXJuID0gXCJkKlwiKSAjIGdldCB0aGUgZmlsZSBuYW1lcyBvZiB0aGUgbWVyZ2VkXG5maWxlcyA8LSBmaWxlLnBhdGgoXCJpbnB1dC8vVHJ1blZfMm1NSDJPMlwiLCBmaWxlcykgICAgICAjIHRoaXMgYXBwZW5kcyB0aGUgZGlyZWN0b3J5IHRvIHRoZSBmaWxlIG5hbWVzXG5uYW1lcyhmaWxlcykgPC0gYyhcIlJlcDEtMm1NSDJPMlwiLFwiUmVwMi0ybU1IMk8yXCIsIFwiUmVwMy0ybU1IMk8yXCIpXG5cbnRwIDwtIGMoXCIwbWluXCIsICBcIjMwbWluXCIsIFwiNjBtaW5cIiwgXCI5MG1pblwiLCBcIjEyMG1pblwiLCBcIjE1MG1pblwiLCAgXCIxODBtaW5cIiwgXCIyMTBtaW5cIiwgXCIyNDBtaW5cIikgIyBvcmRlcmVkIHRpbWUgcG9pbnRzXG5cbiMgaW1wb3J0IGFuZCBwcm9jZXNzIHRoZSBkYXRhIHRvIHRoZSBmb3JtYXQgd2Ugd2FudFxuZGF0YS5UcnVuVi5veGkgPC0gbWFwX2RmcihmaWxlcywgfnJlYWRfY3N2KC4sIG5hID0gYyhcIlwiLCBcIk5BXCIsIFwiTi9BXCIpLCBjb2xfdHlwZXMgPSBjb2xzKCkpLCAuaWQgPSBcIlJlcGxpY2F0ZVwiKSAlPiUgXG4gICNiaW5kX3Jvd3MoLmlkID0gXCJSZXBsaWNhdGVcIikgJT4lIFxuICBmaWx0ZXIoYFggUGFyYW1ldGVyYCA9PSBcIkJMMS1IXCIsIGlzLm5hKGBZIFBhcmFtZXRlcmApKSAlPiUgXG4gIHNlbGVjdChSZXBsaWNhdGUsIEdyb3VwLCBTYW1wbGUsIENvdW50LCBtZWRpYW4gPSBgWCBNZWRpYW5gLCBwZWFrID0gYFggUGVha2AsXG4gICAgICAgICBzZCA9IGBYIFNEYCwgY3YgPSBgWCAlQ1ZgLCByQ1YgPSBgWCAlckNWYCkgJT4lIFxuICBzZXBhcmF0ZShHcm91cCwgaW50byA9IGMoJ1RpbWUnLCAnVHJlYXRtZW50JyksIHNlcCA9IFwiLVwiKSAlPiUgXG4gIG11dGF0ZShUaW1lID0gb3JkZXJlZChUaW1lLCBsZXZlbHMgPSB0cCkpICU+JSBcbiAgbXV0YXRlKFNhbXBsZSA9IGNhc2Vfd2hlbihTYW1wbGUgPT0gXCJDVEExLUdGUC15SDI5OFwiIH4gXCJ5SDI5OC13dFwiLFxuICAgICAgICAgICAgU2FtcGxlID09IFwiQ1RBMS1HRlAteUgyOTlcIiB+IFwieUgyOTktd3RcIixcbiAgICAgICAgICAgIFNhbXBsZSA9PSBcInlIMzQzLXd0XCIgfiBcInlIMzQzLXJlc2N1ZVwiLFxuICAgICAgICAgICAgU2FtcGxlID09IFwieUgzNDQtd3RcIiB+IFwieUgzNDQtcmVzY3VlXCIsXG4gICAgICAgICAgICBUUlVFIH4gU2FtcGxlKSkgJT4lIFxuICBtdXRhdGUoUmVwbGljYXRlID0gZ3N1YihcIlxcXFwtLipcIixcIlwiLCBSZXBsaWNhdGUpKSAlPiUgIyBcbiAgc2VwYXJhdGUoU2FtcGxlLCBpbnRvID0gYyhcIlN0cmFpblwiLCBcImdlbm90eXBlXCIpLCBzZXAgPSBcIi1cIikgJT4lIFxuICBmaWx0ZXIoIWlzLm5hKG1lZGlhbikpICU+JSBcbiAgYXJyYW5nZShUaW1lKVxuIyBUbyByZXBsYWNlIHRoZSB2YWx1ZTogaWZlbHNlKCkgZm9yIGEgc2luZ2xlIHRlc3QsIGNhc2Vfd2hlbigpIGZvciBtdWx0aXBsZSB0ZXN0XG4jIFxcXFwtOiBlc2NhcGUgY2hhcmFjdGVyIFwiXFxcXFwiIHVzZWQgdG8gZXNjYXBlIHRoZSBzcGVjaWFsIG1lYW5pbmcgb2YgLSwgaW5zdGVhZCB0YWtlIC0gYXMgYSBjb21tb24gcmVnZXggcGF0dGVybi4gT3Igd2UgY2FuIHNwZWNpZnkgdGhlIC0gYXMgYSByZWdleCBwYXR0ZXJuIHdpdGhpbiBhIHNxdWFyZSBicmFja2V0IGNsYXNzIFstXVxuIy4qOiBUaGlzIHBhcnQgbWF0Y2hlcyBhbnkgc2VxdWVuY2Ugb2YgY2hhcmFjdGVycyAoLiogaXMgYSBjb21tb24gcmVnZXggcGF0dGVybiBmb3IgXCJhbnkgY2hhcmFjdGVyLCB6ZXJvIG9yIG1vcmUgdGltZXNcIikuIG1ldGFjaGFyYWN0ZXJcbmBgYCJ9 -->

```r
files <- dir("input/TrunV_2mMH2O2", pattern = "d*") # get the file names of the merged
files <- file.path("input//TrunV_2mMH2O2", files)      # this appends the directory to the file names
names(files) <- c("Rep1-2mMH2O2","Rep2-2mMH2O2", "Rep3-2mMH2O2")

tp <- c("0min",  "30min", "60min", "90min", "120min", "150min",  "180min", "210min", "240min") # ordered time points

# import and process the data to the format we want
data.TrunV.oxi <- map_dfr(files, ~read_csv(., na = c("", "NA", "N/A"), col_types = cols()), .id = "Replicate") %>% 
  #bind_rows(.id = "Replicate") %>% 
  filter(`X Parameter` == "BL1-H", is.na(`Y Parameter`)) %>% 
  select(Replicate, Group, Sample, Count, median = `X Median`, peak = `X Peak`,
         sd = `X SD`, cv = `X %CV`, rCV = `X %rCV`) %>% 
  separate(Group, into = c('Time', 'Treatment'), sep = "-") %>% 
  mutate(Time = ordered(Time, levels = tp)) %>% 
  mutate(Sample = case_when(Sample == "CTA1-GFP-yH298" ~ "yH298-wt",
            Sample == "CTA1-GFP-yH299" ~ "yH299-wt",
            Sample == "yH343-wt" ~ "yH343-rescue",
            Sample == "yH344-wt" ~ "yH344-rescue",
            TRUE ~ Sample)) %>% 
  mutate(Replicate = gsub("\\-.*","", Replicate)) %>% # 
  separate(Sample, into = c("Strain", "genotype"), sep = "-") %>% 
  filter(!is.na(median)) %>% 
  arrange(Time)
# To replace the value: ifelse() for a single test, case_when() for multiple test
# \\-: escape character "\\" used to escape the special meaning of -, instead take - as a common regex pattern. Or we can specify the - as a regex pattern within a square bracket class [-]
#.*: This part matches any sequence of characters (.* is a common regex pattern for "any character, zero or more times"). metacharacter
```

<!-- rnb-source-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->



#### under 2mM H2O2
Plot the Truncation variants data(TrunV)

<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuIyB1c2UgdGhlIHJlY29kZWQgdGhlIGdlbm90eXBlXG5cbm94aS5UcnVuVi5kYXQgPC0gZGF0YS5UcnVuVi5veGkgICU+JSBcbiAgZmlsdGVyKGdlbm90eXBlICVpbiUgYyhcInd0XCIsIFwiMlZcIiwgXCI0VlwiLCBcIjZWXCIsIFwiOFZcIixcInJlc2N1ZVwiKSkgJT4lICBcbiAgc2VsZWN0KFRpbWUsIHJlcGxpY2F0ZSA9IFJlcGxpY2F0ZSwgZ2Vub3R5cGUsIFN0cmFpbiwgbWVkaWFuKSAlPiVcbiAgbXV0YXRlKEdlbm90eXBlID0gZmN0X3JlY29kZShnZW5vdHlwZSwgISEhbGV2ZWxzKSkgJT4lIFxuICBtdXRhdGUobmV3X21lZGlhbiA9bWVkaWFuLzEwMDApICU+JSBcbiAgbXV0YXRlKG5ld190aW1lID0gYXMubnVtZXJpYyhnc3ViKFwibWluXCIsXCJcIixUaW1lKSkpJT4lIFxuICBhcnJhbmdlKG5ld190aW1lLCBnZW5vdHlwZSwgcmVwbGljYXRlKSAlPiUgXG4gIG11dGF0ZShHZW5vdHlwZSA9IGZhY3RvcihHZW5vdHlwZSwgbGV2ZWxzID0gRy5sZXZlbHMpKVxuXG5cbm94aS5UcnVuVi5kYXQgJT4lXG4gIGZpbHRlcighaXMubmEobmV3X21lZGlhbiksIGdlbm90eXBlICE9IFwicmVzY3VlXCIpICU+JSBcbiAgZ2dwbG90KGFlcyh4ID0gbmV3X3RpbWUsIHkgPSBuZXdfbWVkaWFuLCBjb2xvciA9IEdlbm90eXBlKSkgKyBwLnRpbWVjb3Vyc2UgK1xuICBzY2FsZV9jb2xvcl92aXJpZGlzX2QobGltaXRzID0gbmFtZXMobGV2ZWxzLm5vcmVzY3VlKSwgb3B0aW9uID0gXCJwbGFzbWFcIikgICtcbiAgeGxhYihcIjJtTSBIMk8yIHN0cmVzcywgdGltZSAobWluKVwiKVxuYGBgIn0= -->

```r
# use the recoded the genotype

oxi.TrunV.dat <- data.TrunV.oxi  %>% 
  filter(genotype %in% c("wt", "2V", "4V", "6V", "8V","rescue")) %>%  
  select(Time, replicate = Replicate, genotype, Strain, median) %>%
  mutate(Genotype = fct_recode(genotype, !!!levels)) %>% 
  mutate(new_median =median/1000) %>% 
  mutate(new_time = as.numeric(gsub("min","",Time)))%>% 
  arrange(new_time, genotype, replicate) %>% 
  mutate(Genotype = factor(Genotype, levels = G.levels))


oxi.TrunV.dat %>%
  filter(!is.na(new_median), genotype != "rescue") %>% 
  ggplot(aes(x = new_time, y = new_median, color = Genotype)) + p.timecourse +
  scale_color_viridis_d(limits = names(levels.norescue), option = "plasma")  +
  xlab("2mM H2O2 stress, time (min)")
```

<!-- rnb-source-end -->

<!-- rnb-plot-begin eyJoZWlnaHQiOjQzMi42MzI5LCJ3aWR0aCI6NzAwLCJzaXplX2JlaGF2aW9yIjowLCJjb25kaXRpb25zIjpbXX0= -->

<img src="data:image/png;base64,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" />

<!-- rnb-plot-end -->

<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuICAjc2NhbGVfeV9jb250aW51b3VzKGxpbWl0cyA9IGMoTkEsIDIyKSlcbiNnZ3NhdmUoXCJvdXRwdXQvVHJ1blZfb3hpX25vcmVzY3VlLnBuZ1wiLCB3aWR0aCA9IDYsIGhlaWdodCA9IDgpXG5gYGAifQ== -->

```r
  #scale_y_continuous(limits = c(NA, 22))
#ggsave("output/TrunV_oxi_norescue.png", width = 6, height = 8)
```

<!-- rnb-source-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->

## Basal expression level of Truncation variants

<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuIyBVc2UgMG1pbiBkYXRhIGZyb20gYm90aCBIMk8yIGFuZCAtUGkgdHJlYXRtZW50OyBcbmRhdGEuVHJ1blYgPC0gYmluZF9yb3dzKGRhdGEuVHJ1blYub3hpLGRhdGEuVHJ1blYucGkpICU+JSAgXG4gIHNlbGVjdChUaW1lLCByZXBsaWNhdGUgPSBSZXBsaWNhdGUsIGdlbm90eXBlLCBtZWRpYW4sIFRyZWF0bWVudCkgJT4lXG4gIG11dGF0ZShHZW5vdHlwZSA9IGZjdF9yZWNvZGUoZ2Vub3R5cGUsICEhIWxldmVscykpICU+JSBcbiAgbXV0YXRlKG5ld19tZWRpYW4gPW1lZGlhbi8xMDAwKSAlPiUgXG4gIG11dGF0ZShuZXdfdGltZSA9IGFzLm51bWVyaWMoZ3N1YihcIm1pblwiLFwiXCIsVGltZSkpKSU+JSBcbiAgYXJyYW5nZShuZXdfdGltZSwgZ2Vub3R5cGUsIHJlcGxpY2F0ZSkgJT4lIFxuICBtdXRhdGUoZ2Vub3R5cGUgPSBmYWN0b3IoZ2Vub3R5cGUsIGxldmVscyA9IGxldmVscykpICU+JSBcbiAgbXV0YXRlKEdlbm90eXBlID0gZmFjdG9yKEdlbm90eXBlLCBsZXZlbHMgPSBHLmxldmVscykpXG5cbiMgcGxvdCBXVCBjdXJ2ZSBhdCAtIFBpIGFuZCAybU0gSDJPMiBjb25kaXRpb25zXG5kYXRhLlRydW5WICU+JVxuICBmaWx0ZXIoIWlzLm5hKG5ld19tZWRpYW4pLCBHZW5vdHlwZSA9PSBcIldUXCIpICU+JSBcbiAgZ2dwbG90KGFlcyh4ID0gbmV3X3RpbWUsIHkgPSBuZXdfbWVkaWFuLCBjb2xvciA9IFRyZWF0bWVudCkpICsgcC50aW1lY291cnNlICtcbiAgc2NhbGVfY29sb3JfbWFudWFsKHZhbHVlcyA9IGMoXCIjOGU3Y2MzZmZcIixcIiNmNmIyNmJmZlwiKSkgICtcbiAgeGxhYihcIlRpbWUgKG1pbilcIilcbmBgYCJ9 -->

```r
# Use 0min data from both H2O2 and -Pi treatment; 
data.TrunV <- bind_rows(data.TrunV.oxi,data.TrunV.pi) %>%  
  select(Time, replicate = Replicate, genotype, median, Treatment) %>%
  mutate(Genotype = fct_recode(genotype, !!!levels)) %>% 
  mutate(new_median =median/1000) %>% 
  mutate(new_time = as.numeric(gsub("min","",Time)))%>% 
  arrange(new_time, genotype, replicate) %>% 
  mutate(genotype = factor(genotype, levels = levels)) %>% 
  mutate(Genotype = factor(Genotype, levels = G.levels))

# plot WT curve at - Pi and 2mM H2O2 conditions
data.TrunV %>%
  filter(!is.na(new_median), Genotype == "WT") %>% 
  ggplot(aes(x = new_time, y = new_median, color = Treatment)) + p.timecourse +
  scale_color_manual(values = c("#8e7cc3ff","#f6b26bff"))  +
  xlab("Time (min)")
```

<!-- rnb-source-end -->

<!-- rnb-plot-begin eyJoZWlnaHQiOjQzMi42MzI5LCJ3aWR0aCI6NzAwLCJzaXplX2JlaGF2aW9yIjowLCJjb25kaXRpb25zIjpbXX0= -->

<img src="data:image/png;base64,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" />

<!-- rnb-plot-end -->

<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuI2dnc2F2ZShcIm91dHB1dC9UcnVuVl9veGlfbm9yZXNjdWUucG5nXCIsIHdpZHRoID0gNiwgaGVpZ2h0ID0gOClcblxuXG5kYXRhLlRydW5WICU+JVxuICBmaWx0ZXIoIWlzLm5hKG5ld19tZWRpYW4pLCBnZW5vdHlwZSAhPSBcInJlc2N1ZVwiLCBUaW1lID09IFwiMG1pblwiKSAlPiUgXG4gIGdncGxvdChhZXMoeCA9IEdlbm90eXBlLCB5ID0gbmV3X21lZGlhbiwgY29sb3IgPSBHZW5vdHlwZSkpICsgYmFyLmxpc3QgK1xuICBnZW9tX2JveHBsb3QoKSArXG4gIHN0YXRfc3VtbWFyeShmdW4uZGF0YSA9IFwibWVhbl9jbF9ib290XCIsIGNvbG9yID0gXCJSZWRcIiwgbGluZXdpZHRoID0gMSwgc2l6ZSA9IDAuOCkgK1xuICBnZW9tX2ppdHRlcih3aWR0aCA9IDAuMikgK1xuICBzY2FsZV9jb2xvcl92aXJpZGlzX2QobGltaXRzID0gbmFtZXMobGV2ZWxzLm5vcmVzY3VlKSwgb3B0aW9uID0gXCJwbGFzbWFcIikgK1xuICB0aGVtZShsZWdlbmQucG9zaXRpb249XCJub25lXCIpICtcbiAgeGxhYihcIlRydW5jYXRpb24gVmFyaWFudHMsIDAgbWluXCIpXG5gYGAifQ== -->

```r
#ggsave("output/TrunV_oxi_norescue.png", width = 6, height = 8)


data.TrunV %>%
  filter(!is.na(new_median), genotype != "rescue", Time == "0min") %>% 
  ggplot(aes(x = Genotype, y = new_median, color = Genotype)) + bar.list +
  geom_boxplot() +
  stat_summary(fun.data = "mean_cl_boot", color = "Red", linewidth = 1, size = 0.8) +
  geom_jitter(width = 0.2) +
  scale_color_viridis_d(limits = names(levels.norescue), option = "plasma") +
  theme(legend.position="none") +
  xlab("Truncation Variants, 0 min")
```

<!-- rnb-source-end -->

<!-- rnb-plot-begin eyJoZWlnaHQiOjQzMi42MzI5LCJ3aWR0aCI6NzAwLCJzaXplX2JlaGF2aW9yIjowLCJjb25kaXRpb25zIjpbXX0= -->

<img src="data:image/png;base64,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" />

<!-- rnb-plot-end -->

<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuI2dnc2F2ZShcIm91dHB1dC9UcnVuVl9iYXNhbC5wbmdcIiwgd2lkdGggPSA2LCBoZWlnaHQgPSA4KVxuXG4jIyBzZXBlcmF0ZWx5IHBsb3QgdGhlIGJhc2FsIGxldmVsIGZvciAwbU0gUGkgYW5kIDJtTSBIMk8yXG5kYXRhLlRydW5WICU+JVxuICBmaWx0ZXIoIWlzLm5hKG5ld19tZWRpYW4pLCBnZW5vdHlwZSAhPSBcInJlc2N1ZVwiLCBUaW1lID09IFwiMG1pblwiKSAlPiUgXG4gIGdncGxvdChhZXMoeCA9IEdlbm90eXBlLCB5ID0gbmV3X21lZGlhbiwgY29sb3IgPSBHZW5vdHlwZSkpICsgYmFyLmxpc3QgK1xuICBnZW9tX2JveHBsb3QoKSArXG4gIHN0YXRfc3VtbWFyeShmdW4uZGF0YSA9IFwibWVhbl9jbF9ib290XCIsIGNvbG9yID0gXCJSZWRcIiwgbGluZXdpZHRoID0gMSwgc2l6ZSA9IDAuOCkgK1xuICBnZW9tX2ppdHRlcih3aWR0aCA9IDAuMikgK1xuICBzY2FsZV9jb2xvcl92aXJpZGlzX2QobGltaXRzID0gbmFtZXMobGV2ZWxzLm5vcmVzY3VlKSwgb3B0aW9uID0gXCJwbGFzbWFcIikgK1xuICB0aGVtZShsZWdlbmQucG9zaXRpb249YygwLjg1LDAuOSkpICtcbiAgeGxhYihcIlRydW5jYXRpb24gVmFyaWFudHMsIDAgbWluXCIpICtcbiAgZmFjZXRfZ3JpZCguIH4gVHJlYXRtZW50KSArXG4gIHRoZW1lKHN0cmlwLmJhY2tncm91bmQgPSBlbGVtZW50X3JlY3QoY29sb3VyPVwiYmxhY2tcIiwgZmlsbD1cIndoaXRlXCIsIHNpemU9MSwgbGluZXR5cGU9XCJzb2xpZFwiKSwgbGVnZW5kLnBvc2l0aW9uID0gXCJub25lXCIpXG5gYGAifQ== -->

```r
#ggsave("output/TrunV_basal.png", width = 6, height = 8)

## seperately plot the basal level for 0mM Pi and 2mM H2O2
data.TrunV %>%
  filter(!is.na(new_median), genotype != "rescue", Time == "0min") %>% 
  ggplot(aes(x = Genotype, y = new_median, color = Genotype)) + bar.list +
  geom_boxplot() +
  stat_summary(fun.data = "mean_cl_boot", color = "Red", linewidth = 1, size = 0.8) +
  geom_jitter(width = 0.2) +
  scale_color_viridis_d(limits = names(levels.norescue), option = "plasma") +
  theme(legend.position=c(0.85,0.9)) +
  xlab("Truncation Variants, 0 min") +
  facet_grid(. ~ Treatment) +
  theme(strip.background = element_rect(colour="black", fill="white", size=1, linetype="solid"), legend.position = "none")
```

<!-- rnb-source-end -->

<!-- rnb-plot-begin eyJoZWlnaHQiOjQzMi42MzI5LCJ3aWR0aCI6NzAwLCJzaXplX2JlaGF2aW9yIjowLCJjb25kaXRpb25zIjpbXX0= -->

<img src="data:image/png;base64,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" />

<!-- rnb-plot-end -->

<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuI2dnc2F2ZShcIm91dHB1dC9UcnVuVl9zZXBlcmF0ZV9iYXNhbC5wbmdcIiwgd2lkdGggPSA2LCBoZWlnaHQgPSA4KVxuXG5gYGAifQ== -->

```r
#ggsave("output/TrunV_seperate_basal.png", width = 6, height = 8)

```

<!-- rnb-source-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->




## Plateau/maximum expression Level of Truncation variants (V1)
The logic is cancel out the impact of basal expression level of each variants. To do so, minus the 0 min basal expression level from each variants, then plot the deduced data at all tp and the selected tp.

<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuIyBnZXQgdGhlIGluZGl2aWR1YWwgYmFzYWwgbWVhblxuZGF0YS5UcnVuVi5waS5iYXNhbCA8LSBkYXRhLlRydW5WLnBpICU+JSBmaWx0ZXIoIWlzLm5hKG1lZGlhbiksIFRpbWUgPT0gXCIwbWluXCIpICU+JSBncm91cF9ieShnZW5vdHlwZSkgJT4lIG11dGF0ZShiYXNhbCA9IG1lZGlhbikgJT4lIHNlbGVjdChSZXBsaWNhdGUsIFN0cmFpbiwgZ2Vub3R5cGUsIGJhc2FsKVxuXG5kYXRhLlRydW5WLm94aS5iYXNhbCA8LSBkYXRhLlRydW5WLm94aSAlPiUgZmlsdGVyKCFpcy5uYShtZWRpYW4pLCBUaW1lID09IFwiMG1pblwiKSAlPiUgZ3JvdXBfYnkoZ2Vub3R5cGUpICU+JSBtdXRhdGUoYmFzYWwgPSBtZWRpYW4pICU+JSBzZWxlY3QoUmVwbGljYXRlLCBTdHJhaW4sIGdlbm90eXBlLCBiYXNhbClcblxuXG5waS5UcnVuVi5kZWN0IDwtIG1lcmdlKGRhdGEuVHJ1blYucGksIGRhdGEuVHJ1blYucGkuYmFzYWwsIGJ5ID0gYyhcIlN0cmFpblwiLCBcIlJlcGxpY2F0ZVwiLFwiZ2Vub3R5cGVcIikpICU+JSBcbiAgZmlsdGVyKGdlbm90eXBlICVpbiUgYyhcInd0XCIsIFwiMlZcIiwgXCI0VlwiLCBcIjZWXCIsIFwiOFZcIiwgXCJyZXNjdWVcIikpICU+JSAgXG4gIHNlbGVjdChUaW1lLCByZXBsaWNhdGUgPSBSZXBsaWNhdGUsIGdlbm90eXBlLCBtZWRpYW4sIGJhc2FsKSAlPiVcbiAgbXV0YXRlKEdlbm90eXBlID0gZmN0X3JlY29kZShnZW5vdHlwZSwgISEhbGV2ZWxzKSkgJT4lIFxuICBtdXRhdGUobmV3X21lZGlhbiA9KG1lZGlhbi1iYXNhbCkvMTAwMCkgJT4lIFxuICBtdXRhdGUobmV3X3RpbWUgPSBhcy5udW1lcmljKGdzdWIoXCJtaW5cIixcIlwiLFRpbWUpKSklPiUgXG4gIG11dGF0ZShnZW5vdHlwZSA9IGZhY3RvcihnZW5vdHlwZSwgbGV2ZWxzID0gbGV2ZWxzKSkgJT4lIFxuICBhcnJhbmdlKG5ld190aW1lLCBnZW5vdHlwZSwgcmVwbGljYXRlKVxuXG5veGkuVHJ1blYuZGVjdCA8LSBtZXJnZShkYXRhLlRydW5WLm94aSwgZGF0YS5UcnVuVi5veGkuYmFzYWwsIGJ5ID0gYyhcIlN0cmFpblwiLCBcIlJlcGxpY2F0ZVwiLFwiZ2Vub3R5cGVcIikpICU+JSBcbiAgZmlsdGVyKGdlbm90eXBlICVpbiUgYyhcInd0XCIsIFwiMlZcIiwgXCI0VlwiLCBcIjZWXCIsIFwiOFZcIiwgXCJyZXNjdWVcIikpICU+JSAgXG4gIHNlbGVjdChUaW1lLCByZXBsaWNhdGUgPSBSZXBsaWNhdGUsIGdlbm90eXBlLCBtZWRpYW4sIGJhc2FsKSAlPiVcbiAgbXV0YXRlKEdlbm90eXBlID0gZmN0X3JlY29kZShnZW5vdHlwZSwgISEhbGV2ZWxzKSkgJT4lIFxuICBtdXRhdGUobmV3X21lZGlhbiA9KG1lZGlhbi1iYXNhbCkvMTAwMCkgJT4lIFxuICBtdXRhdGUobmV3X3RpbWUgPSBhcy5udW1lcmljKGdzdWIoXCJtaW5cIixcIlwiLFRpbWUpKSklPiUgXG4gIG11dGF0ZShnZW5vdHlwZSA9IGZhY3RvcihnZW5vdHlwZSwgbGV2ZWxzID0gbGV2ZWxzKSkgJT4lIFxuICBhcnJhbmdlKG5ld190aW1lLCBnZW5vdHlwZSwgcmVwbGljYXRlKVxuXG4jIHRpbWVjb3Vyc2UgZGVkdWN0IGN1cnZlXG5waS5UcnVuVi5kZWN0ICU+JVxuICBmaWx0ZXIoIWlzLm5hKG5ld19tZWRpYW4pLCBnZW5vdHlwZSAhPSBcInJlc2N1ZVwiKSAlPiUgXG4gIGdncGxvdChhZXMoeCA9IG5ld190aW1lLCB5ID0gbmV3X21lZGlhbiwgY29sb3IgPSBHZW5vdHlwZSkpICsgcC50aW1lY291cnNlICtcbiAgc2NhbGVfY29sb3JfdmlyaWRpc19kKGxpbWl0cyA9IG5hbWVzKGxldmVscy5ub3Jlc2N1ZSksIG9wdGlvbiA9IFwicGxhc21hXCIpICArXG4gIGxhYnMoeCA9IFwiUGhvc3BoYXRlIHN0YXJ2YXRpb24sIFRpbWUgKG1pbilcIilcbmBgYCJ9 -->

```r
# get the individual basal mean
data.TrunV.pi.basal <- data.TrunV.pi %>% filter(!is.na(median), Time == "0min") %>% group_by(genotype) %>% mutate(basal = median) %>% select(Replicate, Strain, genotype, basal)

data.TrunV.oxi.basal <- data.TrunV.oxi %>% filter(!is.na(median), Time == "0min") %>% group_by(genotype) %>% mutate(basal = median) %>% select(Replicate, Strain, genotype, basal)


pi.TrunV.dect <- merge(data.TrunV.pi, data.TrunV.pi.basal, by = c("Strain", "Replicate","genotype")) %>% 
  filter(genotype %in% c("wt", "2V", "4V", "6V", "8V", "rescue")) %>%  
  select(Time, replicate = Replicate, genotype, median, basal) %>%
  mutate(Genotype = fct_recode(genotype, !!!levels)) %>% 
  mutate(new_median =(median-basal)/1000) %>% 
  mutate(new_time = as.numeric(gsub("min","",Time)))%>% 
  mutate(genotype = factor(genotype, levels = levels)) %>% 
  arrange(new_time, genotype, replicate)

oxi.TrunV.dect <- merge(data.TrunV.oxi, data.TrunV.oxi.basal, by = c("Strain", "Replicate","genotype")) %>% 
  filter(genotype %in% c("wt", "2V", "4V", "6V", "8V", "rescue")) %>%  
  select(Time, replicate = Replicate, genotype, median, basal) %>%
  mutate(Genotype = fct_recode(genotype, !!!levels)) %>% 
  mutate(new_median =(median-basal)/1000) %>% 
  mutate(new_time = as.numeric(gsub("min","",Time)))%>% 
  mutate(genotype = factor(genotype, levels = levels)) %>% 
  arrange(new_time, genotype, replicate)

# timecourse deduct curve
pi.TrunV.dect %>%
  filter(!is.na(new_median), genotype != "rescue") %>% 
  ggplot(aes(x = new_time, y = new_median, color = Genotype)) + p.timecourse +
  scale_color_viridis_d(limits = names(levels.norescue), option = "plasma")  +
  labs(x = "Phosphate starvation, Time (min)")
```

<!-- rnb-source-end -->

<!-- rnb-plot-begin eyJoZWlnaHQiOjQzMi42MzI5LCJ3aWR0aCI6NzAwLCJzaXplX2JlaGF2aW9yIjowLCJjb25kaXRpb25zIjpbXX0= -->

<img src="data:image/png;base64,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" />

<!-- rnb-plot-end -->

<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuI2dnc2F2ZShcIm91dHB1dC9UcnVuVl8wUGlfZGVkdWN0LnBuZ1wiLCB3aWR0aCA9IDYsIGhlaWdodCA9IDgpXG5cbm94aS5UcnVuVi5kZWN0ICU+JVxuICBmaWx0ZXIoIWlzLm5hKG5ld19tZWRpYW4pLCBnZW5vdHlwZSAhPSBcInJlc2N1ZVwiKSAlPiUgXG4gIGdncGxvdChhZXMoeCA9IG5ld190aW1lLCB5ID0gbmV3X21lZGlhbiwgY29sb3IgPSBHZW5vdHlwZSkpICsgcC50aW1lY291cnNlICtcbiAgc2NhbGVfY29sb3JfdmlyaWRpc19kKGxpbWl0cyA9IG5hbWVzKGxldmVscy5ub3Jlc2N1ZSksIG9wdGlvbiA9IFwicGxhc21hXCIpICArXG4gIGxhYnMoeCA9IFwiMm1NIEgyTzIsIFRpbWUgKG1pbilcIilcbmBgYCJ9 -->

```r
#ggsave("output/TrunV_0Pi_deduct.png", width = 6, height = 8)

oxi.TrunV.dect %>%
  filter(!is.na(new_median), genotype != "rescue") %>% 
  ggplot(aes(x = new_time, y = new_median, color = Genotype)) + p.timecourse +
  scale_color_viridis_d(limits = names(levels.norescue), option = "plasma")  +
  labs(x = "2mM H2O2, Time (min)")
```

<!-- rnb-source-end -->

<!-- rnb-plot-begin eyJoZWlnaHQiOjQzMi42MzI5LCJ3aWR0aCI6NzAwLCJzaXplX2JlaGF2aW9yIjowLCJjb25kaXRpb25zIjpbXX0= -->

<img src="data:image/png;base64,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" />

<!-- rnb-plot-end -->

<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuI2dnc2F2ZShcIm91dHB1dC9UcnVuVl9veGlfZGVkdWN0LnBuZ1wiLCB3aWR0aCA9IDYsIGhlaWdodCA9IDgpXG5cblxuIyBzaW5nbGUgdGltZXBvaW50IGRlZHVjdCBjdXJ2ZVxuIyAtIFBpOiAyNDBtaW5cbnBpLlRydW5WLmRlY3QgJT4lIFxuICBmaWx0ZXIoIWlzLm5hKG5ld19tZWRpYW4pLCBnZW5vdHlwZSAhPSBcInJlc2N1ZVwiLCBUaW1lID09IFwiMjQwbWluXCIpICU+JSBcbiAgZ2dwbG90KGFlcyh4ID0gZ2Vub3R5cGUsIHkgPSBuZXdfbWVkaWFuLCBjb2xvciA9IEdlbm90eXBlKSkgKyBiYXIubGlzdCArXG4gIGdlb21fYm94cGxvdCgpICtcbiAgc3RhdF9zdW1tYXJ5KGZ1bi5kYXRhID0gXCJtZWFuX2NsX2Jvb3RcIiwgY29sb3IgPSBcIlJlZFwiLCBsaW5ld2lkdGggPSAxLCBzaXplID0gMC44KSArXG4gIGdlb21faml0dGVyKHdpZHRoID0gMC4yKSArXG4gIHRoZW1lKGxlZ2VuZC5wb3NpdGlvbj1jKDAuODUsMC45KSkgK1xuICBzY2FsZV9jb2xvcl92aXJpZGlzX2QobGltaXRzID0gbmFtZXMobGV2ZWxzLm5vcmVzY3VlKSwgb3B0aW9uID0gXCJwbGFzbWFcIikgK1xuICB4bGFiKFwiVHJ1bmNhdGlvbiBWYXJpYW50cywgMG1NIFBpLCAyNDAgbWluXCIpXG5gYGAifQ== -->

```r
#ggsave("output/TrunV_oxi_deduct.png", width = 6, height = 8)


# single timepoint deduct curve
# - Pi: 240min
pi.TrunV.dect %>% 
  filter(!is.na(new_median), genotype != "rescue", Time == "240min") %>% 
  ggplot(aes(x = genotype, y = new_median, color = Genotype)) + bar.list +
  geom_boxplot() +
  stat_summary(fun.data = "mean_cl_boot", color = "Red", linewidth = 1, size = 0.8) +
  geom_jitter(width = 0.2) +
  theme(legend.position=c(0.85,0.9)) +
  scale_color_viridis_d(limits = names(levels.norescue), option = "plasma") +
  xlab("Truncation Variants, 0mM Pi, 240 min")
```

<!-- rnb-source-end -->

<!-- rnb-plot-begin eyJoZWlnaHQiOjQzMi42MzI5LCJ3aWR0aCI6NzAwLCJzaXplX2JlaGF2aW9yIjowLCJjb25kaXRpb25zIjpbXX0= -->

<img src="data:image/png;base64,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" />

<!-- rnb-plot-end -->

<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuI2dnc2F2ZShcIm91dHB1dC9UcnVuVl9kZWR1Y3RfMFBpXzI0MC5wbmdcIiwgd2lkdGggPSA2LCBoZWlnaHQgPSA4KVxuXG4jIDJtTSBPeGk6IDkwbWluXG5veGkuVHJ1blYuZGVjdCAlPiUgXG4gIGZpbHRlcighaXMubmEobmV3X21lZGlhbiksIGdlbm90eXBlICE9IFwicmVzY3VlXCIsIFRpbWUgPT0gXCI5MG1pblwiKSAlPiUgXG4gIGdncGxvdChhZXMoeCA9IGdlbm90eXBlLCB5ID0gbmV3X21lZGlhbiwgY29sb3IgPSBHZW5vdHlwZSkpICsgYmFyLmxpc3QgK1xuICBnZW9tX2JveHBsb3QoKSArXG4gIHN0YXRfc3VtbWFyeShmdW4uZGF0YSA9IFwibWVhbl9jbF9ib290XCIsIGNvbG9yID0gXCJSZWRcIiwgbGluZXdpZHRoID0gMSwgc2l6ZSA9IDAuOCkgK1xuICBnZW9tX2ppdHRlcih3aWR0aCA9IDAuMikgK1xuICB0aGVtZShsZWdlbmQucG9zaXRpb249YygwLjg1LDAuOSkpICtcbiAgc2NhbGVfY29sb3JfdmlyaWRpc19kKGxpbWl0cyA9IG5hbWVzKGxldmVscy5ub3Jlc2N1ZSksIG9wdGlvbiA9IFwicGxhc21hXCIpICtcbiAgeGxhYihcIlRydW5jYXRpb24gVmFyaWFudHMsIDJtTSBIMk8yLCA5MCBtaW5cIilcbmBgYCJ9 -->

```r
#ggsave("output/TrunV_deduct_0Pi_240.png", width = 6, height = 8)

# 2mM Oxi: 90min
oxi.TrunV.dect %>% 
  filter(!is.na(new_median), genotype != "rescue", Time == "90min") %>% 
  ggplot(aes(x = genotype, y = new_median, color = Genotype)) + bar.list +
  geom_boxplot() +
  stat_summary(fun.data = "mean_cl_boot", color = "Red", linewidth = 1, size = 0.8) +
  geom_jitter(width = 0.2) +
  theme(legend.position=c(0.85,0.9)) +
  scale_color_viridis_d(limits = names(levels.norescue), option = "plasma") +
  xlab("Truncation Variants, 2mM H2O2, 90 min")
```

<!-- rnb-source-end -->

<!-- rnb-plot-begin eyJoZWlnaHQiOjQzMi42MzI5LCJ3aWR0aCI6NzAwLCJzaXplX2JlaGF2aW9yIjowLCJjb25kaXRpb25zIjpbXX0= -->

<img src="data:image/png;base64,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" />

<!-- rnb-plot-end -->

<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuI2dnc2F2ZShcIm91dHB1dC9UcnVuVl9kZWR1Y3RfT3hpXzkwLnBuZ1wiLCB3aWR0aCA9IDYsIGhlaWdodCA9IDgpXG5cbiMgY2FsY3VsYXRlIG1heGltdW0gcGxhdGVhdSByZWxhdGl2ZSB0byB3dFxucGkuVHJ1blYuZGVjdC5yZWwgPC0gcGkuVHJ1blYuZGVjdCAlPiUgZmlsdGVyKFRpbWUgPT0gXCIyNDBtaW5cIikgJT4lIGdyb3VwX2J5KGdlbm90eXBlKSAlPiUgXG4gIG11dGF0ZShuZXdfbWVhbl9vcmkgPSBtZWFuKG1lZGlhbikpICU+JSBcbiAgbXV0YXRlKG5ld19tZWFuX3JlZCA9IG1lYW4obmV3X21lZGlhbikpICU+JSBcbiAgbXV0YXRlKHd0X29yaSA9IG1lYW4oLlsuJEdlbm90eXBlID09IFwiV1RcIixdJG5ld19tZWFuX29yaSkpICU+JSBcbiAgbXV0YXRlKHd0X3JlZCA9IG1lYW4oLlsuJEdlbm90eXBlID09IFwiV1RcIixdJG5ld19tZWFuX3JlZCkpICU+JSBcbiAgbXV0YXRlKHJlbF9vcmkgPSBtZWRpYW4vd3Rfb3JpKSAlPiUgXG4gIG11dGF0ZShyZWxfcmVkID0gbmV3X21lZGlhbi93dF9yZWQpICU+JSBcbiAgbXV0YXRlKFRyZWF0bWVudCA9IFwiMFBpXCIpXG4gIFxub3hpLlRydW5WLmRlY3QucmVsIDwtIG94aS5UcnVuVi5kZWN0ICU+JSBmaWx0ZXIoVGltZSA9PSBcIjkwbWluXCIpICU+JSBncm91cF9ieShnZW5vdHlwZSkgJT4lIFxuICBtdXRhdGUobmV3X21lYW5fb3JpID0gbWVhbihtZWRpYW4pKSAlPiUgXG4gIG11dGF0ZShuZXdfbWVhbl9yZWQgPSBtZWFuKG5ld19tZWRpYW4pKSAlPiUgXG4gIG11dGF0ZSh3dF9vcmkgPSBtZWFuKC5bLiRHZW5vdHlwZSA9PSBcIldUXCIsXSRuZXdfbWVhbl9vcmkpKSAlPiUgXG4gIG11dGF0ZSh3dF9yZWQgPSBtZWFuKC5bLiRHZW5vdHlwZSA9PSBcIldUXCIsXSRuZXdfbWVhbl9yZWQpKSAlPiUgXG4gIG11dGF0ZShyZWxfb3JpID0gbWVkaWFuL3d0X29yaSkgJT4lIFxuICBtdXRhdGUocmVsX3JlZCA9IG5ld19tZWRpYW4vd3RfcmVkKSAlPiUgXG4gIG11dGF0ZShUcmVhdG1lbnQgPSBcIjJtTUgyTzJcIilcblxuVHJ1blYucmVsIDwtIGJpbmRfcm93cyhwaS5UcnVuVi5kZWN0LnJlbCwgb3hpLlRydW5WLmRlY3QucmVsKSAlPiUgbXV0YXRlKEdlbm90eXBlID0gZmFjdG9yKEdlbm90eXBlLCBsZXZlbHMgPSBHLmxldmVscykpXG5cbiMgcGxvdCB0aGUgbWF4aW11bSByZWxhdGl2ZSB0byB3dFxuVHJ1blYucmVsICU+JSBcbiAgZmlsdGVyKCFpcy5uYShuZXdfbWVkaWFuKSwgZ2Vub3R5cGUgIT0gXCJyZXNjdWVcIikgJT4lIFxuICBnZ3Bsb3QoYWVzKHggPSBHZW5vdHlwZSwgeSA9IHJlbF9vcmksIGZpbGwgPSBUcmVhdG1lbnQsIHBhdHRlcm4gPSBUcmVhdG1lbnQpKSArIGJhci5saXN0Lm5vLnN0YXQgK1xuICBnZW9tX2Jhcl9wYXR0ZXJuKHN0YXQgPSBcInN1bW1hcnlcIiwgZnVuID0gXCJtZWFuXCIsXG4gICAgICAgICAgICAgICAgICAgcG9zaXRpb24gPSBwb3NpdGlvbl9kb2RnZShwcmVzZXJ2ZSA9IFwic2luZ2xlXCIpLFxuICAgICAgICAgICAgICAgICAgIGNvbG9yID0gXCJibGFja1wiLCBcbiAgICAgICAgICAgICAgICAgICBwYXR0ZXJuX2ZpbGwgPSBcImJsYWNrXCIsXG4gICAgICAgICAgICAgICAgICAgcGF0dGVybl9hbmdsZSA9IDQ1LFxuICAgICAgICAgICAgICAgICAgIHBhdHRlcm5fZGVuc2l0eSA9IDAuMSwgICMgMC4xXG4gICAgICAgICAgICAgICAgICAgcGF0dGVybl9zcGFjaW5nID0gMC4wNCwgICMgMC4wMjVcbiAgICAgICAgICAgICAgICAgICBwYXR0ZXJuX2tleV9zY2FsZV9mYWN0b3IgPSAxLFxuICAgICAgICAgICAgICAgICAgIHdpZHRoPTAuOCkgKyBcbiAgc2NhbGVfZmlsbF9tYW51YWwodmFsdWVzID0gYyhcIiNiNGE3ZDZmZlwiLFwiI2Y2YjI2YmZmXCIpKSArXG4gIHNjYWxlX3BhdHRlcm5fbWFudWFsKHZhbHVlcyA9IGMoYDBQaWAgPSBcInN0cmlwZVwiLCBgMm1NSDJPMmAgPSBcIm5vbmVcIikpICtcbiAgZ2VvbV9lcnJvcmJhcihzdGF0ID0gXCJzdW1tYXJ5XCIsIGZ1bi5kYXRhID0gbWVhbl9jbF9ib290LCB3aWR0aCA9IDAuMiwgY29sb3IgPSBcIlJlZFwiLCBsaW5ld2lkdGggPSAxLCBwb3NpdGlvbiA9IFxuICAgICAgICAgICAgICAgICAgcG9zaXRpb25fZG9kZ2Uod2lkdGggPSAuOSkpICtcbiAgc2NhbGVfeV9jb250aW51b3VzKGxpbWl0cyA9IGMoMCwgMS41KSkgK1xuICAjZ2VvbV9qaXR0ZXIod2lkdGggPSAwLjMpICtcbiAgZ2VvbV9obGluZSh5aW50ZXJjZXB0ID0gMSwgY29sID0gXCJncmF5XCIsIGxpbmV0eXBlID0gXCJkYXNoZWRcIikgK1xuICB4bGFiKFwiSW50ZXJuYWwgcmVtb3ZhbCAoSVIpIHZhcmlhbnRzXCIpICtcbiAgeWxhYihcIk1heCBpbmR1Y3Rpb24gKHJlbGF0aXZlIHRvIHd0LG9yaSlcIikgK1xuICBndWlkZXMoZmlsbCA9IGd1aWRlX2xlZ2VuZChucm93ID0gMSkpICtcbiAgdGhlbWUoc3RyaXAuYmFja2dyb3VuZCA9IGVsZW1lbnRfcmVjdChjb2xvdXI9XCJibGFja1wiLCBmaWxsPVwid2hpdGVcIiwgc2l6ZT0xLCBsaW5ldHlwZT1cInNvbGlkXCIpKVxuYGBgIn0= -->

```r
#ggsave("output/TrunV_deduct_Oxi_90.png", width = 6, height = 8)

# calculate maximum plateau relative to wt
pi.TrunV.dect.rel <- pi.TrunV.dect %>% filter(Time == "240min") %>% group_by(genotype) %>% 
  mutate(new_mean_ori = mean(median)) %>% 
  mutate(new_mean_red = mean(new_median)) %>% 
  mutate(wt_ori = mean(.[.$Genotype == "WT",]$new_mean_ori)) %>% 
  mutate(wt_red = mean(.[.$Genotype == "WT",]$new_mean_red)) %>% 
  mutate(rel_ori = median/wt_ori) %>% 
  mutate(rel_red = new_median/wt_red) %>% 
  mutate(Treatment = "0Pi")
  
oxi.TrunV.dect.rel <- oxi.TrunV.dect %>% filter(Time == "90min") %>% group_by(genotype) %>% 
  mutate(new_mean_ori = mean(median)) %>% 
  mutate(new_mean_red = mean(new_median)) %>% 
  mutate(wt_ori = mean(.[.$Genotype == "WT",]$new_mean_ori)) %>% 
  mutate(wt_red = mean(.[.$Genotype == "WT",]$new_mean_red)) %>% 
  mutate(rel_ori = median/wt_ori) %>% 
  mutate(rel_red = new_median/wt_red) %>% 
  mutate(Treatment = "2mMH2O2")

TrunV.rel <- bind_rows(pi.TrunV.dect.rel, oxi.TrunV.dect.rel) %>% mutate(Genotype = factor(Genotype, levels = G.levels))

# plot the maximum relative to wt
TrunV.rel %>% 
  filter(!is.na(new_median), genotype != "rescue") %>% 
  ggplot(aes(x = Genotype, y = rel_ori, fill = Treatment, pattern = Treatment)) + bar.list.no.stat +
  geom_bar_pattern(stat = "summary", fun = "mean",
                   position = position_dodge(preserve = "single"),
                   color = "black", 
                   pattern_fill = "black",
                   pattern_angle = 45,
                   pattern_density = 0.1,  # 0.1
                   pattern_spacing = 0.04,  # 0.025
                   pattern_key_scale_factor = 1,
                   width=0.8) + 
  scale_fill_manual(values = c("#b4a7d6ff","#f6b26bff")) +
  scale_pattern_manual(values = c(`0Pi` = "stripe", `2mMH2O2` = "none")) +
  geom_errorbar(stat = "summary", fun.data = mean_cl_boot, width = 0.2, color = "Red", linewidth = 1, position = 
                  position_dodge(width = .9)) +
  scale_y_continuous(limits = c(0, 1.5)) +
  #geom_jitter(width = 0.3) +
  geom_hline(yintercept = 1, col = "gray", linetype = "dashed") +
  xlab("Internal removal (IR) variants") +
  ylab("Max induction (relative to wt,ori)") +
  guides(fill = guide_legend(nrow = 1)) +
  theme(strip.background = element_rect(colour="black", fill="white", size=1, linetype="solid"))
```

<!-- rnb-source-end -->

<!-- rnb-plot-begin eyJoZWlnaHQiOjQzMi42MzI5LCJ3aWR0aCI6NzAwLCJzaXplX2JlaGF2aW9yIjowLCJjb25kaXRpb25zIjpbXX0= -->

<img src="data:image/png;base64,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" />

<!-- rnb-plot-end -->

<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuI2dnc2F2ZShcIm91dHB1dC9UcnVuVl9vcmlfcmVsX21heC5wbmdcIiwgd2lkdGggPSAxMC4xNiwgaGVpZ2h0ID0gMilcblxuXG5cblRydW5WLnJlbCAlPiUgXG4gIGZpbHRlcighaXMubmEobmV3X21lZGlhbiksIGdlbm90eXBlICE9IFwicmVzY3VlXCIpICU+JSBcbiAgZ2dwbG90KGFlcyh4ID0gR2Vub3R5cGUsIHkgPSByZWxfcmVkLCBmaWxsID0gVHJlYXRtZW50LCBwYXR0ZXJuID0gVHJlYXRtZW50KSkgKyBiYXIubGlzdC5uby5zdGF0ICtcbiAgZ2VvbV9iYXJfcGF0dGVybihzdGF0ID0gXCJzdW1tYXJ5XCIsIGZ1biA9IFwibWVhblwiLFxuICAgICAgICAgICAgICAgICAgIHBvc2l0aW9uID0gcG9zaXRpb25fZG9kZ2UocHJlc2VydmUgPSBcInNpbmdsZVwiKSxcbiAgICAgICAgICAgICAgICAgICBjb2xvciA9IFwiYmxhY2tcIiwgXG4gICAgICAgICAgICAgICAgICAgcGF0dGVybl9maWxsID0gXCJibGFja1wiLFxuICAgICAgICAgICAgICAgICAgIHBhdHRlcm5fYW5nbGUgPSA0NSxcbiAgICAgICAgICAgICAgICAgICBwYXR0ZXJuX2RlbnNpdHkgPSAwLjEsICAjIDAuMVxuICAgICAgICAgICAgICAgICAgIHBhdHRlcm5fc3BhY2luZyA9IDAuMDQsICAjIDAuMDI1XG4gICAgICAgICAgICAgICAgICAgcGF0dGVybl9rZXlfc2NhbGVfZmFjdG9yID0gMSxcbiAgICAgICAgICAgICAgICAgICB3aWR0aD0wLjgpICsgXG4gIHNjYWxlX2ZpbGxfbWFudWFsKHZhbHVlcyA9IGMoXCIjYjRhN2Q2ZmZcIixcIiNmNmIyNmJmZlwiKSkgK1xuICBzY2FsZV9wYXR0ZXJuX21hbnVhbCh2YWx1ZXMgPSBjKGAwUGlgID0gXCJzdHJpcGVcIiwgYDJtTUgyTzJgID0gXCJub25lXCIpKSArXG4gIGdlb21fZXJyb3JiYXIoc3RhdCA9IFwic3VtbWFyeVwiLCBmdW4uZGF0YSA9IG1lYW5fY2xfYm9vdCwgd2lkdGggPSAwLjIsIGNvbG9yID0gXCJSZWRcIiwgbGluZXdpZHRoID0gMSwgcG9zaXRpb24gPSBcbiAgICAgICAgICAgICAgICAgIHBvc2l0aW9uX2RvZGdlKHdpZHRoID0gLjkpKSArXG4gIHNjYWxlX3lfY29udGludW91cyhsaW1pdHMgPSBjKDAsIDEuNSkpICtcbiAgI2dlb21faml0dGVyKHdpZHRoID0gMC4zKSArXG4gIGdlb21faGxpbmUoeWludGVyY2VwdCA9IDEsIGNvbCA9IFwiZ3JheVwiLCBsaW5ldHlwZSA9IFwiZGFzaGVkXCIpICtcbiAgeGxhYihcIkludGVybmFsIHJlbW92YWwgKElSKSB2YXJpYW50c1wiKSArXG4gIHlsYWIoXCJQbGF0ZWF1XCIpICtcbiAgZ3VpZGVzKGZpbGwgPSBndWlkZV9sZWdlbmQobnJvdyA9IDEpKSArXG4gIHRoZW1lKHN0cmlwLmJhY2tncm91bmQgPSBlbGVtZW50X3JlY3QoY29sb3VyPVwiYmxhY2tcIiwgZmlsbD1cIndoaXRlXCIsIHNpemU9MSwgbGluZXR5cGU9XCJzb2xpZFwiKSwgbGVnZW5kLnBvc2l0aW9uPWMoMC44LDAuOSkpXG5gYGAifQ== -->

```r
#ggsave("output/TrunV_ori_rel_max.png", width = 10.16, height = 2)



TrunV.rel %>% 
  filter(!is.na(new_median), genotype != "rescue") %>% 
  ggplot(aes(x = Genotype, y = rel_red, fill = Treatment, pattern = Treatment)) + bar.list.no.stat +
  geom_bar_pattern(stat = "summary", fun = "mean",
                   position = position_dodge(preserve = "single"),
                   color = "black", 
                   pattern_fill = "black",
                   pattern_angle = 45,
                   pattern_density = 0.1,  # 0.1
                   pattern_spacing = 0.04,  # 0.025
                   pattern_key_scale_factor = 1,
                   width=0.8) + 
  scale_fill_manual(values = c("#b4a7d6ff","#f6b26bff")) +
  scale_pattern_manual(values = c(`0Pi` = "stripe", `2mMH2O2` = "none")) +
  geom_errorbar(stat = "summary", fun.data = mean_cl_boot, width = 0.2, color = "Red", linewidth = 1, position = 
                  position_dodge(width = .9)) +
  scale_y_continuous(limits = c(0, 1.5)) +
  #geom_jitter(width = 0.3) +
  geom_hline(yintercept = 1, col = "gray", linetype = "dashed") +
  xlab("Internal removal (IR) variants") +
  ylab("Plateau") +
  guides(fill = guide_legend(nrow = 1)) +
  theme(strip.background = element_rect(colour="black", fill="white", size=1, linetype="solid"), legend.position=c(0.8,0.9))
```

<!-- rnb-source-end -->

<!-- rnb-plot-begin eyJoZWlnaHQiOjQzMi42MzI5LCJ3aWR0aCI6NzAwLCJzaXplX2JlaGF2aW9yIjowLCJjb25kaXRpb25zIjpbXX0= -->

<img src="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAArwAAAGwCAMAAAB8TkaXAAAA/1BMVEUAAAAAADoAAGYAOjoAOmYAOpAAZmYAZpAAZrYzMzM6AAA6ADo6AGY6OgA6Ojo6OmY6OpA6ZmY6ZpA6ZrY6kJA6kLY6kNtmAABmADpmAGZmOgBmOjpmZjpmZmZmZpBmkGZmkLZmkNtmtrZmtttmtv+QOgCQOjqQOmaQZgCQZjqQZmaQkGaQtpCQtraQ2/+0p9a2ZgC2Zjq2kDq2kGa2kJC2tpC2tra2ttu225C227a229u22/+2/7a2/9u2//++vr7bkDrbkGbbtmbbtpDbtrbbttvb25Db27bb29vb2//b/9vb///2smv/AAD/tmb/25D/27b/29v//7b//9v///8aWe51AAAACXBIWXMAAA7DAAAOwwHHb6hkAAAfO0lEQVR4nO2dC3vjNnaGIY/d2sqtyTRW6mSzno6VZpJ2okl2J9u4dbSeNJnEa9kj8f//lhLgDSQBEqBw4aG+93lmbFEUwMtr6hDAAVkCAFFY7A0AYCiQF5AF8gKyQF5AFsgLyAJ5AVkgLyAL5AVkcSIv/gJADCAvIAvkBWSBvIAskBeQBfICskBeQBbIC8gCeQFZIC8gC+QFZDHzbru4ql6smUBaAnlBDIy8217Iqq4gLxgFJt69mcuq7pYndwMKAcA1/d7tvmLH30rybhen9oUA4J5+77afXd5tJHkf5uf2hQDgHjPvZHk37PJzxj65zj8v8LFlYMRsWMlV54rvjIs0X7PEXt68sWH20rYQMB1M5f37+zeGJZqvWWEv74p9epfsXjEp8oW8h4jizr3F6shUSfM1K+zlzdgtpcog7yFCV95aZZD3ECnk3S1P1+zoOnl8kQaTl2LR7Qfi190yDStOk9XJHy/Y7FmyS1d4yt8v10yL+PVCvJWtaYm1vNuF2OTanx3kPUQqeZ/M2cndw1yEwNzA/LbovJT3a/7y+VIs5O1VxZpiBWlNS4bEvOlfz+OSSQ1mkPcQqeQVLhT3Qlfp9S29DicP/Convp9X7OSa93Sl/98yvrBcM/3o6V3q+mmAsGHNmxi2C/HHIsc7kPcQqeTl3j3MT7MX4sfb1998wEp5uTbZWvwz0prZwm2puSX28mYRy1M5Voe8h0glL/+ZxwLiqpb/XspbaFvIW65ZLfQob4hCADE08h7dpN/NH1/++NuiT96jG8gL4tCUt7wJyr6nt3p5z+tFQF4Qmrq8u+XsWfrjNg1oN/wu7PFChA080GzIK60pyyt32RoCecFA6vIWcUPqYH5Ln4YFvNHstCmvtKa0cO2tqSxEIYAYDXnFjXw2YCu96rInz/m1dMuvv015qzWlhWJNyy2AvIAskBeQBfICskBeQBbIC8gCeQFZIC8gC+QFZIG8gCyQF5AF8oIBMBXBPl4WY/8RT4UAQrDvmpxZyfuPNpAXhKEl7xk7g7yABE15U3e/g7yABKztLuQFNGBtdyEvoAFru1uXd/eKsU/44PJsApLZs9qzIXrlvZ2LjzRZFdkWK3bOEzac7IqLQgAhWNvdmrwiV211Ws5p92Zemy+sT94Ne548LlrzQO+WH2byPrz3xRXPJnKyKy4KAYRgbXdr8q7FPCTvvaxmB6uZ2CNvNnPJupVP/DD/U5YqtPr3f7tJNjPICwbA2u7K8m7FVfNhflVkxHN5V1WCZZ+8f+GZxJtU3s3RTy/Y8cvHCzZLL92b2X/+C5d38/SWp2weQV4wANZ2V5Z3I/LYubzZJEv8IixffE1u2LKE+OMvr3dfP/noOnkldP3b+yKX87mYKuoE8oIBsLa7srzZNz5XeCW+59/MT2vP8jORd12mxospHdZ8fp3T7Wfpr5uTX+dXIsHeya64KAQQgrXdleTNZ9tbi5mfOB8+L67G+cd75d294nGCED4rLf0rSIMRLm/6j5eVBiSQFwyAtd2tySsihDTIfahaGeT7r155d0uhuhBelMEfoJb+slumkcipKCt9D/KCAbC2uy15+WVzXV1uV/JDTHrk3V5kn1vzqKE0WEQOV7v/uBHX4vQV5AUDYG135ZhXiMrNW5Wz4NQay3rkzWanrjWZFfHz6nxzJRozeDgMecEAWNvdZmvDrbjhKi+3tWev98hbTLpXD3nFL6vzv9yJ4nkcAXnBAFjb3Vonxe2cHRfhasam9uC+Tnnzu7yjG97LkbUZc3FFYet/us6uxfwV5AUDYG13MTAH0IC13YW8gAbIYQNgLyAvIAvkBWSBvIAskBeQBfICskBeQBbIC8gCeQFZIC8gC+QFZIG8gCyQF5AF8gKyQF5AFsgLyAJ5AVkgLyAL5AVkgbyALJAXkAXyArJAXkAWyAvIAnkBWSAvIAvkBWSBvIAskBeQBfICskBeQBbIC8gCeQFZIC8gC+QFZIG8gCyQF5AF8gKyQF5AFsgLyAJ5AVkgLyAL5AVkgbyALJAXkCWkvPcSLqoFB8745YXyQEPwsMHaQMgLNIxf3j0+BaYN5AVkgbyALJAXkAXyArJAXkAWyAvIAnkBWSAvIAvkBWSBvIAsZt5tF1fVi90Pcza7vLMuJAPyAlcYebe9YJK8K8Y5tS0kB/ICV5h492bOJHk37Pg6eazpDHlBDPq9233Fjr+VVF3NXqb/P8ylSy/kBTHo92772eXdppJ3tzy5q36YFlIBeYErzLyT5N0uskvu6ujGspAMyAtcsa+84uaN/fzzz/zFz4qf+dvlz/v7+ut9f+rqxc/p/izweuVl31WcsTPx8/5esTCH/UPH/b1qKbKWD5tQ8paayvI23IW8wApreW1u2JhCU0nepruQF1hhLa9NUxlTaFrJ23IX8gIr7OW16KRgCk1LedvuQl5ghZW8a3HRNe8eZgpNC3kV7kJeYMUAeXffmw7MYQpNc3lV7p5BXmCD1yGRTKFpJq/aXcgLbPAub1NTIa/aXVx5gRW+5W1pyuXVuIuYF1jhWd62pqm8OnchL7DCr7wKTe/vte5CXmCFX3kVmt7fa92FvMAKz1felqb8yqtzVy2vPD8v5AUS/pvKGp7WRpXV3YW8wIrA8p6xtrxVDKwPG9RA3sMmrLyppy15pfs3yAtsCCov97Qpr9z2AHmBDSHlFZ425K21m0FeYENAeTNP6/LW23whL7AhnLz8Xq1C5S7kBVYEk1fcqzXkNc9hg7ygTfP8v3ub8/sehZTLdfGBZpknefEYwonSOP/bBcuRkoNtC6mW27kLeYEVjfO/++V1yl+/mF3+eKf+gEEh1XI7d72GDfB2emjO/3p2pX7DphBlAmaXz5AX2KA5/9vFibsrr6m7kBdYoZXXXcxr7G5HGhDkBW3U53/3PXN25bVwF/ICG7StDa5iXgt3ceUFVjRbG775k+DLn/YopFpu5y5iXmBF8ATMDnchL7AieAJmh7vO5GUK+KTWWhRloGdj/LTP29vXop/iSxetDXbuupNXPV/EmW57IC9NmuftYe6ye9jOXYfyquaL0LqrlFdwQN5S/GNtnrcV+2g++/hzJqbUG1pIudzOXXfyKueL0H8PQN5JyLtdzF7y2aPX7Hx4IdVyO3cdxryW80XodozOeXQDsf1tyXt0s2ZXafTgsHvY1F2HV952LZ3zReh2jNjJ3Bti+6uQd5NedV12Dxu76/KGrVVL53wRuh0jdjL3htj+tmLe2Uv+uImHuXt5e931JW87/ahRNeTNIba/zfO2YUf/u2T/uqxN229bSLnczt2w8srhig5N47DFoaEFcXmT2/dvHi4YO7a48Fo9RLDDXV/y6tvI+uo9tPn9qMsreGeTwTY4h81bAmYzXOlrb4a8OZOQ11Eh3Tls/hIwG+FKb18J5M2hL+8v3375x//tW0i23M5dL/IauHto8urHeBCL8dsx75yxo/+xygIalMPmMwGzHq7091Gr6p3wzKqTmcO73dpw/N+Lo5uVyx42U3c9yDs8XIG849/f5mD05ewl76Bw2cNm7K6zTArP4cpoT6YhU5WXi1v8G1xItdzSXdfyegpXRnsyDYG8HYVUy+3cdX3l9RWujPZkGjJVeZMVu8rGNzjqYbNx13HMa1w15C0gLu/DfPbxfPbnuaPxvFbuupXX3F3bK/5oT6Yhk5U34X3DjB3buGuXw9aRlOlSXht3IW8OdXmTZPfbT3a9w1Y5bF0JxT5z2DrcxZW3gLa8288/Ejdqu6WnHLbOZHifOWwd7iLmLaAs79u3vy2OfuJTS7/xMJ63112vOWwO54sY7ck0ZJLyVnM9pfhIA+qbQMdnDpvD+SJGezINmcyDRmsb9vj6r/PZf4l5G2zmlt4vATNMDpvL+SJGezINmaa8fK6yL22sVRdSLbdz12MOm9P5IkZ7Mg2ZzHNrAo3nNXLXawKmw/kiRnsyDZmwvC6ne7Jz15+8bueLGO3JNGSy8rqd7snOXW/yOp4vYrQn05DJyuttuieTCSO9JWC6nS9itCfTkKnK6226J6PJTn0lYDqeL2K0J9OQ6crrZ7ons4l6PSVgup4vYrQn05Apy+thuiczdz0lYDqfL2K0J9OQqcrrZ7onQ3c9JWD2ugt5ie5vOwHT/XRPpu6OKgGT4sk0ZLLyepjuydhdJGCGYbryClxO92ThLhIwgzBxeR0VEushgkjA7GSK8tZGRLrqYbNxN1YCJjIpiO6vtGHF0y/zZ2A6aee1cjdSAiZy2Kjur9+wwc5d7wmYZ27mixjtyTQE8poUMqaHCGaXWCfzRYz2ZBoyUXnffGP5yGxVIdJyO3c9J2CeaSeMhLw091fesN3SOnutXUhtuZ27fhMwkcNWMEl51+zkOnlcWg0oaxVSW27nrtcETOSwlUxRXj69aZJYDihrFlJfbueu14cIIoetZIry5iPJ7AaUNQupL7dzFzlsYYC8mkLqy+3cRQ5bEuQB1pBXU0h9uZ27yGFLIK8NweT1MCh8ujlsfh8pNVF5+Txl+XRlNuPKIg0Kn24OG+Q1wvfAHBt3kcNWAHmNkJvKfnktYTNZWaRB4dPNYYO8Rngfz2vhLnLYCiCvESHk9TUofLo5bJDXiADyehsUPt0ctr3k7W1sg7wmheAhggOBvEZEyWHTjVhEDlvO/mFDVwmQ16QQPERwIJDXCM/yWrmLhwgWQF4jwuewdSRl4iGCOZDXiOA5bF0JxXiIYA7kNcLzldfKXTxEsADyGhGkh83QXTxEsADyGhFY3u7MSDxEMMdOXqbg/l61NMfRYY5OWHl7snrxEMEcS3kVO3h/33HAHR3m6ASVty8jHQ8RzBkgb2MHM3n9dmRGJ6S8vbMpHFgCpv57XfOl37G7zR0U8nruyIxOQHn7ZwI5sARMfbV2T19XtQxyeX13ZEYnnLwGs9gcWAKmO3nbO5jK670jMzoGG7b7Yc5ml1VixTr7DrvqLwQPEezEmbyKHby/99+RGR2DDVsJV08bry3lNXH30BIwncnbvFerUO70Acm7YcfXyeNFKetu2ZoOalhGQ5gcthEnYLq78tb2TSuv647M6PRv2Cqfway49G4XradcDcpoCJPDNuYETIc3bAYH131HZnR6Nyy/0FbX24d5axbJIRkNYXLYRp2A6U/eMB2Z0endsOJCuyomctiwy88Z++TaoBA8RLATb/IG6siMjr28eWODCCaKhnZd4XbuTiwBc49csv3kDdWRGR17eVfs07tk90p+vqt1RoObQeEjT8CMJK/uqTGDd3dK8mbsltJr24wGR4PCKSRgDhuauIe8Z9onbxygvK0btpyVmbw27k7xIYKh5fXQuEJY3mZT2XbRltkuo8HZoHBHCZhec9gCy+ujcYWyvM1OihV7etd47IpVRoO7QeHWCZgRHiIYVl4vjSuU5ZW6h9f8IpzPhCpHETYZDQ4HhdsmYMZ4iGBQef00rpCWd/d9MTBHyJs8vmBs9lSOgC0yGlwOCrdMwNTfyjiS1106zjB5PTWukJZ3eCEH9hDBLFpRZDRYRyuD5PXVuAJ5jY6vzwRMh+FKZ7SiyGiwHxQ+RF5jdyGvUSEH9hBBpohMhg0KHyCvubtIAzIq5MAeIuhuULi9vDbuQl6TQg7sIYJOBoXLnzLfXRt3ceU1KuTAHiLoZFD4IHmt3EXMa1TIgT1EcKKzW0HeoP2WkXLYJjq71cHLG7bfMlIO20Rntzp0eQP3W0bKYZvo7FYHLm/ofstIOWwTnd3qsOUN3m8ZKYdtorNbHbS8FgNrXZ9NP+HK4FA7TONKsI7M6PiX18Jd4jlsE53d6oDltXCXeg7bRGe3Olx5bdyl/hDBic5udbDyWrlL/SGCE53d6lDltXOX+kMEJzq71aHKa+cu9YcITnR2q0OV185d6g8RnOjsVocqr5lA1IZZWYfabqIVJGA2GUECJrlhVrahtqNoBQmYTeInYNIbZmUZaruKVmLNbgV5Ow4luWFWdqG2s2gl1uxWkFd/KOkNs7IKtd1FK7Fmt4K8uuNLcZiVTajtMFqJNbsV5J3SMCuLUNtltBJrdivIO6VhVmMbFB4rXIlOzARMqsOsxjYoPFa4Ep2ICZhkh1mNbVB4rHAlOvESMOkOsxrboHDksPkoZKLDrMY2KBw5bD4Kmegwq7ENCkcOm49CJjrMamyDwpHD5qOQiQ6zGtugcOSw+ShkosOsxjYoHDlsPgqZ6DCrsQ0KRw6bj0ImOsxqbIPCkcPmo5CJDrMa26Bw5LD5KGSiw6zGNigcOWw+CpnoMKuxDQpHDpuPQiY6zMo2WtH9KRFpXDGVV3qYhtkH9iZ+Dhu9YVaW0Yr2rpXI7FaQ1+j4EhlmZRet6FtciMxuZRM2BPNWEDuHjeIwK6topaO1kMjsVpDX6PgSGWZlE610tXQTmd0K8k5pmJVFtNLZS0NkdivIO6VhVubRSncPI5HZrTq+aVrc3ysWFmj9GUrMHDaqw6z2C7XDNK4E6shs1iIeVKtrGdT6M5SIOWxkh1ntFWqHaVwJ1JHZqoXLq20Z1PozlHg5bHSHWe0TaodpXAnWkSnXon3IfRGtaP0ZSrQcNsLDrPYItcM0rsTpyNTLm0crWn+GEiuHjfIwq+GhdpjGlbF1ZBbRiqqM+3365SLlsJEeZjU41A7TuDK2jswyWlGVMXJ5LdwlMsxqaKgdpnFlbB2ZVbSi9Wdo63CUHDZtY4rbo+orXBkYaodpXBlbR6YUrWj9Gau8Vt39U8lhM3OXSsugq9YVcvLaDVWZSA6bobtUWgZdta5Qk9fO3TjDrFJ3AyRghmlcGVtHZj1a0fozTnnt3I0yzIontvlPwFRuDpGWQVetK9TktXM3xjArkZTpPQFTsznOdre7mlgdmc1oRevPOOU1OZT+u346qx4Qa1uH2prNIdIy6Kp1hby8PY0pro6qnbu+EzB1UhFpGXTVukJd3r7GFFdH1c5dzwmYWqmItAy6al0hLm9vY4rro9pX9bBY2y7U1ktFpGXQVesKbXn7G1McH9Xeszgs1rYKtTukIjK7lavWFdLyGjSmuD2qfVUPjbX3HWUVqGXQ+0ME7VpXzvT5QZrkIa1v5Qb0rmEAxWFW8qn1l4DZ+WVOZHYrN60rXdHK/b1NtdIG9K5hAMFhVrXLUtActkAtgzHDFdtoZezymjWmODyqfVXvEWtTHRQeLFyxjVZGLq9hY4q7o9p3LPeJtYkOCg/VkanbHKrymjamODuq3aexeSsTLoctUMtgxHDlO12kTVVe48YUV0e1u5rWbXiwHLZALYMRwxVV3b3RypjlNb6fCNVvuWesTXFQeMSOzP5oZcTyWtwLuzqqXdUomj8D5bAFahmMGK50uUtSXgt3w/Rb7h1r0xsUHrEj0yRaGa28Nm2QQfot94+1yQ0Kj9iR2RetyKnvhtVKG9C7hgF0hllpukwdn0zDQTITy2HrcZeevHZ9PwH6LS07LgedTEN3J5bD1ueuh2mB/co7vn5Ly45L62pNBXJ5NkcRrvS6S07e8fdbDglXBkQr6s1xt7v9x1YiVKztKVqRNqB3DQNo9Fs6C1eGNK44iFaGNa7E68j0Fa1IG9C7hgEk+i3dhSukGlcUfzZhYm1v0Yq0Ab1rGECh39JhuEKpcSVIX5CRu9Tljdhv6TJcIdS4EqQvyMxd4vJG7Ld0Gq4QalxRVR0i1vbZuCJtQO8aBoy+39JtuEK7cSVErK2smrK8BvfCRIZZkW5cCRFr+w21pQ3oXcOA4YPC6/fCIXPY9ghXKDeuhIi1PYfa0gb0rmHA4EHhsbp+Gn82h5PDFiLW9t0yKG1A7xoGDB0UHqvrZ8++H7qNKyFibe8tg9IG9K5hwMBB4bG6fvbt+yHbuBIi1vbfMihtQO8aBgwbFB6r62fvcIVq40qIWDtAy6C0Ab1rGDCs37K9k6Fy2PYMV8Y+KFxXdYBYO0TLoLQBvWsYMNp+Sz/hysgHhYcLV6zcJSlvxH5LT+HKuAeFjy9ccRytSBvQu0ay+2HOZpd32tfd8tp0mYYZZtWuGjls+9fbX3UUeVdivslT7etOea26+4kMsxrzoPARhysx5N2w4+vk8YJdaV53FEJimNUZctj2r9ek6hjyrmYv0/8f5qea1x2FUBhmFeY5bIFaBkcdrkSQd7c8uat+tF93FUJgmFWY57Bpqna3u6YCfef4MBudVsfVShvQt8J2kV1iV0c3qtedE7DrJ3J3RKR6D2x3R3aYpQ3oW6FHXrNCAPAA5AVkgbyALF5v2ADwidemMgB84rWTAgCfWHUPr8VF17x7GACfmAzM+b4YiJPJW722KAQA53gdEgmATyAvIAvkBWSBvIAskBeQBfICskBeQBbIC8jiRl4AwuFWXlfE2phI9WJ3R1fiHuBsTrleyDulerG7oytxD3A2p1zvxOUFwAbIC8gCeQFZIC8gC+QFZIG8gCxR5V3nKchrls1gsl2c3Fa9gFednzUnmyZlk5f6pJZ9x9m9aubkpR/JKm/Po+2w2rRs9onzanvrTcS7V/WP+N/dx88Zmz11u7tR5c0nf9gtc1M37HxTuutJ3nrec157Y+m2SOxvJ0q7rlaausVNtX31ch7mtYMbYnfTKjnHN9In9q42qrzplZafu4f5P2dzSGXZyfXZeFzUkh3W7Ei9mWeVlGzYyXXyuJCWvpmXf0ytKSqcVbsWZS/ZueNq++pNpIuFy3q7q02rfJ443924MW82+04aPay4rrtlFj14lbf5lZn/xWzKw7r7ih1/m62jmBzIVbX5vhYzv7mrtm93E77H31YLw+xuvp+OdzeuvNkuro5uhEHFrsWVd/vZ5V22jmpaNlfVPszPG6s7qrZf3nSJtDDM7tZWclZtXHnFKeR7JH4pdjhs2PAw52HDRW1ptrJqQkxX1abL31ykN2zXjYV7V9sbNvD3G2r5392yovPaqz2rjSuv0JTvw26Z7sE633xP8hY8bbx/y+8lZt7OprraDftQLK0V7VRe3e7yYj3Kq6uWk14n5BNLXF7hq4h50k1vzqLqikYjzvPG27sX2cF2elh7q02Xf3qXvHtRu8n2IG9rd0XzpHd5W9VyHtrfPvtVG1nedPuzJofN7GUZBvoLGx6Xs2fNt1fcot0rt19ovdXmX6DFPaq7anvqzQ6y37BBdZSTvH3FabWR5d0uzrPTmB7UTfF36THm3S1Z80Zpkbc1ty1ydwfTrvZhnrdxuq62p9518bUuXwT9765Y1iyX+A0b3+Tvs6knl6flefR5w7ZdNO4kOuR12HYUrtqeejvk9bm7Sp/3rjb22Ib17IPM1PXxRdkG6LO1YdO4AKRH9akIG9rBp8tW+2a1abSSVvu4dF5tX71yRS7r7d3ddql7Vxtb3od5fvo2Va+P33beVeMSkHdc8j//dXG9KFZ20V+qqXZ7UbY2OK22r16pooC7mx9ksb/uqo0t73aR78F2UX6B+pW39ZX2yJsbRINr67C259F2Vy0fD5S1cTittrfeqqKAu1s2oankHVxtbHkBGAzkBWQ5SHmlcZfKXsxpVTvd3YW8k692urt7kPKCaQB5AVkgLyAL5AVkgbyALJA3kbNTct4ZftBVX6Bczvazl8o88pWim9d4c0x3iBaQN2nL+/f3DYeW+pB3darOI394r7e9Sbs5xjtEC8ibtOU1HhftQd5NlYraSAhbDRypkwwe1z52IG8yLnmFospU3M3wpn7IO12EK6lAv16w2bNsLpvTbLSZGOy0W56u2dFPxfsptx9kb0lpd3yV6+ozyerkjxeitBf52LHHF/Ns8Fo2+FpkP7XKyTMslPKWf2LKAvJNvKttXG2HxDC2j+qZOLSBvEkpbxZfnufnOh+CKt55MmcnfxTvl+kI57K8fJW76jOpvF/zX58v88/kb4nU3SKNrF1OPl5QnUdeXD+VBWSbmBYjLavv0Cp8x7RnIG9SyXvKT/1pbkmRmHmVp7BU728X6TU2eUivfJK8QqjqM+mvJ9d8SqP0/1ueVrAqEzYyM9M6FOXkgqrzyIuBsMoCsk08uastk3coS3S9VY1NpwrkTUp5uTfiFPNzXU4CeJq/I72fJG9ff/MBq8nL35Q+k323F5/kTuVphjzXX6gkVm2XI35R55FXaQqKAoqKmsvKHdouZp+8/j3QEQ0D5E2qmPcu/z+TN1enUEv6P3+vJZ30mewSWn2myOvnV08uoRBRV44mj7wWA6sKUG1cuUNZPDE4QWOMQN6kR95iNpTq/+2CfXz5428Lvbz55VUjb3plFm9oy9HkkZfy6gpQbVwlb/Lbi/wPaypA3kQnbxkcNuUtbv4V8lYBZUNeOWxI1kd/q+ZmU5SjySOvcn41Bag2TpI35d2biwndsUHeRCGvuDzOnvEbnPmpQt70Rujxov11L32mKa90w8Yl/4IrpCinccNWzyMvMxd1Bag2rtyhNCD/XUQhkHdSNOVdS01lwuNW2FALKJLyiiml0Tflld4qZo9RlKNsKivyyFflN76mANXGVTuUNZUNzagfI5A3acu75ReuKiW+dcOWXtjYk+fp5aw1N2CVRt+UN+u/eJrd7q8zG9vl5JGHMo98u6iCEnUBqo2rdkg8BEM5Ax5VIO/IqC6vTfboHp4okHdk6BXdY2DORIG8Y0PnqMGQyEMD8o4NPhhdhcFg9EMD8gKyQF5AFsgLyAJ5AVkgLyAL5AVkgbyALJAXkAXyArL8P+o3UlT1BV9kAAAAAElFTkSuQmCC" />

<!-- rnb-plot-end -->

<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuI2dnc2F2ZShcIm91dHB1dC9UcnVuVl9yZWRfcmVsX21heC5wbmdcIiwgd2lkdGggPSAxMC4xNiwgaGVpZ2h0ID0gMilcblxuYGBgIn0= -->

```r
#ggsave("output/TrunV_red_rel_max.png", width = 10.16, height = 2)

```

<!-- rnb-source-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->

### test epistasis effect between all IR variants

<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuIyBNZXRob2QgMDogY29tYmluZSBhbGwgSVIgdmFyaWFudHMgZm9yIGVwaXN0YXNpcyB0ZXN0XG5JUi5lcGkgPC0gYmluZF9yb3dzKG9sLnJlbCwgVHJ1blYucmVsKSAlPiUgc2VsZWN0KEdlbm90eXBlLCBUcmVhdG1lbnQsIG1lZGlhbiwgbWVkaWFuX2FkaiA9IG5ld19tZWRpYW4pICU+JSBcbiAgbXV0YXRlKG1lZGlhbiA9IG1lZGlhbi8xMDAwLCBiZXRhXzIuNCA9IDEsIGJldGFfNC42ID0gMSwgYmV0YV82LjggPSAxLCBiZXRhXzguMTAgPSAxKVxuYGBgIn0= -->

```r
# Method 0: combine all IR variants for epistasis test
IR.epi <- bind_rows(ol.rel, TrunV.rel) %>% select(Genotype, Treatment, median, median_adj = new_median) %>% 
  mutate(median = median/1000, beta_2.4 = 1, beta_4.6 = 1, beta_6.8 = 1, beta_8.10 = 1)
```

<!-- rnb-source-end -->

<!-- rnb-output-begin eyJkYXRhIjoiQWRkaW5nIG1pc3NpbmcgZ3JvdXBpbmcgdmFyaWFibGVzOiBgZ2Vub3R5cGVgXG4ifQ== -->

```
Adding missing grouping variables: `genotype`
```



<!-- rnb-output-end -->

<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuIyBzZXQgdXAgY29udHJhc3QgbWF0cml4XG5JUi5lcGkkYmV0YV8yLjQgPC0gd2l0aChJUi5lcGksIGlmZWxzZShHZW5vdHlwZSA9PSBcIklSXzIuNFwiIHwgR2Vub3R5cGUgPT0gXCJJUl8yLjEwXCIsIDAsIDEpKVxuSVIuZXBpJGJldGFfNC42IDwtIHdpdGgoSVIuZXBpLCBpZmVsc2UoR2Vub3R5cGUgPT0gXCJJUl80LjZcIiB8IEdlbm90eXBlID09IFwiSVJfMi4xMFwifCBHZW5vdHlwZSA9PSBcIklSXzQuMTBcIiwgMCwgMSkpXG5JUi5lcGkkYmV0YV82LjggPC0gd2l0aChJUi5lcGksIGlmZWxzZShHZW5vdHlwZSA9PSBcIklSXzYuOFwiIHwgR2Vub3R5cGUgPT0gXCJJUl8yLjEwXCJ8IEdlbm90eXBlID09IFwiSVJfNC4xMFwifCBcbiAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgIEdlbm90eXBlID09IFwiSVJfNi4xMFwiLCAwLCAxKSlcbklSLmVwaSRiZXRhXzguMTAgPC0gd2l0aChJUi5lcGksIGlmZWxzZShHZW5vdHlwZSA9PSBcIklSXzguMTBcIiB8IEdlbm90eXBlID09IFwiSVJfMi4xMFwifCBHZW5vdHlwZSA9PSBcIklSXzQuMTBcInwgXG4gICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICBHZW5vdHlwZSA9PSBcIklSXzYuMTBcIiwgMCwgMSkpXG5cbklSLmVwaS5waSA8LSBJUi5lcGkgJT4lIGZpbHRlcihHZW5vdHlwZSAhPSBcIlBDXCIsIFRyZWF0bWVudCA9PSBcIjBQaVwiKVxuSVIuZXBpLm94aSA8LSBJUi5lcGkgJT4lIGZpbHRlcihHZW5vdHlwZSAhPSBcIlBDXCIsIFRyZWF0bWVudCA9PSBcIjJtTUgyTzJcIilcblxuIyBsbSgpIGZpdFxuIyBvcmlnaW5hbCBkYXRhIHdpdGhvdWQgYmFzYWwgZGVkdWN0aW9uXG5maXQucGkgPC0gSVIuZXBpLnBpICU+JSBsbShtZWRpYW4gfiBiZXRhXzIuNCArIGJldGFfNC42ICsgYmV0YV82LjggKyBiZXRhXzguMTAgK1xuICAgICAgICAgICAgICAgICAgICAgICAgICAgICBiZXRhXzIuNDpiZXRhXzQuNiArIGJldGFfNC42OmJldGFfNi44ICsgYmV0YV82Ljg6YmV0YV84LjEwLCBkYXRhID0gLilcblxucm91bmQoc3VtbWFyeShmaXQucGkpJGNvZWYsIDMpXG5gYGAifQ== -->

```r
# set up contrast matrix
IR.epi$beta_2.4 <- with(IR.epi, ifelse(Genotype == "IR_2.4" | Genotype == "IR_2.10", 0, 1))
IR.epi$beta_4.6 <- with(IR.epi, ifelse(Genotype == "IR_4.6" | Genotype == "IR_2.10"| Genotype == "IR_4.10", 0, 1))
IR.epi$beta_6.8 <- with(IR.epi, ifelse(Genotype == "IR_6.8" | Genotype == "IR_2.10"| Genotype == "IR_4.10"| 
                                       Genotype == "IR_6.10", 0, 1))
IR.epi$beta_8.10 <- with(IR.epi, ifelse(Genotype == "IR_8.10" | Genotype == "IR_2.10"| Genotype == "IR_4.10"| 
                                       Genotype == "IR_6.10", 0, 1))

IR.epi.pi <- IR.epi %>% filter(Genotype != "PC", Treatment == "0Pi")
IR.epi.oxi <- IR.epi %>% filter(Genotype != "PC", Treatment == "2mMH2O2")

# lm() fit
# original data withoud basal deduction
fit.pi <- IR.epi.pi %>% lm(median ~ beta_2.4 + beta_4.6 + beta_6.8 + beta_8.10 +
                             beta_2.4:beta_4.6 + beta_4.6:beta_6.8 + beta_6.8:beta_8.10, data = .)

round(summary(fit.pi)$coef, 3)
```

<!-- rnb-source-end -->

<!-- rnb-output-begin eyJkYXRhIjoiICAgICAgICAgICAgICAgICAgIEVzdGltYXRlIFN0ZC4gRXJyb3IgdCB2YWx1ZSBQcig+fHR8KVxuKEludGVyY2VwdCkgICAgICAgICAgIDcuODI0ICAgICAgMC44NTMgICA5LjE2NyAgICAwLjAwMFxuYmV0YV8yLjQgICAgICAgICAgICAgIDguMDc4ICAgICAgMS4zMDQgICA2LjE5NyAgICAwLjAwMFxuYmV0YV80LjYgICAgICAgICAgICAgLTUuNjI5ICAgICAgMS41ODQgIC0zLjU1NCAgICAwLjAwMVxuYmV0YV82LjggICAgICAgICAgICAgMTMuMDQ4ICAgICAgMS42NTkgICA3Ljg2NiAgICAwLjAwMFxuYmV0YV84LjEwICAgICAgICAgICAgIDMuNjEyICAgICAgMS4xMzggICAzLjE3NCAgICAwLjAwMlxuYmV0YV8yLjQ6YmV0YV80LjYgICAgIDIuNDgyICAgICAgMS42ODMgICAxLjQ3NCAgICAwLjE0NVxuYmV0YV80LjY6YmV0YV82LjggICAgLTMuMTExICAgICAgMS43NTQgIC0xLjc3NCAgICAwLjA4MVxuYmV0YV82Ljg6YmV0YV84LjEwICAgIDIuNzE1ICAgICAgMS40NTEgICAxLjg3MiAgICAwLjA2NVxuIn0= -->

```
                   Estimate Std. Error t value Pr(>|t|)
(Intercept)           7.824      0.853   9.167    0.000
beta_2.4              8.078      1.304   6.197    0.000
beta_4.6             -5.629      1.584  -3.554    0.001
beta_6.8             13.048      1.659   7.866    0.000
beta_8.10             3.612      1.138   3.174    0.002
beta_2.4:beta_4.6     2.482      1.683   1.474    0.145
beta_4.6:beta_6.8    -3.111      1.754  -1.774    0.081
beta_6.8:beta_8.10    2.715      1.451   1.872    0.065
```



<!-- rnb-output-end -->

<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuZml0Lm94aSA8LSBJUi5lcGkub3hpICU+JSBsbShtZWRpYW4gfiBiZXRhXzIuNCArIGJldGFfNC42ICsgYmV0YV82LjggKyBiZXRhXzguMTAgK1xuICAgICAgICAgICAgICAgICAgICAgICAgICAgICBiZXRhXzIuNDpiZXRhXzQuNiArIGJldGFfNC42OmJldGFfNi44ICsgYmV0YV82Ljg6YmV0YV84LjEwLCBkYXRhID0gLilcblxucm91bmQoc3VtbWFyeShmaXQub3hpKSRjb2VmLCAzKVxuYGBgIn0= -->

```r
fit.oxi <- IR.epi.oxi %>% lm(median ~ beta_2.4 + beta_4.6 + beta_6.8 + beta_8.10 +
                             beta_2.4:beta_4.6 + beta_4.6:beta_6.8 + beta_6.8:beta_8.10, data = .)

round(summary(fit.oxi)$coef, 3)
```

<!-- rnb-source-end -->

<!-- rnb-output-begin eyJkYXRhIjoiICAgICAgICAgICAgICAgICAgIEVzdGltYXRlIFN0ZC4gRXJyb3IgdCB2YWx1ZSBQcig+fHR8KVxuKEludGVyY2VwdCkgICAgICAgICAgMTIuNTkxICAgICAgMi4yOTMgICA1LjQ5MCAgICAwLjAwMFxuYmV0YV8yLjQgICAgICAgICAgICAgNDIuODMzICAgICAgMy42MjYgIDExLjgxMiAgICAwLjAwMFxuYmV0YV80LjYgICAgICAgICAgICAgIDAuNzE5ICAgICAgNC4yMjUgICAwLjE3MCAgICAwLjg2NVxuYmV0YV82LjggICAgICAgICAgICAgIDEuMzY2ICAgICAgNC40MDkgICAwLjMxMCAgICAwLjc1OFxuYmV0YV84LjEwICAgICAgICAgICAgMjcuNzk3ICAgICAgMy4wMzQgICA5LjE2MiAgICAwLjAwMFxuYmV0YV8yLjQ6YmV0YV80LjYgICAtMTguNTQwICAgICAgNC41MjUgIC00LjA5NyAgICAwLjAwMFxuYmV0YV80LjY6YmV0YV82LjggICAgMTQuMzc1ICAgICAgNC43MzggICAzLjAzNCAgICAwLjAwM1xuYmV0YV82Ljg6YmV0YV84LjEwICAgLTkuNjAyICAgICAgMy44NTIgIC0yLjQ5MyAgICAwLjAxNVxuIn0= -->

```
                   Estimate Std. Error t value Pr(>|t|)
(Intercept)          12.591      2.293   5.490    0.000
beta_2.4             42.833      3.626  11.812    0.000
beta_4.6              0.719      4.225   0.170    0.865
beta_6.8              1.366      4.409   0.310    0.758
beta_8.10            27.797      3.034   9.162    0.000
beta_2.4:beta_4.6   -18.540      4.525  -4.097    0.000
beta_4.6:beta_6.8    14.375      4.738   3.034    0.003
beta_6.8:beta_8.10   -9.602      3.852  -2.493    0.015
```



<!-- rnb-output-end -->

<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuIyBkYXRhIGRlZHVjZWQgYmFzYWwgZGVkdWN0aW9uXG5maXQucGkgPC0gSVIuZXBpLnBpICU+JSBsbShtZWRpYW5fYWRqIH4gYmV0YV8yLjQgKyBiZXRhXzQuNiArIGJldGFfNi44ICsgYmV0YV84LjEwICtcbiAgICAgICAgICAgICAgICAgICAgICAgICAgICAgYmV0YV8yLjQ6YmV0YV80LjYgKyBiZXRhXzQuNjpiZXRhXzYuOCArIGJldGFfNi44OmJldGFfOC4xMCwgZGF0YSA9IC4pXG5cbnJvdW5kKHN1bW1hcnkoZml0LnBpKSRjb2VmLCAzKVxuYGBgIn0= -->

```r
# data deduced basal deduction
fit.pi <- IR.epi.pi %>% lm(median_adj ~ beta_2.4 + beta_4.6 + beta_6.8 + beta_8.10 +
                             beta_2.4:beta_4.6 + beta_4.6:beta_6.8 + beta_6.8:beta_8.10, data = .)

round(summary(fit.pi)$coef, 3)
```

<!-- rnb-source-end -->

<!-- rnb-output-begin eyJkYXRhIjoiICAgICAgICAgICAgICAgICAgIEVzdGltYXRlIFN0ZC4gRXJyb3IgdCB2YWx1ZSBQcig+fHR8KVxuKEludGVyY2VwdCkgICAgICAgICAgIDYuMDg5ICAgICAgMC44ODUgICA2Ljg3OSAgICAwLjAwMFxuYmV0YV8yLjQgICAgICAgICAgICAgIDcuNDgzICAgICAgMS4zNTIgICA1LjUzNSAgICAwLjAwMFxuYmV0YV80LjYgICAgICAgICAgICAgLTUuNjcwICAgICAgMS42NDMgIC0zLjQ1MiAgICAwLjAwMVxuYmV0YV82LjggICAgICAgICAgICAgMTEuMzE0ICAgICAgMS43MjAgICA2LjU3NiAgICAwLjAwMFxuYmV0YV84LjEwICAgICAgICAgICAgLTAuNzYyICAgICAgMS4xODAgIC0wLjY0NSAgICAwLjUyMVxuYmV0YV8yLjQ6YmV0YV80LjYgICAgIDMuNTMwICAgICAgMS43NDYgICAyLjAyMiAgICAwLjA0N1xuYmV0YV80LjY6YmV0YV82LjggICAgLTEuOTY3ICAgICAgMS44MTkgIC0xLjA4MSAgICAwLjI4M1xuYmV0YV82Ljg6YmV0YV84LjEwICAgIDMuMTU0ICAgICAgMS41MDQgICAyLjA5NyAgICAwLjA0MFxuIn0= -->

```
                   Estimate Std. Error t value Pr(>|t|)
(Intercept)           6.089      0.885   6.879    0.000
beta_2.4              7.483      1.352   5.535    0.000
beta_4.6             -5.670      1.643  -3.452    0.001
beta_6.8             11.314      1.720   6.576    0.000
beta_8.10            -0.762      1.180  -0.645    0.521
beta_2.4:beta_4.6     3.530      1.746   2.022    0.047
beta_4.6:beta_6.8    -1.967      1.819  -1.081    0.283
beta_6.8:beta_8.10    3.154      1.504   2.097    0.040
```



<!-- rnb-output-end -->

<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuZml0Lm94aSA8LSBJUi5lcGkub3hpICU+JSBsbShtZWRpYW5fYWRqIH4gYmV0YV8yLjQgKyBiZXRhXzQuNiArIGJldGFfNi44ICsgYmV0YV84LjEwICtcbiAgICAgICAgICAgICAgICAgICAgICAgICAgICAgYmV0YV8yLjQ6YmV0YV80LjYgKyBiZXRhXzQuNjpiZXRhXzYuOCArIGJldGFfNi44OmJldGFfOC4xMCwgZGF0YSA9IC4pXG5cbnJvdW5kKHN1bW1hcnkoZml0Lm94aSkkY29lZiwgMylcbmBgYCJ9 -->

```r
fit.oxi <- IR.epi.oxi %>% lm(median_adj ~ beta_2.4 + beta_4.6 + beta_6.8 + beta_8.10 +
                             beta_2.4:beta_4.6 + beta_4.6:beta_6.8 + beta_6.8:beta_8.10, data = .)

round(summary(fit.oxi)$coef, 3)
```

<!-- rnb-source-end -->

<!-- rnb-output-begin eyJkYXRhIjoiICAgICAgICAgICAgICAgICAgIEVzdGltYXRlIFN0ZC4gRXJyb3IgdCB2YWx1ZSBQcig+fHR8KVxuKEludGVyY2VwdCkgICAgICAgICAgMTAuNzA0ICAgICAgMi4yNDkgICA0Ljc2MCAgICAwLjAwMFxuYmV0YV8yLjQgICAgICAgICAgICAgNDIuMjc4ICAgICAgMy41NTYgIDExLjg5MSAgICAwLjAwMFxuYmV0YV80LjYgICAgICAgICAgICAgIDAuODg4ICAgICAgNC4xNDIgICAwLjIxNCAgICAwLjgzMVxuYmV0YV82LjggICAgICAgICAgICAgLTEuMTA5ICAgICAgNC4zMjMgIC0wLjI1NyAgICAwLjc5OFxuYmV0YV84LjEwICAgICAgICAgICAgMjMuMjE3ICAgICAgMi45NzUgICA3LjgwNSAgICAwLjAwMFxuYmV0YV8yLjQ6YmV0YV80LjYgICAtMTcuODk3ICAgICAgNC40MzcgIC00LjAzNCAgICAwLjAwMFxuYmV0YV80LjY6YmV0YV82LjggICAgMTUuNzQ1ICAgICAgNC42NDYgICAzLjM4OSAgICAwLjAwMVxuYmV0YV82Ljg6YmV0YV84LjEwICAgLTkuMDI0ICAgICAgMy43NzcgIC0yLjM4OSAgICAwLjAxOVxuIn0= -->

```
                   Estimate Std. Error t value Pr(>|t|)
(Intercept)          10.704      2.249   4.760    0.000
beta_2.4             42.278      3.556  11.891    0.000
beta_4.6              0.888      4.142   0.214    0.831
beta_6.8             -1.109      4.323  -0.257    0.798
beta_8.10            23.217      2.975   7.805    0.000
beta_2.4:beta_4.6   -17.897      4.437  -4.034    0.000
beta_4.6:beta_6.8    15.745      4.646   3.389    0.001
beta_6.8:beta_8.10   -9.024      3.777  -2.389    0.019
```



<!-- rnb-output-end -->

<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuIyBDb25jbHVzaW9uOiBcbiMgMS4gYWJzb2x1dGUgZGF0YSByZXZlYWxlZCB0aGF0IG5vIGVwaXRhc2lzIGVmZmVjdCBmb3IgLSBQaSAob25seSBhZGRpdGl2ZSBlZmZlY3QpOyBmb3Igb3hpZGF0aXZlIHN0cmVzcyBlcGlzdGF0aWMgZWZmZWN0IGlkZW50aWZlZCBiZXR3ZWVuIGFsbCBldmVyeSAyMDAgYnBzIENSTXNcblxuIyAyLiBFcGlzdGFzaXMgZWZmZWN0IG9uIEluZHVjdGlvbiBsZXZlbDogYWJzb2x1dGUgZGF0YSAoYmFzYWwgcmVkdWNlZCkgcmV2ZWFsZWQgZXBpdGF0aWMgZWZmZWN0IGJldHdlZW4gMjQgdG8gNDYsIGFuZCA2OCB0byA4MCByZWdhcmRsZXNzIG9mIHN0cmVzczsgZXBpc3RhdGljIGVmZmVjdCBiZXR3ZWVuIDQ2IHRvIDY4IG9ubHkgaW4gSDJPMiB0cmVhdG1lbnRcblxuIyAzLiBFcGlzdGFzaXMgZWZmZWN0IG9uIGJhc2FsIGV4cHJlc3Npb24gbGV2ZWw/XG5gYGAifQ== -->

```r
# Conclusion: 
# 1. absolute data revealed that no epitasis effect for - Pi (only additive effect); for oxidative stress epistatic effect identifed between all every 200 bps CRMs

# 2. Epistasis effect on Induction level: absolute data (basal reduced) revealed epitatic effect between 24 to 46, and 68 to 80 regardless of stress; epistatic effect between 46 to 68 only in H2O2 treatment

# 3. Epistasis effect on basal expression level?
```

<!-- rnb-source-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->


# epitasis test between 600 - 800 bps and 800 - 1kb bps region

<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuIyBNZXRob2QgSTogZ2V0IElSXzYuMTAsIElSXzYuOCwgSVJfOC4xMCBhbmQgV1QgZm9yIGVwaXN0YXNpcyB0ZXN0XG5JUl82ODEwLnBpIDwtIG9sLnJlbCAlPiUgZmlsdGVyKEdlbm90eXBlICVpbiUgYyhcIklSXzYuOFwiLCBcIklSXzguMTBcIiwgXCJXVFwiKSwgVHJlYXRtZW50ID09IFwiMFBpXCIsIFRpbWUgPT0gXCIyNDBtaW5cIilcblxuSVJfNjgxMC5veGkgPC0gb2wucmVsICU+JSBmaWx0ZXIoR2Vub3R5cGUgJWluJSBjKFwiSVJfNi44XCIsIFwiSVJfOC4xMFwiLCBcIldUXCIpLCBUcmVhdG1lbnQgPT0gXCIybU1IMk8yXCIsIFRpbWUgPT0gXCI5MG1pblwiKVxuXG5JUl82MTAucGkgPC0gVHJ1blYucmVsICU+JSBmaWx0ZXIoR2Vub3R5cGUgJWluJSBjKFwiSVJfNi4xMFwiLCBcIklSXzguMTBcIiwgXCJXVFwiKSwgVHJlYXRtZW50ID09IFwiMFBpXCIsIFRpbWUgPT0gXCIyNDBtaW5cIilcbklSXzYxMC5veGkgPC0gVHJ1blYucmVsICU+JSBmaWx0ZXIoR2Vub3R5cGUgJWluJSBjKFwiSVJfNi4xMFwiLCBcIklSXzguMTBcIiwgXCJXVFwiKSwgVHJlYXRtZW50ID09IFwiMm1NSDJPMlwiLCBUaW1lID09IFwiOTBtaW5cIilcblxuZXBpLnBpIDwtIGJpbmRfcm93cyhJUl82ODEwLnBpLCBJUl82MTAucGkpXG5lcGkub3hpIDwtIGJpbmRfcm93cyhJUl82ODEwLm94aSwgSVJfNjEwLm94aSlcblxuZXBpLnBpIDwtIGVwaS5waSAlPiUgc2VsZWN0KEdlbm90eXBlLCBUcmVhdG1lbnQsIG1lZGlhbiwgbWVkaWFuX2FkaiA9IG5ld19tZWRpYW4pICU+JSBcbiAgbXV0YXRlKG1lZGlhbiA9IG1lZGlhbi8xMDAwKVxuYGBgIn0= -->

```r
# Method I: get IR_6.10, IR_6.8, IR_8.10 and WT for epistasis test
IR_6810.pi <- ol.rel %>% filter(Genotype %in% c("IR_6.8", "IR_8.10", "WT"), Treatment == "0Pi", Time == "240min")

IR_6810.oxi <- ol.rel %>% filter(Genotype %in% c("IR_6.8", "IR_8.10", "WT"), Treatment == "2mMH2O2", Time == "90min")

IR_610.pi <- TrunV.rel %>% filter(Genotype %in% c("IR_6.10", "IR_8.10", "WT"), Treatment == "0Pi", Time == "240min")
IR_610.oxi <- TrunV.rel %>% filter(Genotype %in% c("IR_6.10", "IR_8.10", "WT"), Treatment == "2mMH2O2", Time == "90min")

epi.pi <- bind_rows(IR_6810.pi, IR_610.pi)
epi.oxi <- bind_rows(IR_6810.oxi, IR_610.oxi)

epi.pi <- epi.pi %>% select(Genotype, Treatment, median, median_adj = new_median) %>% 
  mutate(median = median/1000)
```

<!-- rnb-source-end -->

<!-- rnb-output-begin eyJkYXRhIjoiQWRkaW5nIG1pc3NpbmcgZ3JvdXBpbmcgdmFyaWFibGVzOiBgZ2Vub3R5cGVgXG4ifQ== -->

```
Adding missing grouping variables: `genotype`
```



<!-- rnb-output-end -->

<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuZXBpLm94aSA8LSBlcGkub3hpICU+JSBzZWxlY3QoR2Vub3R5cGUsIFRyZWF0bWVudCwgbWVkaWFuLCBtZWRpYW5fYWRqID0gbmV3X21lZGlhbikgJT4lIFxuICBtdXRhdGUobWVkaWFuID0gbWVkaWFuLzEwMDApXG5gYGAifQ== -->

```r
epi.oxi <- epi.oxi %>% select(Genotype, Treatment, median, median_adj = new_median) %>% 
  mutate(median = median/1000)
```

<!-- rnb-source-end -->

<!-- rnb-output-begin eyJkYXRhIjoiQWRkaW5nIG1pc3NpbmcgZ3JvdXBpbmcgdmFyaWFibGVzOiBgZ2Vub3R5cGVgXG4ifQ== -->

```
Adding missing grouping variables: `genotype`
```



<!-- rnb-output-end -->

<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuIyBzZXQgdXAgY29udHJhc3QgbWF0cml4XG5lcGkgPC0gYmluZF9yb3dzKGVwaS5waSwgZXBpLm94aSkgJT4lIG11dGF0ZShiZXRhXzYuOCA9IDAsIGJldGFfOC4xMCA9IDApXG5lcGkkYmV0YV82LjggPC0gd2l0aChlcGksIGlmZWxzZShHZW5vdHlwZSA9PSBcIklSXzYuOFwiIHwgR2Vub3R5cGUgPT0gXCJJUl82LjEwXCIsIC0xLCAwKSlcbmVwaSRiZXRhXzguMTAgPC0gd2l0aChlcGksIGlmZWxzZShHZW5vdHlwZSA9PSBcIklSXzguMTBcIiB8IEdlbm90eXBlID09IFwiSVJfNi4xMFwiLCAtMSwgMCkpXG5cbiMgbWFrZSB0aGUgc3RhdGlzdGljYWwgbW9kZWxcbiMjIG9yaWdpbmFsIGRhdGEgKGJhc2FsIGV4cHJlc3Npb24gbm90IGRlZHVjZWQpXG5maXQub3JpLnBpIDwtIGVwaSAlPiUgZmlsdGVyKFRyZWF0bWVudCA9PSBcIjBQaVwiKSAlPiUgbG0obWVkaWFuIH4gYmV0YV82LjggKyBiZXRhXzguMTAgKyBcbiAgICAgICAgICAgICAgICAgICAgICBiZXRhXzYuODpiZXRhXzguMTAsXG4gICAgICAgICAgICAgICAgICAgIGRhdGEgPSAuKVxucm91bmQoc3VtbWFyeShmaXQub3JpLnBpKSRjb2VmLCAzKVxuYGBgIn0= -->

```r
# set up contrast matrix
epi <- bind_rows(epi.pi, epi.oxi) %>% mutate(beta_6.8 = 0, beta_8.10 = 0)
epi$beta_6.8 <- with(epi, ifelse(Genotype == "IR_6.8" | Genotype == "IR_6.10", -1, 0))
epi$beta_8.10 <- with(epi, ifelse(Genotype == "IR_8.10" | Genotype == "IR_6.10", -1, 0))

# make the statistical model
## original data (basal expression not deduced)
fit.ori.pi <- epi %>% filter(Treatment == "0Pi") %>% lm(median ~ beta_6.8 + beta_8.10 + 
                      beta_6.8:beta_8.10,
                    data = .)
round(summary(fit.ori.pi)$coef, 3)
```

<!-- rnb-source-end -->

<!-- rnb-output-begin eyJkYXRhIjoiICAgICAgICAgICAgICAgICAgIEVzdGltYXRlIFN0ZC4gRXJyb3IgdCB2YWx1ZSBQcig+fHR8KVxuKEludGVyY2VwdCkgICAgICAgICAgMjkuMDIwICAgICAgMC43ODMgIDM3LjA1MiAgICAwLjAwMFxuYmV0YV82LjggICAgICAgICAgICAgMTIuNjUzICAgICAgMS4xOTYgIDEwLjU3NiAgICAwLjAwMFxuYmV0YV84LjEwICAgICAgICAgICAgIDYuMzI3ICAgICAgMS4wMTEgICA2LjI1OCAgICAwLjAwMFxuYmV0YV82Ljg6YmV0YV84LjEwICAgIDIuNzE1ICAgICAgMS42MzAgICAxLjY2NiAgICAwLjEwM1xuIn0= -->

```
                   Estimate Std. Error t value Pr(>|t|)
(Intercept)          29.020      0.783  37.052    0.000
beta_6.8             12.653      1.196  10.576    0.000
beta_8.10             6.327      1.011   6.258    0.000
beta_6.8:beta_8.10    2.715      1.630   1.666    0.103
```



<!-- rnb-output-end -->

<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuZml0Lm9yaS5veGkgPC0gZXBpICU+JSBmaWx0ZXIoVHJlYXRtZW50ID09IFwiMm1NSDJPMlwiKSAlPiUgbG0obWVkaWFuIH4gYmV0YV82LjggKyBiZXRhXzguMTAgK1xuICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgYmV0YV82Ljg6YmV0YV84LjEwLCBkYXRhID0gLilcbnJvdW5kKHN1bW1hcnkoZml0Lm9yaS5veGkpJGNvZWYsIDMpXG5gYGAifQ== -->

```r
fit.ori.oxi <- epi %>% filter(Treatment == "2mMH2O2") %>% lm(median ~ beta_6.8 + beta_8.10 +
                                                               beta_6.8:beta_8.10, data = .)
round(summary(fit.ori.oxi)$coef, 3)
```

<!-- rnb-source-end -->

<!-- rnb-output-begin eyJkYXRhIjoiICAgICAgICAgICAgICAgICAgIEVzdGltYXRlIFN0ZC4gRXJyb3IgdCB2YWx1ZSBQcig+fHR8KVxuKEludGVyY2VwdCkgICAgICAgICAgNzEuNTM4ICAgICAgMS45MzggIDM2LjkxMSAgICAwLjAwMFxuYmV0YV82LjggICAgICAgICAgICAgIDYuMTM5ICAgICAgMi44NTMgICAyLjE1MiAgICAwLjAzNlxuYmV0YV84LjEwICAgICAgICAgICAgMTguMTk1ICAgICAgMi41MDIgICA3LjI3MiAgICAwLjAwMFxuYmV0YV82Ljg6YmV0YV84LjEwICAgLTkuNjAyICAgICAgNC4wNjAgIC0yLjM2NSAgICAwLjAyMlxuIn0= -->

```
                   Estimate Std. Error t value Pr(>|t|)
(Intercept)          71.538      1.938  36.911    0.000
beta_6.8              6.139      2.853   2.152    0.036
beta_8.10            18.195      2.502   7.272    0.000
beta_6.8:beta_8.10   -9.602      4.060  -2.365    0.022
```



<!-- rnb-output-end -->

<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuIyMgZGVkdWNlZCBkYXRhXG5maXQuYWRqLnBpIDwtIGVwaSAlPiUgZmlsdGVyKFRyZWF0bWVudCA9PSBcIjBQaVwiKSAlPiUgbG0obWVkaWFuX2FkaiB+IGJldGFfNi44ICsgYmV0YV84LjEwICtcbiAgICAgICAgICAgICAgICBiZXRhXzYuODpiZXRhXzguMTAsXG4gICAgICAgICAgICAgIGRhdGEgPSAuKVxucm91bmQoc3VtbWFyeShmaXQuYWRqLnBpKSRjb2VmLCAzKVxuYGBgIn0= -->

```r
## deduced data
fit.adj.pi <- epi %>% filter(Treatment == "0Pi") %>% lm(median_adj ~ beta_6.8 + beta_8.10 +
                beta_6.8:beta_8.10,
              data = .)
round(summary(fit.adj.pi)$coef, 3)
```

<!-- rnb-source-end -->

<!-- rnb-output-begin eyJkYXRhIjoiICAgICAgICAgICAgICAgICAgIEVzdGltYXRlIFN0ZC4gRXJyb3IgdCB2YWx1ZSBQcig+fHR8KVxuKEludGVyY2VwdCkgICAgICAgICAgMjMuMTcyICAgICAgMC44MjIgIDI4LjE3NSAgICAwLjAwMFxuYmV0YV82LjggICAgICAgICAgICAgMTIuNTAyICAgICAgMS4yNTYgICA5Ljk1MSAgICAwLjAwMFxuYmV0YV84LjEwICAgICAgICAgICAgIDIuMzkzICAgICAgMS4wNjIgICAyLjI1NCAgICAwLjAyOVxuYmV0YV82Ljg6YmV0YV84LjEwICAgIDMuMTU0ICAgICAgMS43MTIgICAxLjg0MiAgICAwLjA3MlxuIn0= -->

```
                   Estimate Std. Error t value Pr(>|t|)
(Intercept)          23.172      0.822  28.175    0.000
beta_6.8             12.502      1.256   9.951    0.000
beta_8.10             2.393      1.062   2.254    0.029
beta_6.8:beta_8.10    3.154      1.712   1.842    0.072
```



<!-- rnb-output-end -->

<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuZml0LmFkai5veGkgPC0gZXBpICU+JSBmaWx0ZXIoVHJlYXRtZW50ID09IFwiMm1NSDJPMlwiKSAlPiUgbG0obWVkaWFuX2FkaiB+IGJldGFfNi44ICsgYmV0YV84LjEwICtcbiAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgIGJldGFfNi44OmJldGFfOC4xMCwgZGF0YSA9IC4pXG5yb3VuZChzdW1tYXJ5KGZpdC5hZGoub3hpKSRjb2VmLCAzKVxuYGBgIn0= -->

```r
fit.adj.oxi <- epi %>% filter(Treatment == "2mMH2O2") %>% lm(median_adj ~ beta_6.8 + beta_8.10 +
                                                               beta_6.8:beta_8.10, data = .)
round(summary(fit.adj.oxi)$coef, 3)
```

<!-- rnb-source-end -->

<!-- rnb-output-begin eyJkYXRhIjoiICAgICAgICAgICAgICAgICAgIEVzdGltYXRlIFN0ZC4gRXJyb3IgdCB2YWx1ZSBQcig+fHR8KVxuKEludGVyY2VwdCkgICAgICAgICAgNjQuODAxICAgICAgMS45MTIgIDMzLjg5MSAgICAwLjAwMFxuYmV0YV82LjggICAgICAgICAgICAgIDUuNjExICAgICAgMi44MTQgICAxLjk5NCAgICAwLjA1MVxuYmV0YV84LjEwICAgICAgICAgICAgMTQuMTkzICAgICAgMi40NjggICA1Ljc1MCAgICAwLjAwMFxuYmV0YV82Ljg6YmV0YV84LjEwICAgLTkuMDI0ICAgICAgNC4wMDYgIC0yLjI1MyAgICAwLjAyOVxuIn0= -->

```
                   Estimate Std. Error t value Pr(>|t|)
(Intercept)          64.801      1.912  33.891    0.000
beta_6.8              5.611      2.814   1.994    0.051
beta_8.10            14.193      2.468   5.750    0.000
beta_6.8:beta_8.10   -9.024      4.006  -2.253    0.029
```



<!-- rnb-output-end -->

<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuIyBDb25jbHVzaW9uOiBmb3IgdGhlIHBsYWV0ZWF1LCByZWdhcmRsZXNzIG9mIHRyZWF0bWVudCBhbmQgYmFzYWwgZXhwcmVzc2lvbiwgODAwLTEwMDAgYnBzIGFuZCA2MDAgdG8gODAwIGJwcyBoYXMgbm8gc2lnbmlmaWNhbnQgaW50ZXJhY3Rpb25cblxuIyMgaWYgY29tcGFyaW5nIElSXzYuMTAsIElSXzguMTAgYW5kIFdUIGNhbm5vdCBnaXZlIHRoZSBpbnRlcmFjdGlvbiB0LXRlc3QgcmVzdWx0XG5cbmBgYCJ9 -->

```r
# Conclusion: for the plaeteau, regardless of treatment and basal expression, 800-1000 bps and 600 to 800 bps has no significant interaction

## if comparing IR_6.10, IR_8.10 and WT cannot give the interaction t-test result

```

<!-- rnb-source-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->


### slope/differetiation of the loess curve

<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuIyBwbG90ICYgY2FsY3VsYXRlIHRoZSBzbG9wZS9kaWZmZXJpYXRpb24gY2hhbmdlcyBvZiBPTDotIFBpXG4jIGNoZWNrIHRoZSBub24tZHVwbGljYXRlZCBzdHJhaW4gbmFtZXNcbmNoZWNrLlRydW5WIDwtIHBpLlRydW5WLmRhdCAlPiUgIGdyb3VwX2J5KEdlbm90eXBlKSAlPiUgc3VtbWFyaXNlKFN0cmFpbiA9IHBhc3RlKHVuaXF1ZShTdHJhaW4pLCBjb2xsYXBzZSA9ICcsICcpKVxuXG4jIENhbiBwbGF5IHRoZSB0aGUgZ2Vub3R5cGUgbmFtZSB0byBwbG90IHRoZSBkaWZmKGxvZXNzIG1vZGVsKVxudGVzdC5waSA8LSBwaS5UcnVuVi5kYXQgJT4lIGZpbHRlcihHZW5vdHlwZSA9PSBcIjRWXCIpICU+JSBsb2Vzcyhmb3JtdWxhID0gbmV3X21lZGlhbiB+IG5ld190aW1lLCBzcGFuID0gMC43NSwgZGVncmVlID0gMikgXG5cbnggPC0gMDoyNDBcbnB4IDwtIHByZWRpY3QodGVzdC5waSwgbmV3ZGF0YSA9IHgpXG5weDEgPC0gZGlmZihweClcbndoaWNoLm1heChweDEpICMgZ2V0IHRoZSB4IHZhbHVlXG5tYXgocHgxKSAjIGVxdWFscyBweDFbd2hpY2gubWF4KHB4MSldXG5cbnBhcihtZnJvdz1jKDEsIDIpKVxucGxvdCh4LCBweCwgbWFpbj1cImxvZXNzIG1vZGVsXCIpXG5cbnBsb3QoeFstMV0sIHB4MSwgbWFpbj1cImRpZmYobG9lc3MgbW9kZWwpXCIpXG5hYmxpbmUodj13aGljaC5tYXgocHgxKSwgY29sPVwicmVkXCIpXG5cbiMgZ2V0IHRoZSBtYXggc2xvcGUgYW5kIHRoZSByZXNwZWN0aXZlIHRwIGZvciBlYWNoIHNhbXBsZSBpbnRvIGEgZGF0YWZyYW1lOiAtIFBpIFxucGkuVHJ1blYuc2xvcGUgPC0gZGF0YS5mcmFtZShtYXRyaXgobmNvbD0yLG5yb3c9MCwgZGltbmFtZXM9bGlzdChOVUxMLCBjKFwicGkuc2xvcGVcIiwgXCJHZW5vdHlwZVwiKSkpKVxucm93X2NudCA9IDFcbmNvbF9jbnQgPSAxXG5mb3IgKHggaW4gbmFtZXMobGV2ZWxzKSkge1xuICB0bXAucGkgPC0gcGkuVHJ1blYuZGF0ICU+JSBmaWx0ZXIoR2Vub3R5cGUgPT0geClcbiMgZ2V0IHRoZSBsb2VzcyBmdW5jdGlvblxuICBmb3IgKHkgaW4gdW5pcXVlKHBpLlRydW5WLmRhdCRyZXBsaWNhdGUpKSB7XG4gICAgdGVzdC5waSA8LSB0bXAucGkgJT4lIGZpbHRlcihyZXBsaWNhdGUgPT0geSkgXG4gICAgZm9yICh6IGluIHVuaXF1ZSh0ZXN0LnBpJFN0cmFpbikpIHtcbiAgICAgIGZpbmFsLnBpIDwtIHRlc3QucGkgJT4lIGZpbHRlcihTdHJhaW4gPT0geikgJT4lIGxvZXNzKGZvcm11bGEgPSBuZXdfbWVkaWFuIH4gbmV3X3RpbWUsIHNwYW4gPSAwLjc1LCBkZWdyZWUgPSAyKVxuICAgICAgeF92YXIgPC0gMDoyNDBcbiAgICAgIHB4IDwtIHByZWRpY3QoZmluYWwucGksIG5ld2RhdGEgPSB4X3ZhcilcbiAgICAgICMgcGVyZm9ybSBkaWZmZXJlbnRpYXRpb25cbiAgICAgIHRtcCA8LSBtYXgoZGlmZihweCkpXG4gICAgICBndF90bXAgPC0geFxuICAgICAgcGkuVHJ1blYuc2xvcGVbcm93X2NudCxjb2xfY250XSA8LSB0bXBcbiAgICAgIGNvbF9jbnQgPSBjb2xfY250ICsgMVxuICAgICAgcGkuVHJ1blYuc2xvcGVbcm93X2NudCxjb2xfY250XSA8LSBndF90bXBcbiAgICAgIGNvbF9jbnQgPSAxXG4gICAgICByb3dfY250ID0gcm93X2NudCArIDFcbiAgICB9fX1cblxuXG5waS5UcnVuVi5zbG9wZSA8LSBwaS5UcnVuVi5zbG9wZSAlPiUgbXV0YXRlKEdlbm90eXBlID0gZmFjdG9yKEdlbm90eXBlLCBsZXZlbHMgPSBjKFwiV1RcIixcIlBDXCIsIFwiMlZcIiwgXCI0VlwiLFwiNlZcIixcIjhWXCIpKSkgXG5cbiMgcGxvdCB0aGUgc2xvcGUgb2YgdGhlIGN1cnZlOiAtIFBpXG5waS5UcnVuVi5zbG9wZSAlPiUgXG4gIGZpbHRlcighaXMubmEocGkuc2xvcGUpLCBHZW5vdHlwZSAhPSBcIlBDXCIpICU+JSBcbiAgZ2dwbG90KGFlcyh4ID0gR2Vub3R5cGUsIHkgPSBwaS5zbG9wZSwgY29sb3IgPSBHZW5vdHlwZSkpICsgYmFyLmxpc3QgK1xuICBnZW9tX2JveHBsb3QoKSArXG4gIHN0YXRfc3VtbWFyeShmdW4uZGF0YSA9IFwibWVhbl9jbF9ib290XCIsIGNvbG9yID0gXCJSZWRcIiwgbGluZXdpZHRoID0gMSwgc2l6ZSA9IDAuOCkgK1xuICBnZW9tX2ppdHRlcih3aWR0aCA9IDAuMikgK1xuICB0aGVtZShsZWdlbmQucG9zaXRpb249YygwLjg1LDAuOSkpICtcbiAgc2NhbGVfY29sb3JfdmlyaWRpc19kKGxpbWl0cyA9IG5hbWVzKGxldmVscy5ub3Jlc2N1ZSksIG9wdGlvbiA9IFwicGxhc21hXCIpICtcbiAgdGhlbWUobGVnZW5kLnBvc2l0aW9uPWMoMC44NSwwLjkpKSArXG4gIHlsYWIoXCJNYXhpbXVtIFNsb3BlIChsb2VzcyBmaXQpXCIpICtcbiAgeGxhYihcIlRydW5jYXRpb24gVmFyaWFudHMsIDBtTSBQaVwiKVxuI2dnc2F2ZShcIm91dHB1dC9UcnVuVl9zbG9wZV8wUGkucG5nXCIsIHdpZHRoID0gNiwgaGVpZ2h0ID0gOClcblxuXG4jIGdldCB0aGUgbWF4IHNsb3BlIGFuZCB0aGUgcmVzcGVjdGl2ZSB0cCBmb3IgZWFjaCBzYW1wbGUgaW50byBhIGRhdGFmcmFtZTogMm1NIEgyTzIgXG5veGkuVHJ1blYuc2xvcGUgPC0gZGF0YS5mcmFtZShtYXRyaXgobmNvbD0yLG5yb3c9MCwgZGltbmFtZXM9bGlzdChOVUxMLCBjKFwib3hpLnNsb3BlXCIsIFwiR2Vub3R5cGVcIikpKSlcbnJvd19jbnQgPSAxXG5jb2xfY250ID0gMVxuZm9yICh4IGluIG5hbWVzKGxldmVscykpIHtcbiAgdG1wLm94aSA8LSBveGkuVHJ1blYuZGF0ICU+JSBmaWx0ZXIoR2Vub3R5cGUgPT0geClcbiMgZ2V0IHRoZSBsb2VzcyBmdW5jdGlvblxuICBmb3IgKHkgaW4gdW5pcXVlKG94aS5UcnVuVi5kYXQkcmVwbGljYXRlKSkge1xuICAgIHRlc3Qub3hpIDwtIHRtcC5veGkgJT4lIGZpbHRlcihyZXBsaWNhdGUgPT0geSkgXG4gICAgZm9yICh6IGluIHVuaXF1ZSh0ZXN0Lm94aSRTdHJhaW4pKSB7XG4gICAgICBmaW5hbC5veGkgPC0gdGVzdC5veGkgJT4lIGZpbHRlcihTdHJhaW4gPT0geikgJT4lIGxvZXNzKGZvcm11bGEgPSBuZXdfbWVkaWFuIH4gbmV3X3RpbWUsIHNwYW4gPSAwLjc1LCBkZWdyZWUgPSAyKVxuICAgICAgeF92YXIgPC0gMDoyNDBcbiAgICAgIHB4IDwtIHByZWRpY3QoZmluYWwub3hpLCBuZXdkYXRhID0geF92YXIpXG4gICAgICAjIHBlcmZvcm0gZGlmZmVyZW50aWF0aW9uXG4gICAgICB0bXAgPC0gbWF4KGRpZmYocHgpKVxuICAgICAgZ3RfdG1wIDwtIHhcbiAgICAgIG94aS5UcnVuVi5zbG9wZVtyb3dfY250LGNvbF9jbnRdIDwtIHRtcFxuICAgICAgY29sX2NudCA9IGNvbF9jbnQgKyAxXG4gICAgICBveGkuVHJ1blYuc2xvcGVbcm93X2NudCxjb2xfY250XSA8LSBndF90bXBcbiAgICAgIGNvbF9jbnQgPSAxXG4gICAgICByb3dfY250ID0gcm93X2NudCArIDFcbiAgICB9fX1cblxuXG5veGkuVHJ1blYuc2xvcGUgPC0gb3hpLlRydW5WLnNsb3BlICU+JSBtdXRhdGUoR2Vub3R5cGUgPSBmYWN0b3IoR2Vub3R5cGUsIGxldmVscyA9IGMoXCJXVFwiLFwiUENcIiwgXCIyVlwiLFwiNFZcIixcIjZWXCIsIFwiOFZcIikpKSBcblxuIyBwbG90IHRoZSBzbG9wZSBvZiB0aGUgY3VydmU6IC0gUGlcbm94aS5UcnVuVi5zbG9wZSAlPiUgXG4gIGZpbHRlcighaXMubmEob3hpLnNsb3BlKSwgR2Vub3R5cGUgIT0gXCJQQ1wiKSAlPiUgXG4gIGdncGxvdChhZXMoeCA9IEdlbm90eXBlLCB5ID0gb3hpLnNsb3BlLCBjb2xvciA9IEdlbm90eXBlKSkgKyBiYXIubGlzdCArXG4gIGdlb21fYm94cGxvdCgpICtcbiAgc3RhdF9zdW1tYXJ5KGZ1bi5kYXRhID0gXCJtZWFuX2NsX2Jvb3RcIiwgY29sb3IgPSBcIlJlZFwiLCBsaW5ld2lkdGggPSAxLCBzaXplID0gMC44KSArXG4gIGdlb21faml0dGVyKHdpZHRoID0gMC4yKSArXG4gIHRoZW1lKGxlZ2VuZC5wb3NpdGlvbj1jKDAuODUsMC45KSkgK1xuICBzY2FsZV9jb2xvcl92aXJpZGlzX2QobGltaXRzID0gbmFtZXMobGV2ZWxzLm5vcmVzY3VlKSwgb3B0aW9uID0gXCJwbGFzbWFcIikgK1xuICB5bGFiKFwiTWF4aW11bSBTbG9wZSAobG9lc3MgZml0KVwiKSArXG4gIHhsYWIoXCJUcnVuY2F0aW9uIFZhcmlhbnRzLCAybU0gSDJPMlwiKVxuI2dnc2F2ZShcIm91dHB1dC9UcnVuVl9zbG9wZV9veGkucG5nXCIsIHdpZHRoID0gNiwgaGVpZ2h0ID0gOClcblxuYGBgIn0= -->

```r
# plot & calculate the slope/differiation changes of OL:- Pi
# check the non-duplicated strain names
check.TrunV <- pi.TrunV.dat %>%  group_by(Genotype) %>% summarise(Strain = paste(unique(Strain), collapse = ', '))

# Can play the the genotype name to plot the diff(loess model)
test.pi <- pi.TrunV.dat %>% filter(Genotype == "4V") %>% loess(formula = new_median ~ new_time, span = 0.75, degree = 2) 

x <- 0:240
px <- predict(test.pi, newdata = x)
px1 <- diff(px)
which.max(px1) # get the x value
max(px1) # equals px1[which.max(px1)]

par(mfrow=c(1, 2))
plot(x, px, main="loess model")

plot(x[-1], px1, main="diff(loess model)")
abline(v=which.max(px1), col="red")

# get the max slope and the respective tp for each sample into a dataframe: - Pi 
pi.TrunV.slope <- data.frame(matrix(ncol=2,nrow=0, dimnames=list(NULL, c("pi.slope", "Genotype"))))
row_cnt = 1
col_cnt = 1
for (x in names(levels)) {
  tmp.pi <- pi.TrunV.dat %>% filter(Genotype == x)
# get the loess function
  for (y in unique(pi.TrunV.dat$replicate)) {
    test.pi <- tmp.pi %>% filter(replicate == y) 
    for (z in unique(test.pi$Strain)) {
      final.pi <- test.pi %>% filter(Strain == z) %>% loess(formula = new_median ~ new_time, span = 0.75, degree = 2)
      x_var <- 0:240
      px <- predict(final.pi, newdata = x_var)
      # perform differentiation
      tmp <- max(diff(px))
      gt_tmp <- x
      pi.TrunV.slope[row_cnt,col_cnt] <- tmp
      col_cnt = col_cnt + 1
      pi.TrunV.slope[row_cnt,col_cnt] <- gt_tmp
      col_cnt = 1
      row_cnt = row_cnt + 1
    }}}


pi.TrunV.slope <- pi.TrunV.slope %>% mutate(Genotype = factor(Genotype, levels = c("WT","PC", "2V", "4V","6V","8V"))) 

# plot the slope of the curve: - Pi
pi.TrunV.slope %>% 
  filter(!is.na(pi.slope), Genotype != "PC") %>% 
  ggplot(aes(x = Genotype, y = pi.slope, color = Genotype)) + bar.list +
  geom_boxplot() +
  stat_summary(fun.data = "mean_cl_boot", color = "Red", linewidth = 1, size = 0.8) +
  geom_jitter(width = 0.2) +
  theme(legend.position=c(0.85,0.9)) +
  scale_color_viridis_d(limits = names(levels.norescue), option = "plasma") +
  theme(legend.position=c(0.85,0.9)) +
  ylab("Maximum Slope (loess fit)") +
  xlab("Truncation Variants, 0mM Pi")
#ggsave("output/TrunV_slope_0Pi.png", width = 6, height = 8)


# get the max slope and the respective tp for each sample into a dataframe: 2mM H2O2 
oxi.TrunV.slope <- data.frame(matrix(ncol=2,nrow=0, dimnames=list(NULL, c("oxi.slope", "Genotype"))))
row_cnt = 1
col_cnt = 1
for (x in names(levels)) {
  tmp.oxi <- oxi.TrunV.dat %>% filter(Genotype == x)
# get the loess function
  for (y in unique(oxi.TrunV.dat$replicate)) {
    test.oxi <- tmp.oxi %>% filter(replicate == y) 
    for (z in unique(test.oxi$Strain)) {
      final.oxi <- test.oxi %>% filter(Strain == z) %>% loess(formula = new_median ~ new_time, span = 0.75, degree = 2)
      x_var <- 0:240
      px <- predict(final.oxi, newdata = x_var)
      # perform differentiation
      tmp <- max(diff(px))
      gt_tmp <- x
      oxi.TrunV.slope[row_cnt,col_cnt] <- tmp
      col_cnt = col_cnt + 1
      oxi.TrunV.slope[row_cnt,col_cnt] <- gt_tmp
      col_cnt = 1
      row_cnt = row_cnt + 1
    }}}


oxi.TrunV.slope <- oxi.TrunV.slope %>% mutate(Genotype = factor(Genotype, levels = c("WT","PC", "2V","4V","6V", "8V"))) 

# plot the slope of the curve: - Pi
oxi.TrunV.slope %>% 
  filter(!is.na(oxi.slope), Genotype != "PC") %>% 
  ggplot(aes(x = Genotype, y = oxi.slope, color = Genotype)) + bar.list +
  geom_boxplot() +
  stat_summary(fun.data = "mean_cl_boot", color = "Red", linewidth = 1, size = 0.8) +
  geom_jitter(width = 0.2) +
  theme(legend.position=c(0.85,0.9)) +
  scale_color_viridis_d(limits = names(levels.norescue), option = "plasma") +
  ylab("Maximum Slope (loess fit)") +
  xlab("Truncation Variants, 2mM H2O2")
#ggsave("output/TrunV_slope_oxi.png", width = 6, height = 8)

```

<!-- rnb-source-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->



<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuIyMjIyMgMm1NIEgyTzIgT0wgdGltZXBvaW50IHBsb3QgZnVuY3Rpb25cbnRwX0dGUCA8LSBmdW5jdGlvbiguLi4pe1xuICBcbiAgYWxsX3RwIDwtIGxpc3QoLi4uKVxuICBmb3IgKGlucHV0X3RwIGluIGFsbF90cCkgeyAgIFxuICBcbiAgICBkZl90cCA8LSBveGkuVHJ1blYuZGF0ICU+JSBmaWx0ZXIobmV3X3RpbWUgPT0gaW5wdXRfdHApICU+JSBtdXRhdGUoZ2Vub3R5cGUgPSBmYWN0b3IoZ2Vub3R5cGUsIGxldmVscyA9IGxldmVscykpXG4gICAgXG4gICAgcHJpbnQoZ2dwbG90KGRmX3RwLCBhZXMoeCA9IGdlbm90eXBlLCB5ID0gbmV3X21lZGlhbiwgZmlsbCA9IEdlbm90eXBlKSkgKyBcbiAgICBnZW9tX3BvaW50KCkgK1xuICAgIHN0YXRfc3VtbWFyeShmdW4uZGF0YSA9IFwibWVhbl9jbF9ib290XCIsIGNvbmYuaW50ID0gLjk1LCBjb2xvciA9IFwiUmVkXCIsIGxpbmV3aWR0aCA9IDEsIHNpemUgPSAwLjgpICtcbiAgICBsYWJzKHggPXBhc3RlMChcIjJtTSBIMk8yLCBPTCB2YXJpYW50cyBcIiwgZGVwYXJzZTEoc3Vic3RpdHV0ZShpbnB1dF90cCkpLCBcIiBtaW5cIiksIHkgPSBcIkN0YTEtR0ZQIHByb3RlaW4gbGV2ZWwgKGEudS4pXCIpICtcbiAgICB0aGVtZV9jb3dwbG90KGxpbmVfc2l6ZSA9IDAuNywgZm9udF9zaXplID0gMTQpICtcbiAgICB0aGVtZShsZWdlbmQucG9zaXRpb24gPSBcIm5vbmVcIixcbiAgICAgICAgICBheGlzLnRpdGxlID0gZWxlbWVudF90ZXh0KHNpemUgPSByZWwoMSkpLCBcbiAgICAgICAgICBheGlzLnRleHQueCA9IGVsZW1lbnRfdGV4dChoanVzdD0wLjUpLCBheGlzLnRleHQgPSBlbGVtZW50X3RleHQoc2l6ZSA9IHJlbCgxKSksKSlcbiAgfVxufVxuXG4jIHBsb3QgdGhlIDJtTSBIMk8yIE9MIHZhcmlhbnRzIGF0IDBtaW4sIDkwbWluLCAxMjBtaW4gdGltZXBvaW50c1xuXG50cF9HRlAoMCw5MCwxMjAsMjQwKVxuXG5gYGAifQ== -->

```r
##### 2mM H2O2 OL timepoint plot function
tp_GFP <- function(...){
  
  all_tp <- list(...)
  for (input_tp in all_tp) {   
  
    df_tp <- oxi.TrunV.dat %>% filter(new_time == input_tp) %>% mutate(genotype = factor(genotype, levels = levels))
    
    print(ggplot(df_tp, aes(x = genotype, y = new_median, fill = Genotype)) + 
    geom_point() +
    stat_summary(fun.data = "mean_cl_boot", conf.int = .95, color = "Red", linewidth = 1, size = 0.8) +
    labs(x =paste0("2mM H2O2, OL variants ", deparse1(substitute(input_tp)), " min"), y = "Cta1-GFP protein level (a.u.)") +
    theme_cowplot(line_size = 0.7, font_size = 14) +
    theme(legend.position = "none",
          axis.title = element_text(size = rel(1)), 
          axis.text.x = element_text(hjust=0.5), axis.text = element_text(size = rel(1)),))
  }
}

# plot the 2mM H2O2 OL variants at 0min, 90min, 120min timepoints

tp_GFP(0,90,120,240)

```

<!-- rnb-source-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->

** Truncation variants**
#### Get the loess curve fitting for the timecourse data

<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuIyBuZWVkIG5hbWVzIGNvbG9yc1xuZ2Vub3R5cGVfY29sb3IgPC0gUkNvbG9yQnJld2VyOjpicmV3ZXIucGFsKDgsIFwiRGFyazJcIilbYyg4LCA3LCA2LCAxLCA1LCA0LCAyKV0gXG5uYW1lcyhnZW5vdHlwZV9jb2xvcikgPC0gbmFtZXMobGV2ZWxzKVxuXG4jIGNoZWNrIGZvciB0aGUgbG9zcyBmaXQgY3VydmVcbnBpLm1vZGVsIDwtIHBpLlRydW5WLmRhdCAgJT4lICAgXG5ncm91cF9ieShHZW5vdHlwZSkgJT4lXG5tdXRhdGUobW9kZWwgPSBsb2VzcyhtZWRpYW4gfiBuZXdfdGltZSwgc3BhbiA9IDAuNzUsIGRlZ3JlZSA9IDIpJGZpdHRlZClcblxuaDJvMi5tb2RlbCA8LSBveGkuVHJ1blYuZGF0ICAlPiUgICBcbmdyb3VwX2J5KEdlbm90eXBlKSAlPiVcbm11dGF0ZShtb2RlbCA9IGxvZXNzKG1lZGlhbiB+IG5ld190aW1lLCBzcGFuID0gMC43NSwgZGVncmVlID0gMikkZml0dGVkKVxuXG5waS5tb2RlbCAlPiUgZ2dwbG90KGFlcyh4ID0gbmV3X3RpbWUsIHkgPSBuZXdfbWVkaWFuLCBjb2xvciA9IEdlbm90eXBlKSkgKyBtZWFuLnRpbWVjb3Vyc2UgKyBzY2FsZV9jb2xvcl9tYW51YWwodmFsdWVzPSBnZW5vdHlwZV9jb2xvciwgbGltaXRzID0gbmFtZXMoZ2Vub3R5cGVfY29sb3IpKSArXG4gIGxhYnMoeCA9IFwiUGhvc3BoYXRlIHN0YXJ2YXRpb24sIFRpbWUgKG1pbilcIilcbiNnZ3NhdmUoXCJvdXRwdXQvbG9lc3NfVHJ1blZfMFBpLnBuZ1wiLCB3aWR0aCA9IDYuMywgaGVpZ2h0ID0gOClcblxuaDJvMi5tb2RlbCAlPiUgZ2dwbG90KGFlcyh4ID0gbmV3X3RpbWUsIHkgPSBuZXdfbWVkaWFuLCBjb2xvciA9IEdlbm90eXBlKSkgKyBtZWFuLnRpbWVjb3Vyc2UgKyBzY2FsZV9jb2xvcl9tYW51YWwodmFsdWVzPSBnZW5vdHlwZV9jb2xvciwgbGltaXRzID0gbmFtZXMoZ2Vub3R5cGVfY29sb3IpKSArXG5sYWJzKHggPSBcIjJtTSBIMk8yLCBUaW1lIChtaW4pXCIpXG4jZ2dzYXZlKFwib3V0cHV0L2xvZXNzX1RydW5WXzJtTUgyTzIucG5nXCIsIHdpZHRoID0gNi4zLCBoZWlnaHQgPSA4KVxuXG5cbiMjIGdldCBBVUMgZm9yIC0gUGkgZGF0YSBpbnRvIGEgZGF0YWZyYW1lXG5waS5hcmVhIDwtIGRhdGEuZnJhbWUobWF0cml4KG5jb2w9Mixucm93PTAsIGRpbW5hbWVzPWxpc3QoTlVMTCwgYyhcInBpLmFyZWFcIiwgXCJHZW5vdHlwZVwiKSkpKVxucm93X2NudCA9IDFcbmNvbF9jbnQgPSAxXG5mb3IgKHggaW4gbmFtZXMoZ2Vub3R5cGVfY29sb3IpKSB7XG4jIGNhbGN1bGF0ZSBBVUMgIFxubWFkZXVwLnBpIDwtIHBpLm1vZGVsICU+JSBmaWx0ZXIoR2Vub3R5cGUgPT0geCkgJT4lIGxvZXNzKGZvcm11bGEgPSBuZXdfbWVkaWFuIH4gbmV3X3RpbWUsIHNwYW4gPSAwLjc1LCBkZWdyZWUgPSAyKSBcbmYgPC0gZnVuY3Rpb24oeCkgcHJlZGljdChtYWRldXAucGksbmV3ZGF0YT14KVxuIyBwZXJmb3JtIGludGVncmF0aW9uXG50bXAgPC0gaW50ZWdyYXRlKGYsMCwyNDApJHZhbHVlXG5ndF90bXAgPC0geFxucGkuYXJlYVtyb3dfY250LGNvbF9jbnRdIDwtIHRtcFxuY29sX2NudCA9IGNvbF9jbnQgKyAxXG5waS5hcmVhW3Jvd19jbnQsY29sX2NudF0gPC0gZ3RfdG1wXG5jb2xfY250ID0gMVxucm93X2NudCA9IHJvd19jbnQgKyAxXG59XG5cblxuXG4jIGdldCBBVUMgZm9yIDJtTSBIMk8yIGRhdGFcbmgybzIuYXJlYSA8LSBkYXRhLmZyYW1lKG1hdHJpeChuY29sPTIsbnJvdz0wLCBkaW1uYW1lcz1saXN0KE5VTEwsIGMoXCJoMm8yLmFyZWFcIiwgXCJHZW5vdHlwZVwiKSkpKVxucm93X2NudCA9IDFcbmNvbF9jbnQgPSAxXG5mb3IgKHggaW4gbmFtZXMoZ2Vub3R5cGVfY29sb3IpKSB7XG4jIGNhbGN1bGF0ZSBBVUMgIFxubWFkZXVwLmgybzIgPC0gaDJvMi5tb2RlbCAlPiUgZmlsdGVyKEdlbm90eXBlID09IHgpICU+JSBsb2Vzcyhmb3JtdWxhID0gbmV3X21lZGlhbiB+IG5ld190aW1lLCBzcGFuID0gMC43NSwgZGVncmVlID0gMikgXG5mIDwtIGZ1bmN0aW9uKHgpIHByZWRpY3QobWFkZXVwLmgybzIsbmV3ZGF0YT14KVxuIyBwZXJmb3JtIGludGVncmF0aW9uXG50bXAgPC0gaW50ZWdyYXRlKGYsMCwyNDApJHZhbHVlXG5ndF90bXAgPC0geFxuaDJvMi5hcmVhW3Jvd19jbnQsY29sX2NudF0gPC0gdG1wXG5jb2xfY250ID0gY29sX2NudCArIDFcbmgybzIuYXJlYVtyb3dfY250LGNvbF9jbnRdIDwtIGd0X3RtcFxuY29sX2NudCA9IDFcbnJvd19jbnQgPSByb3dfY250ICsgMVxufVxuXG4jIGNvbWJpbmQgYXJlYSBkYXRhXG5hcmVhIDwtIG1lcmdlKHBpLmFyZWEsaDJvMi5hcmVhKVxuYGBgIn0= -->

```r
# need names colors
genotype_color <- RColorBrewer::brewer.pal(8, "Dark2")[c(8, 7, 6, 1, 5, 4, 2)] 
names(genotype_color) <- names(levels)

# check for the loss fit curve
pi.model <- pi.TrunV.dat  %>%   
group_by(Genotype) %>%
mutate(model = loess(median ~ new_time, span = 0.75, degree = 2)$fitted)

h2o2.model <- oxi.TrunV.dat  %>%   
group_by(Genotype) %>%
mutate(model = loess(median ~ new_time, span = 0.75, degree = 2)$fitted)

pi.model %>% ggplot(aes(x = new_time, y = new_median, color = Genotype)) + mean.timecourse + scale_color_manual(values= genotype_color, limits = names(genotype_color)) +
  labs(x = "Phosphate starvation, Time (min)")
#ggsave("output/loess_TrunV_0Pi.png", width = 6.3, height = 8)

h2o2.model %>% ggplot(aes(x = new_time, y = new_median, color = Genotype)) + mean.timecourse + scale_color_manual(values= genotype_color, limits = names(genotype_color)) +
labs(x = "2mM H2O2, Time (min)")
#ggsave("output/loess_TrunV_2mMH2O2.png", width = 6.3, height = 8)


## get AUC for - Pi data into a dataframe
pi.area <- data.frame(matrix(ncol=2,nrow=0, dimnames=list(NULL, c("pi.area", "Genotype"))))
row_cnt = 1
col_cnt = 1
for (x in names(genotype_color)) {
# calculate AUC  
madeup.pi <- pi.model %>% filter(Genotype == x) %>% loess(formula = new_median ~ new_time, span = 0.75, degree = 2) 
f <- function(x) predict(madeup.pi,newdata=x)
# perform integration
tmp <- integrate(f,0,240)$value
gt_tmp <- x
pi.area[row_cnt,col_cnt] <- tmp
col_cnt = col_cnt + 1
pi.area[row_cnt,col_cnt] <- gt_tmp
col_cnt = 1
row_cnt = row_cnt + 1
}



# get AUC for 2mM H2O2 data
h2o2.area <- data.frame(matrix(ncol=2,nrow=0, dimnames=list(NULL, c("h2o2.area", "Genotype"))))
row_cnt = 1
col_cnt = 1
for (x in names(genotype_color)) {
# calculate AUC  
madeup.h2o2 <- h2o2.model %>% filter(Genotype == x) %>% loess(formula = new_median ~ new_time, span = 0.75, degree = 2) 
f <- function(x) predict(madeup.h2o2,newdata=x)
# perform integration
tmp <- integrate(f,0,240)$value
gt_tmp <- x
h2o2.area[row_cnt,col_cnt] <- tmp
col_cnt = col_cnt + 1
h2o2.area[row_cnt,col_cnt] <- gt_tmp
col_cnt = 1
row_cnt = row_cnt + 1
}

# combind area data
area <- merge(pi.area,h2o2.area)
```

<!-- rnb-source-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->


#### Check the loess fitting assumption: normality and curve fitting

<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->



<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->


### regulatory information map

<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuIyBjYWxjdWxhdGUgdGhlIHJlbGF0aXZlIGluZm9ybWF0aW9uIHJldGFpbmluZyB3aXRoaW4gZWFjaCBnZW5vdHlwZVxucmVnX2luZm8gPC0gYXJlYSAlPiUgXG4gIG11dGF0ZShwaV9wY250ID0gcGkuYXJlYS8oLlsuJEdlbm90eXBlID09IFwiV1RcIixdJHBpLmFyZWEpKSAlPiUgXG4gIG11dGF0ZShoMm8yX3BjbnQgPSBoMm8yLmFyZWEvKCguWy4kR2Vub3R5cGUgPT0gXCJXVFwiLF0kaDJvMi5hcmVhKSkpXG5cbnJlZ19pbmZvICU+JSBcbiAgZ2dwbG90KGFlcyh4ID0gcGlfcGNudCwgeSA9IGgybzJfcGNudCksIGNvbG9yID0gR2Vub3R5cGUpICtcbiAgc2NhdHRlciArIFxuICBnZW9tX3BvaW50KHNpemUgPSAzLCBhZXMoY29sb3IgPSBHZW5vdHlwZSkpICtcbiAgZ2VvbV9hYmxpbmUoc2xvcGUgPSAxLCBpbnRlcmNlcHQgPSAwLCBsaW5ldHlwZSA9IFwiZGFzaGVkXCIsIGNvbG9yID0gXCIjNjY2NjY2XCIpICtcbiAgbGFicyh4ID0gXCJQaSAocmVsYXRpdmUgdG8gd3QpXCIsIHkgPSBcIkgyTzIgKHJlbGF0aXZlIHRvIHd0KVwiKSArXG4gIHNjYWxlX2NvbG9yX21hbnVhbCh2YWx1ZXMgPSBnZW5vdHlwZV9jb2xvciwgbGltaXRzID0gbmFtZXMoZ2Vub3R5cGVfY29sb3IpKVxuI2dnc2F2ZShcIm91dHB1dC9UcnVuVnZzd3RfMHBpdnNoMm8yX3NjYXR0ZXIucG5nXCIsIHdpZHRoID0gNi4zLCBoZWlnaHQgPSA2LjMpXG5gYGAifQ== -->

```r
# calculate the relative information retaining within each genotype
reg_info <- area %>% 
  mutate(pi_pcnt = pi.area/(.[.$Genotype == "WT",]$pi.area)) %>% 
  mutate(h2o2_pcnt = h2o2.area/((.[.$Genotype == "WT",]$h2o2.area)))

reg_info %>% 
  ggplot(aes(x = pi_pcnt, y = h2o2_pcnt), color = Genotype) +
  scatter + 
  geom_point(size = 3, aes(color = Genotype)) +
  geom_abline(slope = 1, intercept = 0, linetype = "dashed", color = "#666666") +
  labs(x = "Pi (relative to wt)", y = "H2O2 (relative to wt)") +
  scale_color_manual(values = genotype_color, limits = names(genotype_color))
#ggsave("output/TrunVvswt_0pivsh2o2_scatter.png", width = 6.3, height = 6.3)
```

<!-- rnb-source-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->






**test code**
**_1st Differential derivative (Slope) for each curve_**

<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxud3QudGVzdCA8LSBveGkuZGF0ICU+JSBmaWx0ZXIoZ2Vub3R5cGUgJWluJSBjKFwid3RcIikpXG5cbmZpdC53dCA8LSBsb2VzcyhuZXdfbWVkaWFufm5ld190aW1lLCBkYXRhPXd0LnRlc3QpXG5cbnggPC0gMDoyNDBcbnB4IDwtIHByZWRpY3QoZml0Lnd0LCBuZXdkYXRhID0geClcbnB4MSA8LSBkaWZmKHB4KVxuI3doaWNoLm1heChweDEpXG5cbnd0LmxvZXNzIDwtIHRpYmJsZSh4ID0geCwgeSA9IHB4KVxud3QuZGlmZiA8LSB0aWJibGUgKHggPSB4Wy0xXSwgeSA9IHB4MSlcblxudHdvVi50ZXN0IDwtIG94aS5kYXQgJT4lIGZpbHRlcihnZW5vdHlwZSAlaW4lIGMoXCIyVlwiKSlcblxuZml0LnR3b1YgPC0gbG9lc3MobmV3X21lZGlhbn5uZXdfdGltZSwgZGF0YT10d29WLnRlc3QpXG5cbnggPC0gMDoyNDBcbnB4LjJWIDwtIHByZWRpY3QoZml0LnR3b1YsIG5ld2RhdGEgPSB4KVxucHgxLjJWIDwtIGRpZmYocHguMlYpXG5cbnR3b1YubG9lc3MgPC0gdGliYmxlKHggPSB4LCB5ID0gcHguMlYpXG50d29WLmRpZmYgPC0gdGliYmxlICh4ID0geFstMV0sIHkgPSBweDEuMlYpXG5cbnBhcihtZnJvdz1jKDEsIDQpKVxud3QubG9lc3MgJT4lIFxuZ2dwbG90KGFlcyh4ID0geCwgeSA9IHkpKSArIGdlb21fcG9pbnQoc2l6ZSA9IDEsIGFscGhhID0gMC41KSArIHNjYWxlX3hfY29udGludW91cyhicmVha3MgPSBzZXEoMCwyNDAsMzApKSArIHRoZW1lX2J3KCkgKyBnZ3RpdGxlKFwibG9lc3MgbW9kZWxcIilcblxud3QuZGlmZiAlPiUgXG4gIGdncGxvdChhZXMoeCA9IHgsIHkgPSB5KSkgKyBnZW9tX3BvaW50KHNpemUgPSAxLCBhbHBoYSA9IDAuNSkrIHNjYWxlX3hfY29udGludW91cyhicmVha3MgPSBzZXEoMCwgMjQwLCAzMCkpICsgdGhlbWVfYncoKSArIGdndGl0bGUoXCJkaWZmKGxvZXNzIG1vZGVsKVwiKVxuXG5cbnR3b1YubG9lc3MgJT4lIFxuZ2dwbG90KGFlcyh4ID0geCwgeSA9IHkpKSArIGdlb21fcG9pbnQoc2l6ZSA9IDEsIGFscGhhID0gMC41KSArIHNjYWxlX3hfY29udGludW91cyhicmVha3MgPSBzZXEoMCwyNDAsMzApKSArIHRoZW1lX2J3KCkgKyBnZ3RpdGxlKFwibG9lc3MgbW9kZWxcIilcblxudHdvVi5kaWZmICU+JSBcbiAgZ2dwbG90KGFlcyh4ID0geCwgeSA9IHkpKSArIGdlb21fcG9pbnQoc2l6ZSA9IDEsIGFscGhhID0gMC41KSsgc2NhbGVfeF9jb250aW51b3VzKGJyZWFrcyA9IHNlcSgwLCAyNDAsIDMwKSkgKyB0aGVtZV9idygpICsgZ2d0aXRsZShcImRpZmYobG9lc3MgbW9kZWwpXCIpXG5cblxuYGBgIn0= -->

```r
wt.test <- oxi.dat %>% filter(genotype %in% c("wt"))

fit.wt <- loess(new_median~new_time, data=wt.test)

x <- 0:240
px <- predict(fit.wt, newdata = x)
px1 <- diff(px)
#which.max(px1)

wt.loess <- tibble(x = x, y = px)
wt.diff <- tibble (x = x[-1], y = px1)

twoV.test <- oxi.dat %>% filter(genotype %in% c("2V"))

fit.twoV <- loess(new_median~new_time, data=twoV.test)

x <- 0:240
px.2V <- predict(fit.twoV, newdata = x)
px1.2V <- diff(px.2V)

twoV.loess <- tibble(x = x, y = px.2V)
twoV.diff <- tibble (x = x[-1], y = px1.2V)

par(mfrow=c(1, 4))
wt.loess %>% 
ggplot(aes(x = x, y = y)) + geom_point(size = 1, alpha = 0.5) + scale_x_continuous(breaks = seq(0,240,30)) + theme_bw() + ggtitle("loess model")

wt.diff %>% 
  ggplot(aes(x = x, y = y)) + geom_point(size = 1, alpha = 0.5)+ scale_x_continuous(breaks = seq(0, 240, 30)) + theme_bw() + ggtitle("diff(loess model)")


twoV.loess %>% 
ggplot(aes(x = x, y = y)) + geom_point(size = 1, alpha = 0.5) + scale_x_continuous(breaks = seq(0,240,30)) + theme_bw() + ggtitle("loess model")

twoV.diff %>% 
  ggplot(aes(x = x, y = y)) + geom_point(size = 1, alpha = 0.5)+ scale_x_continuous(breaks = seq(0, 240, 30)) + theme_bw() + ggtitle("diff(loess model)")

```

<!-- rnb-source-end -->

<!-- rnb-chunk-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuZml0Lnd0JFxuXG5cbmBgYCJ9 -->

```r
fit.wt$

```

<!-- rnb-source-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->




**_Statistical test_**

1. Basal level

<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuIyBmaWx0ZXIgdGhlIGRhdGEgYW5kIHNldCB0aGUgYmFzYWwgbGV2ZWxcbmdlbm90eXBlX29yZGVyIDwtIG5hbWVzKGxldmVscylcblxudG1wIDwtIHBpLmRhdCAlPiUgXG4gIGZpbHRlcihuZXdfdGltZSA9PSAwLCAhaXMubmEobmV3X21lZGlhbikpICU+JSBcbiAgbXV0YXRlKEdlbm90eXBlID0gZmFjdG9yKEdlbm90eXBlLCBsZXZlbHMgPSBnZW5vdHlwZV9vcmRlcikpXG5sbShuZXdfbWVkaWFuIH4gR2Vub3R5cGUsIGRhdGEgPSB0bXApICU+JSBcbiAgc3VtbWFyeSgpXG4gICNUdWtleUhTRCgpXG5gYGAifQ== -->

```r
# filter the data and set the basal level
genotype_order <- names(levels)

tmp <- pi.dat %>% 
  filter(new_time == 0, !is.na(new_median)) %>% 
  mutate(Genotype = factor(Genotype, levels = genotype_order))
lm(new_median ~ Genotype, data = tmp) %>% 
  summary()
  #TukeyHSD()
```

<!-- rnb-source-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->

2. At 120 minutes

<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxudG1wIDwtIHBpLmRhdCAlPiUgXG4gIGZpbHRlcihuZXdfdGltZSA9PSAxMjAsICFpcy5uYShuZXdfbWVkaWFuKSkgJT4lIFxuICBtdXRhdGUoR2Vub3R5cGUgPSBmYWN0b3IoR2Vub3R5cGUsIGxldmVscyA9IGdlbm90eXBlX29yZGVyKSlcbmxtKG5ld19tZWRpYW4gfiBHZW5vdHlwZSwgZGF0YSA9IHRtcCkgJT4lIFxuICBzdW1tYXJ5KClcbmBgYCJ9 -->

```r
tmp <- pi.dat %>% 
  filter(new_time == 120, !is.na(new_median)) %>% 
  mutate(Genotype = factor(Genotype, levels = genotype_order))
lm(new_median ~ Genotype, data = tmp) %>% 
  summary()
```

<!-- rnb-source-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->

#### under mock treatment.

Get the subset of Ctrl data

<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuY3RybC5kYXQgPC0gZGF0YSAlPiUgXG4gIGZpbHRlcih0cmVhdCA9PSBcImN0cmxcIiwgZ2Vub3R5cGUgJWluJSBsZXZlbHMpICU+JSAgXG4gIHNlbGVjdChUaW1lID0gR3JvdXAsIFNhbXBsZSwgUGxhdGUsIHJlcGxpY2F0ZSA9IFJlcGxpY2F0ZSwgZ2Vub3R5cGUsIG1lZGlhbikgJT4lXG4gIG11dGF0ZShHZW5vdHlwZSA9IGZjdF9yZWNvZGUoZ2Vub3R5cGUsICEhIWxldmVscykpICU+JSBcbiAgbXV0YXRlKG5ld19tZWRpYW4gPW1lZGlhbi8xMDAwKSAlPiUgXG4gIG11dGF0ZShuZXdfdGltZSA9IGFzLm51bWVyaWMoZ3N1YihcIm1pblwiLFwiXCIsVGltZSkpKSU+JSBcbiAgYXJyYW5nZShuZXdfdGltZSwgZ2Vub3R5cGUsIHJlcGxpY2F0ZSlcbmBgYCJ9 -->

```r
ctrl.dat <- data %>% 
  filter(treat == "ctrl", genotype %in% levels) %>%  
  select(Time = Group, Sample, Plate, replicate = Replicate, genotype, median) %>%
  mutate(Genotype = fct_recode(genotype, !!!levels)) %>% 
  mutate(new_median =median/1000) %>% 
  mutate(new_time = as.numeric(gsub("min","",Time)))%>% 
  arrange(new_time, genotype, replicate)
```

<!-- rnb-source-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->



<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuZ2Vub3R5cGVfY29sb3IgPC0gUkNvbG9yQnJld2VyOjpicmV3ZXIucGFsKDgsIFwiRGFyazJcIilbYyg4LCA3LCAyKV0gXG5uYW1lcyhnZW5vdHlwZV9jb2xvcikgPC0gbmFtZXMobGV2ZWxzKVxuXG5jdHJsLmRhdCAlPiVcbiAgZmlsdGVyKCFpcy5uYShuZXdfbWVkaWFuKSkgJT4lIFxuICBnZ3Bsb3QoYWVzKHggPSBuZXdfdGltZSwgeSA9IG5ld19tZWRpYW4sIGNvbG9yID0gR2Vub3R5cGUpKSArIHAudGltZWNvdXJzZSArXG4gIHNjYWxlX2NvbG9yX21hbnVhbCh2YWx1ZXM9IGdlbm90eXBlX2NvbG9yLCBsaW1pdHMgPSBuYW1lcyhnZW5vdHlwZV9jb2xvcikpICtcbiAgc2NhbGVfeV9jb250aW51b3VzKGxpbWl0cyA9IGMoTkEsIDIyKSlcbmdnc2F2ZShcIm91dHB1dC8yMDIzMDUxMi1DZ1NDSDktcGhvc3Bob21pbWV0aWMtbXV0YW50LXRpbWVjb3Vyc2UtY3RybC5wbmdcIiwgd2lkdGggPSA0LjIsIGhlaWdodCA9IDQpXG5gYGAifQ== -->

```r
genotype_color <- RColorBrewer::brewer.pal(8, "Dark2")[c(8, 7, 2)] 
names(genotype_color) <- names(levels)

ctrl.dat %>%
  filter(!is.na(new_median)) %>% 
  ggplot(aes(x = new_time, y = new_median, color = Genotype)) + p.timecourse +
  scale_color_manual(values= genotype_color, limits = names(genotype_color)) +
  scale_y_continuous(limits = c(NA, 22))
ggsave("output/20230512-CgSCH9-phosphomimetic-mutant-timecourse-ctrl.png", width = 4.2, height = 4)
```

<!-- rnb-source-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->

### Sch9-2E
In _S. cerevisiae_, Pho80/85 was shown to directly phosphorylate Sch9 and thereby regulate its lysosome localization. Here, Jinye interogate a phosphomimetic mutant in _C. glabrata_ and its interaction with _pho80∆_ and _pho81∆_ mutants.

<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxubGV2ZWxzIDwtIGMoV1QgPSBcInd0XCIsIGBzY2g5OjpTY2g5LVdULU5hdGAgPSBcInd0X0NnU0NIOS1OYXRcIiwgYHNjaDk6OlNjaDktM0UtTmF0YCA9IFwiQ2dTQ0g5XzNFLU5hdFwiLCBgcGhvODDiiIZgID0gXCJwaG84MF9rb1wiLCBgcGhvODDiiIYgc2NoOTo6U2NoOS0yRWAgPSBcInBobzgwX2tvX1NjaDlfMkVcIiwgYHBobzgx4oiGYCA9IFwicGhvODFfa29cIiwgYHBobzgx4oiGIHNjaDk6OlNjaDktMkVgID0gXCJwaG84MV9rb19TY2g5XzJFXCIpXG5cbnBpLmRhdC5leHQgPC0gZGF0YSAlPiUgXG4gIGZpbHRlcih0cmVhdCA9PSBcIjBQaVwiKSAlPiUgIFxuICBzZWxlY3QoVGltZSA9IEdyb3VwLCBTYW1wbGUsIFBsYXRlLCByZXBsaWNhdGUgPSBSZXBsaWNhdGUsIGdlbm90eXBlLCBtZWRpYW4pICU+JVxuICBtdXRhdGUoR2Vub3R5cGUgPSBmY3RfcmVjb2RlKGdlbm90eXBlLCAgISEhbGV2ZWxzKSkgJT4lIFxuICBtdXRhdGUobmV3X21lZGlhbiA9bWVkaWFuLzEwMDApICU+JSBcbiAgbXV0YXRlKG5ld190aW1lID0gYXMubnVtZXJpYyhnc3ViKFwibWluXCIsXCJcIixUaW1lKSkpJT4lIFxuICBhcnJhbmdlKG5ld190aW1lLCBnZW5vdHlwZSwgcmVwbGljYXRlKVxuYGBgIn0= -->

```r
levels <- c(WT = "wt", `sch9::Sch9-WT-Nat` = "wt_CgSCH9-Nat", `sch9::Sch9-3E-Nat` = "CgSCH9_3E-Nat", `pho80∆` = "pho80_ko", `pho80∆ sch9::Sch9-2E` = "pho80_ko_Sch9_2E", `pho81∆` = "pho81_ko", `pho81∆ sch9::Sch9-2E` = "pho81_ko_Sch9_2E")

pi.dat.ext <- data %>% 
  filter(treat == "0Pi") %>%  
  select(Time = Group, Sample, Plate, replicate = Replicate, genotype, median) %>%
  mutate(Genotype = fct_recode(genotype,  !!!levels)) %>% 
  mutate(new_median =median/1000) %>% 
  mutate(new_time = as.numeric(gsub("min","",Time)))%>% 
  arrange(new_time, genotype, replicate)
```

<!-- rnb-source-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->


Plot the time course

<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuZ2Vub3R5cGVfY29sb3IgPC0gUkNvbG9yQnJld2VyOjpicmV3ZXIucGFsKDgsIFwiRGFyazJcIilbYyg4LCA3LCA2LCAxLCA1LCA0LCAyKV0gXG5uYW1lcyhnZW5vdHlwZV9jb2xvcikgPC0gbmFtZXMobGV2ZWxzKVxuXG5waS5kYXQuZXh0ICU+JVxuICBmaWx0ZXIoIWlzLm5hKG5ld19tZWRpYW4pKSAlPiUgXG4gIGdncGxvdChhZXMoeCA9IG5ld190aW1lLCB5ID0gbmV3X21lZGlhbiwgY29sb3IgPSBHZW5vdHlwZSkpICsgcC50aW1lY291cnNlICtcbiAgc2NhbGVfY29sb3JfbWFudWFsKHZhbHVlcz0gZ2Vub3R5cGVfY29sb3IsIGxpbWl0cyA9IG5hbWVzKGdlbm90eXBlX2NvbG9yKSlcbiNnZ3NhdmUoXCJvdXRwdXQvMjAyMzA1MTItQ2dTQ0g5LXBob3NwaG9taW1ldGljLW11dGFudC10aW1lY291cnNlLW5vUGkucG5nXCIsIHdpZHRoID0gNC4yLCBoZWlnaHQgPSA0KVxuYGBgIn0= -->

```r
genotype_color <- RColorBrewer::brewer.pal(8, "Dark2")[c(8, 7, 6, 1, 5, 4, 2)] 
names(genotype_color) <- names(levels)

pi.dat.ext %>%
  filter(!is.na(new_median)) %>% 
  ggplot(aes(x = new_time, y = new_median, color = Genotype)) + p.timecourse +
  scale_color_manual(values= genotype_color, limits = names(genotype_color))
#ggsave("output/20230512-CgSCH9-phosphomimetic-mutant-timecourse-noPi.png", width = 4.2, height = 4)
```

<!-- rnb-source-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->


> All comparisons except for rom2- vs WT are statistically significant at 0.05 level after Bonferroni correction (threshold: 0.05/5 = 0.01)


<!-- rnb-text-end -->

