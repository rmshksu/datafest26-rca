---
title: Solving problems using data
nav: Live
topics: Real world application
---

## Let's put it all together.

> We'll start with an RCA, form a hypothesis from it, clean the data, and deliver a product.

<br>

<br>

## Overdose

{% capture text %}

Drug and alcohol overdose deaths have risen nationwide at a startling pace. Midwestern U.S. has seen the most significant rise of them all, with almost a 6 fold increase since 1999. 

As overdose deaths rise so rises the need for emergency response systems to adapt to the environment. The cause of this rise and its overall impact is too complex to confine to one analysis, but if we can isolate one strong root cause we should be able to *anticipate* where and when resources need to be spent. 


{% endcapture %}
{% include card.html text=text title="Getting ahead of tragedy." img="Authentic_Fentanyl_lethal_dose_pencil.jpg"%}

<br>

### Problem statement

> Overdose deaths have risen 6-fold in Midwestern states since 1999.

<br>

### Why?

1. Counties in Midwestern states are experiencing rapid socioeconomic decline proportional to overdose death increases.

2. The region has very low intergenerational income mobility on average, leading to consistent decline.

3. "Economic hopelessness" is shown to have a strong impact on individuals choice to begin drug use. 

4. People tend to turn towards drugs when they need a powerful way to escape an "inescapable" situation.

5. Midwestern U.S. is primarily rural and travel is very difficult without high enough economic status to afford the trek outside of the region.

<br>

{% include alert.html text="Think through a Five-why analysis independently on the same problem statement. Can you arrive at a different root cause? Carry that root cause with you as we move along." align="center" color="success" %}

<br>

<br>

### Categorize

{% include question.html header="Learning check" text="What category does the root cause identified in the Five-why analysis above fall into?" solution="Capability: Missing resources / Impossible." %}

<br>

<br>

## Forming a hypothesis

> This should be familiar territory for any scientist, but try to think of it with a different approach here. Rather than marrying ourselves to a hypothesis we intend to test, let's build something that can guide us in our analysis. It's possible we'll discard the hypothesis later—keep an open mind!

<br>

{% include jumbotron.html heading="Midwestern overdose rates are economic." text="The best predictor of where to send resources to handle or prevent overdose deaths will be the economic status of the area." border=true %}

<br>

### Avenues of approach

**We need to select potential indicators for our root cause. Sometimes this comes with the data on our problem statement, sometimes this is auxillary data.**

<div class="container my-4">
  <div class="row row-cols-1 row-cols-md-2 g-4">

    <div class="col">
      <div class="card h-100 shadow-sm border-3 border-step-1">
        <div class="card-body">
          <h4 class="card-title fw-bold">Crime</h4>
          <ul>
            <li>High crime indicates lower economic class</li>
            <li>Violent crimes and larceny</li>
            <li>Possibly biased to demographic</li>
          </ul>
        </div>
      </div>
    </div>

    <div class="col">
      <div class="card h-100 shadow-sm border-3 border-step-4">
        <div class="card-body">
          <h4 class="card-title fw-bold">Social vulnerability</h4>
          <ul>
            <li>Direct measures of socioeconomic health</li>
            <li>High vulnerability = high overdose</li>
            <li>More demographic neutral</li>
          </ul>
        </div>
      </div>
    </div>

  </div>
</div>

<br>

<br>

## CDC WONDER

> The CDC WONDER database happens to have a *very* detailed account of deaths and their causes nationwide. However for privacy reasons the death counts are censored when the fall between 1 and 9 for a specific pairing of strata.

<br>

### Goal: Acquire data on Kansas county overdose deaths

I pulled the underlying cause of death between 2018 and 2023 data using the query below:
				
Query Parameters:					
- Drug/Alcohol Induced Causes: Drug poisonings (overdose) Unintentional (X40-X44)					
- Place of Death: Medical Facility - Inpatient; Medical Facility - Outpatient or ER; Medical Facility - Dead on Arrival; Medical					
- Facility - Status unknown; Decedent's home					
- States: Kansas (20)					
- Ten-Year Age Groups: 5-14 years; 15-24 years; 25-34 years; 35-44 years; 45-54 years; 55-64 years; 65-74 years					
- Group By: Year; County				

