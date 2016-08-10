AlphaPipes: R package providing named magrittr-style pipe operators
================
Aleksander Rutkowski
2016-08-10

The package provides "named pipes" which may complement: the **magrittr** package pipes. The named pipes make it possible to use all lower-case and upper-case letters as the right-hand-side symbols/placeholders for the values piped from the left-hand-side, while the standard **magrittr** operator `%>%` uses only a dot.

When the package is loaded (via `library(AlphaPipes)`) the pipe operators (`%a%` ... `%z%` and `%A%` ... `%Z%`) are dynamically created in **AlphaPipes** namespace. So you cannot import them via `` `%myoperator%` <- AlphaPipes::`%a%` ``. Anyway, such an import does not seem to make sense -- namespaced operators e.g. `` AlphaPipes::`%a%` `` would be inconvenient -- too verbose, while *re-named* "named pipes" e.g. `%aa%` as an alias for `%a%` would be confusing (since symbol `a` would need to be used on the right-hand side anyway).

### Installation

`devtools::install_github('alekrutkowski/AlphaPipes')`

**AlphaPipes** needs package **clojR** which can also be installed from GitHub:

`devtools::install_github('alekrutkowski/clojR')`

### Examples

``` r
library(AlphaPipes)
```

``` r
# Trivial -- the same as
#  mean(1:3)
# or
#  1:3 %>% mean
1:3 %A% mean(A)
```

    ## [1] 2

``` r
# Showing the actual usefulness -- referring to earlier values
# from the piped flow:
data.frame(xx = 1:5) %a%
    (dplyr::mutate(a, nnn = xx + 10) %b%
         dplyr::rename(b, xx2 = xx) %b%
         cbind(b, a))
```

    ##   xx2 nnn xx
    ## 1   1  11  1
    ## 2   2  12  2
    ## 3   3  13  3
    ## 4   4  14  4
    ## 5   5  15  5

``` r
# All the available "named pipes":
cat(ls(name = "package:AlphaPipes"), sep="  ")
```

    ## %a%  %A%  %b%  %B%  %c%  %C%  %d%  %D%  %e%  %E%  %f%  %F%  %g%  %G%  %h%  %H%  %i%  %I%  %j%  %J%  %k%  %K%  %l%  %L%  %m%  %M%  %n%  %N%  %o%  %O%  %p%  %P%  %q%  %Q%  %r%  %R%  %s%  %S%  %t%  %T%  %u%  %U%  %v%  %V%  %w%  %W%  %x%  %X%  %y%  %Y%  %z%  %Z%
