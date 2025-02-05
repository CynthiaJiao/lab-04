Lab 04 - La Quinta is Spanish for next to Denny’s, Pt. 1
================
Cynthia Jiao
02/03/2025

### Load packages and data

``` r
library(tidyverse) 
library(dplyr)
library(dsbox) 
```

``` r
states <- read_csv("data/states.csv")
```

### Exercise 1

In total, there are 1643 Denny’s restaurants (each row in the tibble
represents one Denny’s location), and there are 6 variables (6 columns)
that describes the address, city, state, zip code, longitude and
latitude of each Denny’s.

``` r
## two dataset are called dennys and laquinta
## dennys
print(dennys)
```

    ## # A tibble: 1,643 × 6
    ##    address                        city            state zip   longitude latitude
    ##    <chr>                          <chr>           <chr> <chr>     <dbl>    <dbl>
    ##  1 2900 Denali                    Anchorage       AK    99503    -150.      61.2
    ##  2 3850 Debarr Road               Anchorage       AK    99508    -150.      61.2
    ##  3 1929 Airport Way               Fairbanks       AK    99701    -148.      64.8
    ##  4 230 Connector Dr               Auburn          AL    36849     -85.5     32.6
    ##  5 224 Daniel Payne Drive N       Birmingham      AL    35207     -86.8     33.6
    ##  6 900 16th St S, Commons on Gree Birmingham      AL    35294     -86.8     33.5
    ##  7 5931 Alabama Highway, #157     Cullman         AL    35056     -86.9     34.2
    ##  8 2190 Ross Clark Circle         Dothan          AL    36301     -85.4     31.2
    ##  9 900 Tyson Rd                   Hope Hull (Tys… AL    36043     -86.4     32.2
    ## 10 4874 University Drive          Huntsville      AL    35816     -86.7     34.7
    ## # ℹ 1,633 more rows

``` r
nrow(dennys)
```

    ## [1] 1643

``` r
ncol(dennys)
```

    ## [1] 6

### Exercise 2

In total, there are 909 La quinta hotels (each row in tibble represents
one La quinta locatin), and there are 6 variables (6 columns) that
describes the address, city, state, zip code, longitude and latitude of
each La quinta.

``` r
## laquinta
print(laquinta)
```

    ## # A tibble: 909 × 6
    ##    address                          city          state zip   longitude latitude
    ##    <chr>                            <chr>         <chr> <chr>     <dbl>    <dbl>
    ##  1 793 W. Bel Air Avenue            "\nAberdeen"  MD    21001     -76.2     39.5
    ##  2 3018 CatClaw Dr                  "\nAbilene"   TX    79606     -99.8     32.4
    ##  3 3501 West Lake Rd                "\nAbilene"   TX    79601     -99.7     32.5
    ##  4 184 North Point Way              "\nAcworth"   GA    30102     -84.7     34.1
    ##  5 2828 East Arlington Street       "\nAda"       OK    74820     -96.6     34.8
    ##  6 14925 Landmark Blvd              "\nAddison"   TX    75254     -96.8     33.0
    ##  7 Carretera Panamericana Sur KM 12 "\nAguascali… AG    20345    -102.      21.8
    ##  8 909 East Frontage Rd             "\nAlamo"     TX    78516     -98.1     26.2
    ##  9 2116 Yale Blvd Southeast         "\nAlbuquerq… NM    87106    -107.      35.1
    ## 10 7439 Pan American Fwy Northeast  "\nAlbuquerq… NM    87109    -107.      35.2
    ## # ℹ 899 more rows

``` r
nrow(laquinta)
```

    ## [1] 909

``` r
ncol(laquinta)
```

    ## [1] 6

### Exercise 3

There are multiple locations of La quinta that are outside of the U.S.
In total, there are 25 locations outside of the U.S. (If I am counting
correctly), including locations in Canada, Mexico, China, New Zealand,
Turkey, United Arab Emirates, Chile, Colombia, and Ecuador.

As for Denny’s, their website did not specify which or the total number
of locations that are outside of the U.S. However, they do have
locations in the following countries: Canada, Puerto Rico, Guam, Mexico,
Honduras, Costa Rica, Guatemala, El Salvador, The Philippines,
Indonesia, New Zealand, The United Arab Emirates, The United Kingdom,
and Japan.

### Exercise 4