<br>

The output is tossed into a .xls file and ready to roll!

<div class="card shadow-sm mb-4">
  <div class="card-header bg-dark text-white">
    R Code
  </div>
  <div class="card-body bg-light">
<pre class="mb-0"><code>
YrC = read.delim("KS_OD_Data/KS_OD_YrC.xls", sep = "\t")
head(YrC)
YrC[637:641,]
YrC = YrC[1:636,-1]
</code></pre>
  </div>
</div>

<div class="card shadow-sm mb-4">
  <div class="card-header bg-secondary text-white">
    Output
  </div>
  <div class="card-body bg-white">
<pre class="mb-0"><code>
&gt; head(YrC)
  Notes Year Year.Code              County County.Code     Deaths
1       2018      2018    Allen County, KS       20001 Suppressed
2       2018      2018 Anderson County, KS       20003 Suppressed
3       2018      2018 Atchison County, KS       20005 Suppressed
4       2018      2018   Barber County, KS       20007          0
5       2018      2018   Barton County, KS       20009 Suppressed
6       2018      2018  Bourbon County, KS       20011          0

&gt; YrC[637:641,]
                                                                              Notes Year Year.Code County County.Code Deaths
637                                                                           Total   NA        NA                 NA   2171
638                                                                             ---   NA        NA                 NA       
639                      Dataset: Underlying Cause of Death, 2018-2023, Single Race   NA        NA                 NA       
640                                                               Query Parameters:   NA        NA                 NA       
641 Drug/Alcohol Induced Causes: Drug poisonings (overdose) Unintentional (X40-X44)   NA        NA                 NA       
</code></pre>
  </div>
</div>

<br>

**We'll need to fix the suppressed data if we want to get anywhere with this. Luckily, this is a great chance to test how strong our predictors are!**

<br>

## CDC/ATSDR Social Vulnerability Index

>"The current CDC/ATSDR Social Vulnerability Index uses 16 U.S. Census variables from the 5-year American Community Survey (ACS) to identify communities that may need support before, during, or after disasters." - ATSDR

<br>

**These reports are only updated and released every other year.**

<br>

We'll query the data for 2018-2029, 2020-2021, 2022-2023, and pretend that these values don't change much between years.

<br>

<div class="card shadow-sm mb-4">
  <div class="card-header bg-dark text-white">
    R Code
  </div>
  <div class="card-body bg-light">
<pre class="mb-0"><code>
svi18 = read.csv("ks_svi_2018.csv")
svi20 = read.csv("ks_svi_2020.csv")
svi22 = read.csv("ks_svi_2022.csv")
colnames(svi18)
</code></pre>
  </div>
</div>

<div class="card shadow-sm mb-4">
  <div class="card-header bg-secondary text-white">
    Output
  </div>
  <div class="card-body bg-white">