One way to filter out the non-US locations would be using US state
abbreviations. Use dplyr and enter all 50 US state abbreviations to
filter out all observations that have non-US state abbreviations. For
example, there is one La quinta in Colombia with state column saying
“ANT,” which will be filtered out if using this method.

The other way to do it is through US zip code range. According to
ChatGPT, all US zip codes fall within the range of 00501 to 99950.
Although not every consecutive number within the range is assigned as an
existing US zip code, we can still use dplyr to filter out any location
with zip code outside of this range. Or, all existing US zip code can be
scraped from USPS website, and a filter that contains all existing zip
codes can be applied to the dennys and laquinta data to filter out any
non-US locations.

### Exercise 5

No, there is not any Denny’s location outside of the US in the dataset.

``` r
################### dn and lq means dennys and laquinta dataset, correct???

## finding any non-US Denny's location
dennys %>%
  filter(!(state %in% states$abbreviation))
```

    ## # A tibble: 0 × 6
    ## # ℹ 6 variables: address <chr>, city <chr>, state <chr>, zip <chr>,
    ## #   longitude <dbl>, latitude <dbl>

### Exercise 6

``` r
## creating country variable for dennys
dennys %>%
  mutate(country = "United States")
```

    ## # A tibble: 1,643 × 7
    ##    address                        city    state zip   longitude latitude country
    ##    <chr>                          <chr>   <chr> <chr>     <dbl>    <dbl> <chr>  
    ##  1 2900 Denali                    Anchor… AK    99503    -150.      61.2 United…
    ##  2 3850 Debarr Road               Anchor… AK    99508    -150.      61.2 United…
    ##  3 1929 Airport Way               Fairba… AK    99701    -148.      64.8 United…
    ##  4 230 Connector Dr               Auburn  AL    36849     -85.5     32.6 United…
    ##  5 224 Daniel Payne Drive N       Birmin… AL    35207     -86.8     33.6 United…
    ##  6 900 16th St S, Commons on Gree Birmin… AL    35294     -86.8     33.5 United…
    ##  7 5931 Alabama Highway, #157     Cullman AL    35056     -86.9     34.2 United…
    ##  8 2190 Ross Clark Circle         Dothan  AL    36301     -85.4     31.2 United…
    ##  9 900 Tyson Rd                   Hope H… AL    36043     -86.4     32.2 United…
    ## 10 4874 University Drive          Huntsv… AL    35816     -86.7     34.7 United…
    ## # ℹ 1,633 more rows

### Exercise 7

Yes, there are 14 La quinta locations outside of the US.

10 locations in Mexico; 2 locations in Canada; 1 location in Colombia; 1
location in Honduras.

``` r
## finding any non-US La quinta locations
laquinta %>%
  filter(!(state %in% states$abbreviation))
```

    ## # A tibble: 14 × 6
    ##    address                                  city  state zip   longitude latitude
    ##    <chr>                                    <chr> <chr> <chr>     <dbl>    <dbl>
    ##  1 Carretera Panamericana Sur KM 12         "\nA… AG    20345    -102.     21.8 
    ##  2 Av. Tulum Mza. 14 S.M. 4 Lote 2          "\nC… QR    77500     -86.8    21.2 
    ##  3 Ejercito Nacional 8211                   "Col… CH    32528    -106.     31.7 
    ##  4 Blvd. Aeropuerto 4001                    "Par… NL    66600    -100.     25.8 
    ##  5 Carrera 38 # 26-13 Avenida las Palmas c… "\nM… ANT   0500…     -75.6     6.22
    ##  6 AV. PINO SUAREZ No. 1001                 "Col… NL    64000    -100.     25.7 
    ##  7 Av. Fidel Velazquez #3000 Col. Central   "\nM… NL    64190    -100.     25.7 
    ##  8 63 King Street East                      "\nO… ON    L1H1…     -78.9    43.9 
    ##  9 Calle Las Torres-1 Colonia Reforma       "\nP… VE    93210     -97.4    20.6 
    ## 10 Blvd. Audi N. 3 Ciudad Modelo            "\nS… PU    75010     -97.8    19.2 
    ## 11 Ave. Zeta del Cochero No 407             "Col… PU    72810     -98.2    19.0 
    ## 12 Av. Benito Juarez 1230 B (Carretera 57)… "\nS… SL    78399    -101.     22.1 
    ## 13 Blvd. Fuerza Armadas                     "con… FM    11101     -87.2    14.1 
    ## 14 8640 Alexandra Rd                        "\nR… BC    V6X1…    -123.     49.2