<pre class="mb-0"><code>
&gt; colnames(svi18)
  [1] "ST"         "STATE"      "ST_ABBR"    "COUNTY"     "FIPS"       "LOCATION"   "AREA_SQMI"  "E_TOTPOP"   "M_TOTPOP"   "E_HU"      
 [11] "M_HU"       "E_HH"       "M_HH"       "E_POV"      "M_POV"      "E_UNEMP"    "M_UNEMP"    "E_PCI"      "M_PCI"      "E_NOHSDP"  
 [21] "M_NOHSDP"   "E_AGE65"    "M_AGE65"    "E_AGE17"    "M_AGE17"    "E_DISABL"   "M_DISABL"   "E_SNGPNT"   "M_SNGPNT"   "E_MINRTY"  
 [31] "M_MINRTY"   "E_LIMENG"   "M_LIMENG"   "E_MUNIT"    "M_MUNIT"    "E_MOBILE"   "M_MOBILE"   "E_CROWD"    "M_CROWD"    "E_NOVEH"   
 [41] "M_NOVEH"    "E_GROUPQ"   "M_GROUPQ"   "EP_POV"     "MP_POV"     "EP_UNEMP"   "MP_UNEMP"   "EP_PCI"     "MP_PCI"     "EP_NOHSDP" 
 [51] "MP_NOHSDP"  "EP_AGE65"   "MP_AGE65"   "EP_AGE17"   "MP_AGE17"   "EP_DISABL"  "MP_DISABL"  "EP_SNGPNT"  "MP_SNGPNT"  "EP_MINRTY" 
 [61] "MP_MINRTY"  "EP_LIMENG"  "MP_LIMENG"  "EP_MUNIT"   "MP_MUNIT"   "EP_MOBILE"  "MP_MOBILE"  "EP_CROWD"   "MP_CROWD"   "EP_NOVEH"  
 [71] "MP_NOVEH"   "EP_GROUPQ"  "MP_GROUPQ"  "EPL_POV"    "EPL_UNEMP"  "EPL_PCI"    "EPL_NOHSDP" "SPL_THEME1" "RPL_THEME1" "EPL_AGE65" 
 [81] "EPL_AGE17"  "EPL_DISABL" "EPL_SNGPNT" "SPL_THEME2" "RPL_THEME2" "EPL_MINRTY" "EPL_LIMENG" "SPL_THEME3" "RPL_THEME3" "EPL_MUNIT" 
 [91] "EPL_MOBILE" "EPL_CROWD"  "EPL_NOVEH"  "EPL_GROUPQ" "SPL_THEME4" "RPL_THEME4" "SPL_THEMES" "RPL_THEMES" "F_POV"      "F_UNEMP"   
[101] "F_PCI"      "F_NOHSDP"   "F_THEME1"   "F_AGE65"    "F_AGE17"    "F_DISABL"   "F_SNGPNT"   "F_THEME2"   "F_MINRTY"   "F_LIMENG"  
[111] "F_THEME3"   "F_MUNIT"    "F_MOBILE"   "F_CROWD"    "F_NOVEH"    "F_GROUPQ"   "F_THEME4"   "F_TOTAL"    "E_UNINSUR"  "M_UNINSUR" 
[121] "EP_UNINSUR" "MP_UNINSUR" "E_DAYPOP"  
</code></pre>
  </div>
</div>

<br>

> That's a lot of letters that make only a little bit of sense. Fortuantely, the SVI data comes with a [data dictionary!](https://svi.cdc.gov/map25/data/docs/SVI2018Documentation_01192022_1.pdf)

The columns we'll end up grabbing will be:

- County ID code (a.k.a. FIPS)

- Estimated total population

- Estimated population below the poverty line

- Estimated unemployed

- Estimated number of persons with no high school diploma

- Estimated population with a disability

- Estimated single parent households

- Estimated count mobile homes

- Estimated households with more occupants than rooms

<br>

**We'll split the overdose data by suppressed and visible data. If a strong trend exists in the visible data then it probably exists in the suppressed data.**

<br>

<div class="card shadow-sm mb-4">
  <div class="card-header bg-dark text-white">
    R Code
  </div>
  <div class="card-body bg-light">
<pre class="mb-0"><code>
# subset to only the visible data
YrC_s = subset(YrC, YrC$Deaths != "Suppressed")
YrC_s = subset(YrC_s, YrC_s$County != "")

# lookup table for visible data
c_lkp = unique(YrC_s$County.Code)
c_lkp
</code></pre>
  </div>
</div>

<div class="card shadow-sm mb-4">
  <div class="card-header bg-secondary text-white">
    Output
  </div>
  <div class="card-body bg-white">
<pre class="mb-0"><code>
&gt; c_lkp
 [1] 20007 20011 20013 20021 20023 20025 20027 20033 20039 20043 20047 20049 20053 20063 20065 20067 20069 20073 20075 20077 20083 20089
[23] 20091 20093 20095 20097 20101 20105 20109 20113 20119 20123 20127 20129 20131 20135 20143 20147 20151 20153 20157 20159 20165 20167
[45] 20171 20173 20177 20179 20183 20185 20187 20193 20195 20199 20201 20203 20003 20017 20019 20029 20045 20071 20081 20087 20103 20115
[67] 20117 20141 20155 20163 20181 20189 20197 20207 20209 20005 20015 20051 20137 20145 20149 20175 20009 20001 20031
</code></pre>
  </div>
</div>

<br>

{% include alert.html text="Always check your lookup table to make sure you've built what you intended. The first errors in matching up data sources start with misspecified lookup tables!" align="center" color="danger" %}

<br>

>Now to pull out the data we want with the lookup table we've built, and form data for each year.

<div class="card shadow-sm mb-4">
  <div class="card-header bg-dark text-white">
    R Code
  </div>
  <div class="card-body bg-light">
<pre class="mb-0"><code>
# svi data pulled via the lookup table
lkp_dat_18 = subset(svi18, svi18$FIPS %in% c_lkp)
lkp_dat_20 = subset(svi20, svi20$FIPS %in% c_lkp)
lkp_dat_22 = subset(svi22, svi22$FIPS %in% c_lkp)

dat18 = data.frame(Year = 2018,
                   County.Code = lkp_dat_18$FIPS,
                   Population = lkp_dat_18$E_TOTPOP,
                   Poverty = lkp_dat_18$E_POV,
                   Unemployment = lkp_dat_18$E_UNEMP,
                   School = lkp_dat_18$E_NOHSDP,
                   Disabled = lkp_dat_18$E_DISABL,
                   Parent = lkp_dat_18$E_SNGPNT,
                   Mobile = lkp_dat_18$E_MOBILE,
                   Crowd = lkp_dat_18$E_CROWD)

dat19 = data.frame(Year = 2019,
                   County.Code = lkp_dat_18$FIPS,
                   Population = lkp_dat_18$E_TOTPOP,
                   Poverty = lkp_dat_18$E_POV,
                   Unemployment = lkp_dat_18$E_UNEMP,
                   School = lkp_dat_18$E_NOHSDP,
                   Disabled = lkp_dat_18$E_DISABL,
                   Parent = lkp_dat_18$E_SNGPNT,
                   Mobile = lkp_dat_18$E_MOBILE,
                   Crowd = lkp_dat_18$E_CROWD)

# ...
# repeat the same pattern for 2020–2023, switching to lkp_dat_20 for 2020–2021,
# and lkp_dat_22 for 2022–2023; note a change in naming for Poverty after 2020.

dat23 = data.frame(Year = 2023,
                   County.Code = lkp_dat_22$FIPS,
                   Population = lkp_dat_22$E_TOTPOP,
                   Poverty = lkp_dat_22$E_POV150, # naming convention changed
                   Unemployment = lkp_dat_22$E_UNEMP,
                   School = lkp_dat_22$E_NOHSDP,
                   Disabled = lkp_dat_22$E_DISABL,
                   Parent = lkp_dat_22$E_SNGPNT,
                   Mobile = lkp_dat_22$E_MOBILE,
                   Crowd = lkp_dat_22$E_CROWD)

# combine all of the data pulled via the lookup
lkp_dat = rbind(dat18,dat19,dat20,dat21,dat22,dat23)

# join it with the visible overdose data subset
full_dat = left_join(YrC_s,lkp_dat, join_by(Year,County.Code))
head(full_dat)
</code></pre>
  </div>
</div>

<div class="card shadow-sm mb-4">
  <div class="card-header bg-secondary text-white">
    Output
  </div>
  <div class="card-body bg-white">
<pre class="mb-0"><code>
> head(full_dat)
  Year Year.Code              County County.Code Deaths Population Poverty Unemployment School Disabled Parent Mobile Crowd