### Exercise 8

``` r
## adding a country variable to the La Quinta dataset AND filtering out all non-US La Quinta locations

laquinta %>%
  mutate(country = case_when(
    state %in% state.abb ~ "United States",
    state %in% c("ON", "BC") ~ "Canada",
    state == "ANT" ~ "Colombia",
    state == "FM" ~ "Honduras",
    state %in% c("AG", "QR", "CH", "NL", "VE","PU","Sl") ~ "Mexico"
  )) %>%
  filter(country == "United States")
```

    ## # A tibble: 895 × 7
    ##    address                         city   state zip   longitude latitude country
    ##    <chr>                           <chr>  <chr> <chr>     <dbl>    <dbl> <chr>  
    ##  1 793 W. Bel Air Avenue           "\nAb… MD    21001     -76.2     39.5 United…
    ##  2 3018 CatClaw Dr                 "\nAb… TX    79606     -99.8     32.4 United…
    ##  3 3501 West Lake Rd               "\nAb… TX    79601     -99.7     32.5 United…
    ##  4 184 North Point Way             "\nAc… GA    30102     -84.7     34.1 United…
    ##  5 2828 East Arlington Street      "\nAd… OK    74820     -96.6     34.8 United…
    ##  6 14925 Landmark Blvd             "\nAd… TX    75254     -96.8     33.0 United…
    ##  7 909 East Frontage Rd            "\nAl… TX    78516     -98.1     26.2 United…
    ##  8 2116 Yale Blvd Southeast        "\nAl… NM    87106    -107.      35.1 United…
    ##  9 7439 Pan American Fwy Northeast "\nAl… NM    87109    -107.      35.2 United…
    ## 10 2011 Menaul Blvd Northeast      "\nAl… NM    87107    -107.      35.1 United…
    ## # ℹ 885 more rows

### Exercise 9

California has the most Denny’s locations (403 locations), and Delaware
has least Denny’s (just 1 location). I am not surprised about California
being the state that has the most Denny’s locations, as Denny’s
originated from California. But I am not sure why Delaware has the least
location, maybe they already have similar local brand that is more
popular than Denny’s?

Texas has the most La quinta locations (237 locations), but DC,
Delaware, Hawaii have no La quinta hotel. Similar to Denny’s, I am not
surprised about Texas being the state that has the most La quinta
locations, as they originated from Texas. But I don’t know why there are
3 states without any La quinta locations, maybe the competition is too
fierce at these places??

``` r
## counting the states have the most and fewest Denny’s locations

dennys %>%
  count(state) %>%
  inner_join(states, by = c("state" = "abbreviation"))
```

    ## # A tibble: 51 × 4
    ##    state     n name                     area
    ##    <chr> <int> <chr>                   <dbl>
    ##  1 AK        3 Alaska               665384. 
    ##  2 AL        7 Alabama               52420. 
    ##  3 AR        9 Arkansas              53179. 
    ##  4 AZ       83 Arizona              113990. 
    ##  5 CA      403 California           163695. 
    ##  6 CO       29 Colorado             104094. 
    ##  7 CT       12 Connecticut            5543. 
    ##  8 DC        2 District of Columbia     68.3
    ##  9 DE        1 Delaware               2489. 
    ## 10 FL      140 Florida               65758. 
    ## # ℹ 41 more rows

``` r
## counting the states have the most and fewest La quinta’s locations

laquinta %>%
  count(state) %>%
  inner_join(states, by = c("state" = "abbreviation"))
```

    ## # A tibble: 48 × 4
    ##    state     n name           area
    ##    <chr> <int> <chr>         <dbl>
    ##  1 AK        2 Alaska      665384.
    ##  2 AL       16 Alabama      52420.
    ##  3 AR       13 Arkansas     53179.
    ##  4 AZ       18 Arizona     113990.
    ##  5 CA       56 California  163695.
    ##  6 CO       27 Colorado    104094.
    ##  7 CT        6 Connecticut   5543.
    ##  8 FL       74 Florida      65758.
    ##  9 GA       41 Georgia      59425.
    ## 10 IA        4 Iowa         56273.
    ## # ℹ 38 more rows

### Exercise 10

DC has the most Denny’s locations per thousand square miles. For every
1000 square miles, DC has 29 locations of Denny’s. Since DC only has 2
Denny’s, this high density is probably because DC is the smallest state.