1 2018      2018   Barber County, KS       20007      0       4733     729           38    280      742    135    180    33
2 2018      2018  Bourbon County, KS       20011      0      14702    2359          161    846     2963    484    505   221
3 2018      2018    Brown County, KS       20013      0       9664    1358          168    484     1532    306    173    69
4 2018      2018 Cherokee County, KS       20021      0      20331    2763          427   1535     4528    576   1129    94
5 2018      2018 Cheyenne County, KS       20023      0       2677     249           38    124      416     85     70     6
6 2018      2018    Clark County, KS       20025      0       2053     220           12     91      273     89     74    23
</code></pre>
  </div>
</div>

<br>

### Now is a good time to explore

**It's good to know how connected everything is. The benefit of being so careful with our root cause analysis and hypothesis formation is that we can use simple tools to answer questions like this.**

<div class="card shadow-sm mb-4">
  <div class="card-header bg-dark text-white">
    R Code
  </div>
  <div class="card-body bg-light">
<pre class="mb-0"><code>
# covert everything besides columns 2 and 3 to numeric
full_dat_num = full_dat[,-c(2,3)] |> 
  mutate(across(everything(), ~ as.numeric(as.character(.))))

# marginal correlations with overdose deaths
cor(full_dat_num)[,3]
</code></pre>
  </div>
</div>

<div class="card shadow-sm mb-4">
  <div class="card-header bg-secondary text-white">
    Output
  </div>
  <div class="card-body bg-white">
<pre class="mb-0"><code>
&gt; cor(full_dat_num)[,3]
        Year  County.Code       Deaths   Population      Poverty Unemployment       School     Disabled       Parent       Mobile 
   0.0826567    0.1553381    1.0000000    0.8460529    0.9706848    0.9120029    0.9233689    0.9266400    0.8397724    0.8981695 
       Crowd 
   0.9307773
</code></pre>
  </div>
</div>

<br>

> With a good understanding of our data and it's connections we can start to fill in those "suppressed" blanks. We'll try out two different models, one with two 'strong' indicators along with time, and the other with just time.

<br>

<div class="card shadow-sm mb-4">
  <div class="card-header bg-dark text-white">
    R Code
  </div>
  <div class="card-body bg-light">
<pre class="mb-0"><code>
m1 = lm(Deaths ~ Poverty + School + Year, data = full_dat_num)
summary(m1)
</code></pre>
  </div>
</div>

<div class="card shadow-sm mb-4">
  <div class="card-header bg-secondary text-white">
    Output
  </div>
  <div class="card-body bg-white">
<pre class="mb-0"><code>
&gt; summary(m1)

Call:
lm(formula = Deaths ~ Poverty + School + Year, data = full_dat_num)

Residuals:
    Min      1Q  Median      3Q     Max 
-23.983  -0.037   0.534   0.867  44.387 

Coefficients:
              Estimate Std. Error t value Pr(&gt;|t|)    
(Intercept) -4.970e+01  2.771e+02  -0.179  0.85778    
Poverty      1.279e-03  5.462e-05  23.423  &lt; 2e-16 ***
School      -4.527e-04  1.549e-04  -2.923  0.00368 ** 
Year         2.395e-02  1.372e-01   0.175  0.86149    
---
Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1

Residual standard error: 4.282 on 357 degrees of freedom
Multiple R-squared:  0.9437,  Adjusted R-squared:  0.9432 
F-statistic: 1994 on 3 and 357 DF,  p-value: &lt; 2.2e-16
</code></pre>
  </div>
</div>

<div class="card shadow-sm mb-4">
  <div class="card-header bg-dark text-white">
    R Code
  </div>
  <div class="card-body bg-light">
<pre class="mb-0"><code>
m2 = lm(Deaths ~ Year, data = full_dat_num)
summary(m2)
</code></pre>
  </div>
</div>

<div class="card shadow-sm mb-4">
  <div class="card-header bg-secondary text-white">
    Output
  </div>
  <div class="card-body bg-white">
<pre class="mb-0"><code>
&gt; summary(m2)

Call:
lm(formula = Deaths ~ Year, data = full_dat_num)

Residuals:
    Min      1Q  Median      3Q     Max 
 -6.490  -5.609  -3.847  -2.084 164.391 

Coefficients:
              Estimate Std. Error t value Pr(>|t|)
(Intercept) -1776.2978  1133.0395  -1.568    0.118
Year            0.8813     0.5608   1.571    0.117

Residual standard error: 17.93 on 359 degrees of freedom
Multiple R-squared:  0.006832,	Adjusted R-squared:  0.004066 
F-statistic:  2.47 on 1 and 359 DF,  p-value: 0.1169
</code></pre>
  </div>
</div>

<br>

> We now return to our original data and filter for only the suppressed values to build a new lookup table.

<br>

<div class="card shadow-sm mb-4">
  <div class="card-header bg-dark text-white">
    R Code
  </div>
  <div class="card-body bg-light">
<pre class="mb-0"><code>
YrC_pred = subset(YrC, YrC$Deaths == "Suppressed")
YrC_pred = subset(YrC_pred, YrC_pred$County != "")

c_lkp = unique(YrC_pred$County.Code)
c_lkp
</code></pre>
  </div>
</div>

<div class="card shadow-sm mb-4">
  <div class="card-header bg-secondary text-white">
    Output
  </div>
  <div class="card-body bg-white">
<pre class="mb-0"><code>
&gt; c_lkp
 [1] 20001 20003 20005 20009 20015 20017 20019 20029 20031 20035 20037 20041 20045 20051 20055 20057 20059 20061 20071
[20] 20079 20081 20085 20087 20099 20103 20107 20111 20115 20117 20121 20125 20133 20137 20139 20141 20145 20149 20155
[39] 20161 20163 20169 20175 20181 20189 20191 20197 20205 20207 20209 20007 20011 20013 20021 20033 20077 20109 20129
[58] 20183 20201 20027 20047 20049 20095 20113 20151 20167 20171 20065 20073 20105 20203 20023 20043 20123 20143 20157
[77] 20159 20187 20199 20075 20101 20147
</code></pre>
  </div>
</div>

<br>

**Reusing syntax/code is fine as long as you aren't using it for anything vital later down the road. Since these are all temporary objects there's no harm is overwriting them.**

<div class="card shadow-sm mb-4">
  <div class="card-header bg-dark text-white">
    R Code
  </div>
  <div class="card-body bg-light">
<pre class="mb-0"><code>
lkp_dat_18 = subset(svi18, svi18$FIPS %in% c_lkp)
lkp_dat_20 = subset(svi20, svi20$FIPS %in% c_lkp)
lkp_dat_22 = subset(svi22, svi22$FIPS %in% c_lkp)

dat18 = data.frame(Year = 2018,
                   County.Code = lkp_dat_18$FIPS,
                   Population = lkp_dat_18$E_TOTPOP,
                   Poverty = lkp_dat_18$E_POV,
                   Unemployment = lkp_dat_18$E_UNEMP,
                   School = lkp_dat_18$E_NOHSDP,
                   Disabled = lkp_dat_18$E_DISABL,
                   Parent = lkp_dat_18$E_SNGPNT,
                   Mobile = lkp_dat_18$E_MOBILE,
                   Crowd = lkp_dat_18$E_CROWD)

dat19 = data.frame(Year = 2019,
                   County.Code = lkp_dat_18$FIPS,
                   Population = lkp_dat_18$E_TOTPOP,
                   Poverty = lkp_dat_18$E_POV,
                   Unemployment = lkp_dat_18$E_UNEMP,
                   School = lkp_dat_18$E_NOHSDP,
                   Disabled = lkp_dat_18$E_DISABL,
                   Parent = lkp_dat_18$E_SNGPNT,
                   Mobile = lkp_dat_18$E_MOBILE,
                   Crowd = lkp_dat_18$E_CROWD)

# ...
# repeat the same pattern for 2020–2023, 
# switching to lkp_dat_20 for 2020–2021,
# and lkp_dat_22 for 2022–2023;