Rhode Island has the most La quinta locations per thousand square miles.
For every 1000 square miles, RI has 1 location of La quinta.

``` r
## counting states having the most Denny's location per thousand square miles.

dennys_density <- dennys %>%
  count(state) %>%
  inner_join(states, by = c("state" = "abbreviation")) %>%
  mutate(dennys_per_1000_sq_miles = n / (area / 1000)) %>%
  arrange(desc(dennys_per_1000_sq_miles))

print(dennys_density)
```

    ## # A tibble: 51 × 5
    ##    state     n name                     area dennys_per_1000_sq_miles
    ##    <chr> <int> <chr>                   <dbl>                    <dbl>
    ##  1 DC        2 District of Columbia     68.3                   29.3  
    ##  2 RI        5 Rhode Island           1545.                     3.24 
    ##  3 CA      403 California           163695.                     2.46 
    ##  4 CT       12 Connecticut            5543.                     2.16 
    ##  5 FL      140 Florida               65758.                     2.13 
    ##  6 MD       26 Maryland              12406.                     2.10 
    ##  7 NJ       10 New Jersey             8723.                     1.15 
    ##  8 NY       56 New York              54555.                     1.03 
    ##  9 IN       37 Indiana               36420.                     1.02 
    ## 10 OH       44 Ohio                  44826.                     0.982
    ## # ℹ 41 more rows

``` r
## counting states having the most La quinta location per thousand square miles.

lq_density <- laquinta %>%
  count(state) %>%
  inner_join(states, by = c("state" = "abbreviation")) %>%
  mutate(lq_per_1000_sq_miles = n / (area / 1000)) %>%
  arrange(desc(lq_per_1000_sq_miles))

print(lq_density)
```

    ## # A tibble: 48 × 5
    ##    state     n name             area lq_per_1000_sq_miles
    ##    <chr> <int> <chr>           <dbl>                <dbl>
    ##  1 RI        2 Rhode Island    1545.                1.29 
    ##  2 FL       74 Florida        65758.                1.13 
    ##  3 CT        6 Connecticut     5543.                1.08 
    ##  4 MD       13 Maryland       12406.                1.05 
    ##  5 TX      237 Texas         268596.                0.882
    ##  6 TN       30 Tennessee      42144.                0.712
    ##  7 GA       41 Georgia        59425.                0.690
    ##  8 NJ        5 New Jersey      8723.                0.573
    ##  9 MA        6 Massachusetts  10554.                0.568
    ## 10 LA       28 Louisiana      52378.                0.535
    ## # ℹ 38 more rows

### Exercise 11

Just from the NC scatter plot, Mitch Hedberg’s joke does not hold true.
Out of 40 locations of Denny’s and La quinta in NC, only 7 of them (3
pairs) seem to be next to each other.

``` r
## combining two dataset
dennys <- dennys %>%
  mutate(establishment = "Denny's")

laquinta <- laquinta %>%
  mutate(establishment = "La Quinta")

dn_lq <- bind_rows(dennys, laquinta)

## scatter plot for ALL the ds and lq locations

ggplot(dn_lq, mapping = aes(
  x = longitude,
  y = latitude,
  color = establishment
)) +
  geom_point()
```

![](lab-04_files/figure-gfm/exercise%2011-1-1.png)<!-- -->

``` r
## filter the data for observations in North Carolina only

dn_lq_nc <- dn_lq %>%
  filter(state == "NC")

## recreate the scatter plot for NC

ggplot(dn_lq_nc, mapping = aes(
  x = longitude,
  y = latitude,
  color = establishment
)) +
  geom_point(alpha = 0.7)
```

![](lab-04_files/figure-gfm/exercise%2011-2-1.png)<!-- -->

### Exercise 12

From Texas scatter plot, Mitch Hedberg’s joke holds true. Although I
cannot count the exact numbers of Denny’s and La quinta that are next to
each other, there are clearly many of them clustering together on the
graph.

``` r
## filter the data for observations in Texas only

dn_lq_tx <- dn_lq %>%
  filter(state == "TX")

## recreate the scatter plot for TX

ggplot(dn_lq_tx, mapping = aes(
  x = longitude,
  y = latitude,
  color = establishment
)) +
  geom_point(alpha = 0.3)
```

![](lab-04_files/figure-gfm/exercise%2012-1.png)<!-- -->