dat23 = data.frame(Year = 2023,
                   County.Code = lkp_dat_22$FIPS,
                   Population = lkp_dat_22$E_TOTPOP,
                   Poverty = lkp_dat_22$E_POV150,
                   Unemployment = lkp_dat_22$E_UNEMP,
                   School = lkp_dat_22$E_NOHSDP,
                   Disabled = lkp_dat_22$E_DISABL,
                   Parent = lkp_dat_22$E_SNGPNT,
                   Mobile = lkp_dat_22$E_MOBILE,
                   Crowd = lkp_dat_22$E_CROWD)

# bind everything together
lkp_dat = rbind(dat18,dat19,dat20,dat21,dat22,dat23)

# build our "prediction" dataframe
pred_dat = left_join(YrC_pred,lkp_dat, join_by(Year,County.Code))
head(pred_dat)
</code></pre>
  </div>
</div>

<div class="card shadow-sm mb-4">
  <div class="card-header bg-secondary text-white">
    Output
  </div>
  <div class="card-body bg-white">
<pre class="mb-0"><code>
&gt; head(pred_dat)
  Year Year.Code              County County.Code     Deaths Population Poverty Unemployment School Disabled Parent
1 2018      2018    Allen County, KS       20001 Suppressed      12630    1989          281    697     2271    383
2 2018      2018 Anderson County, KS       20003 Suppressed       7852    1068          106    454     1058    189
3 2018      2018 Atchison County, KS       20005 Suppressed      16363    2643          376    761     2469    411
4 2018      2018   Barton County, KS       20009 Suppressed      26791    4395          541   2052     4011   1120
5 2018      2018   Butler County, KS       20015 Suppressed      66468    6687         1378   3250     7276   1933
6 2018      2018    Chase County, KS       20017 Suppressed       2645     321           52    185      441     64
  Mobile Crowd
1    545    62
2    292    36
3    303   103
4    924   151
5   1892   514
6    128    24
</code></pre>
  </div>
</div>

<div class="card shadow-sm mb-4">
  <div class="card-header bg-dark text-white">
    R Code
  </div>
  <div class="card-body bg-light">
<pre class="mb-0"><code>
# predict the missing values
Pred_m1 = predict(m1, newdata = pred_dat)
Pred_m2 = predict(m2, newdata = pred_dat)

# hisotgrams for comparison
par(mfrow = c(1,2), mar = c(4,4,4,1))
hist(Pred_m1, xlab = "Overdose related deaths", main = "Model 1 Predictions", col = "white")
hist(Pred_m2, xlab = "Overdose related deaths", main = "Model 2 Predictions", col = "white")
</code></pre>
  </div>
</div>

{% include figure.html img="model_perform_df26.png" alt="model 1 and 2 performance shown via histogram" width="125%" %}

<br>

{% include alert.html text="Check for impossible (or insane) values!" align="center" color="danger" %}

<br>

<br>

## Let's finalize our data

<br>

### UCR Program

>"The Uniform Crime Reporting (UCR) Program generates reliable statistics for use in law enforcement. It also provides information for students of criminal justice, researchers, the media, and the public. The program has been providing crime statistics since 1930." - Federal Bureau of Investigation

<br>

**We'll match this data to the data we've built prior and try to inform some decisions on overdose deaths using crime statistics.**

<br>

<div class="card shadow-sm mb-4">
  <div class="card-header bg-dark text-white">
    R Code
  </div>
  <div class="card-body bg-light">
<pre class="mb-0"><code>
# finalize alignment of the overdose data
pred_dat$Deaths = Pred_m1
final_OD = rbind(full_dat,pred_dat)

# make a new subset to be added with the crime data
OD_add = subset(final_OD, final_OD$Year &lt; 2022)

# collapse the crime data to match the overdose data
Crime_add = ks_crime %&gt;%
  group_by(year,fips_state_county_code) %&gt;%
  summarise(All_crime = sum(actual_all_crimes),
            Violent = sum(actual_index_violent))

# align the column names and variable types
colnames(Crime_add)[c(1,2)] = c("Year", "County.Code")
Crime_add$County.Code = as.integer(Crime_add$County.Code) 

# join everything together
KS_OD_YrC_Aux = left_join(OD_add, Crime_add, join_by(Year, County.Code))
head(KS_OD_YrC_Aux)
</code></pre>
  </div>
</div>

<div class="card shadow-sm mb-4">
  <div class="card-header bg-secondary text-white">
    Output
  </div>
  <div class="card-body bg-white">
<pre class="mb-0"><code>
&gt; head(KS_OD_YrC_Aux)
  Year Year.Code              County County.Code Deaths Population Poverty Unemployment School Disabled Parent Mobile
1 2018      2018   Barber County, KS       20007      0       4733     729           38    280      742    135    180
2 2018      2018  Bourbon County, KS       20011      0      14702    2359          161    846     2963    484    505
3 2018      2018    Brown County, KS       20013      0       9664    1358          168    484     1532    306    173
4 2018      2018 Cherokee County, KS       20021      0      20331    2763          427   1535     4528    576   1129
5 2018      2018 Cheyenne County, KS       20023      0       2677     249           38    124      416     85     70
6 2018      2018    Clark County, KS       20025      0       2053     220           12     91      273     89     74
  Crowd All_crime Violent
1    33        44       3
2   221       623      70
3    69       319      32
4    94       716      61
5     6        59       3
6    23        30       3
</code></pre>
  </div>
</div>

<br>

> Just as before, the benefit of a strong investigation into root cause is that we can keep our methods of data analysis simple and interpretable. There's not much more interpretable than a line, is there?

<div class="card shadow-sm mb-4">
  <div class="card-header bg-dark text-white">
    R Code
  </div>
  <div class="card-body bg-light">
<pre class="mb-0"><code>
ggplot(KS_OD_YrC_Aux,
       aes(x = All_crime, y = as.numeric(Deaths))) +
  geom_point(alpha = 0.4) + 
  labs(x = "Violent crime incidents", y = "Deaths attributed to overdose") +
  geom_smooth(method = "lm", se = FALSE, color = "#512885") +
  theme_minimal()

ggplot(KS_OD_YrC_Aux,
       aes(x = Violent, y = as.numeric(Deaths))) +
  geom_point(alpha = 0.4) +
  labs(x = "All crime incidents", y = "Deaths attributed to overdose") +
  geom_smooth(method = "lm", se = FALSE, color = "#512885") +
  theme_minimal()

ggplot(KS_OD_YrC_Aux,
       aes(x = Poverty, y = as.numeric(Deaths))) +
  geom_point(alpha = 0.4) +
  labs(x = "Population below the poverty line", y = "Deaths attributed to overdose") +
  geom_smooth(method = "lm", se = FALSE, color = "#512885") +
  theme_minimal()
</code></pre>
  </div>
</div>

{% include figure.html img="all_crime_df26.png" alt="all crime incidence in a scatter with overdose deaths" width="125%" %}

{% include figure.html img="violent_df26.png" alt="violent crime incidence in a scatter with overdose deaths" width="125%" %}

{% include figure.html img="poverty_df26.png" alt="population below the poverty line is a scatter with overdose deaths" width="125%" %}

<br>

## Cautionary quotes

> "...the objectivist sweeps them under the carpet by calling assumptions knowledge, and he basks in the glorious objectivity of science." - I.J. Good

We made a lot of assumptions to get here, look out for egregious ones in your process!

<br>

2. "It's easy to lie with statistics; it is easier to lie without them." - Frederick Mosteller

Be sure to show as much of the truth as you can in your presentation. Even a poorly scaled figure can warp a decision maker's perspective enough to cause errors.

<br>

3. "Most of the time, when you get an amazing, counterintuitive result, it means you have screwed up the experiment." - Michael Wigler

We want significant results, but don't get married to the idea of them. More than likely what we'll find is very minimal *and that's okay*!

<br>

<br>

# Questions?

<br>

<br>

<br>
