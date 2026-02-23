---
title: Solving problems in your data
nav: Data
topics: Data preparation and cleaning
---

<br>

{% capture text %}

Data cleaning is a necessary evil in data science. For every summary statistic, graphic, and model we fit there were hundreds of gsubs, joins, and imputations that got us there.

Before we can analyze our data we need to work through the three heads of data preparation:

1. **Shape**

2. **Type**

3. **Validity**

{% endcapture %}
{% include card.html text=text title="Messy data is an oxymoron" img="messy-data.png"%}

<br>

---

# 1. Shape

<br>

{% capture text %}

Prior to shaping the data, we need to answer these three questions:

- What does one row represent?

- What does one column represent?

- What is the unit of observation?

The structure of our data usually provides hints as to what shape is best.

{% endcapture %}
{% include card.html text=text header="Start with structure" %}

<br>

## Wide vs Long

<br>

<div class="container my-4">
  <div class="row row-cols-1 row-cols-md-2 g-4">

    <div class="col">
      <div class="card h-100 shadow-sm border-3 border-primary">
        <div class="card-body">
          <h4 class="card-title fw-bold">Wide</h4>
          <ul>
            <li>One row per entity</li>
            <li>Repeated measures across columns</li>
            <li>Spreadsheet-friendly</li>
            <li>Harder for models</li>
          </ul>
        </div>
      </div>
    </div>

    <div class="col">
      <div class="card h-100 shadow-sm border-3 border-success">
        <div class="card-body">
          <h4 class="card-title fw-bold">Long</h4>
          <ul>
            <li>One row per observation</li>
            <li>Repeated measures stacked</li>
            <li>Model-friendly</li>
            <li>Preferred for most graphics</li>
          </ul>
        </div>
      </div>
    </div>

  </div>
</div>

<br>

---

## Junk Space

<br>

> When shaping or building data, be weary of junk space. This includes white space, rarely used descriptive columns, or just bad naming inconsistencies. 

<br>

<div class="container my-4">
  <div class="row row-cols-1 row-cols-md-3 g-4">

    <div class="col">
      <div class="card h-100 text-center shadow-sm">
        <div class="card-body">
          <h5>Male</h5>
        </div>
      </div>
    </div>

    <div class="col">
      <div class="card h-100 text-center shadow-sm">
        <div class="card-body">
          <h5> male</h5>
        </div>
      </div>
    </div>

    <div class="col">
      <div class="card h-100 text-center shadow-sm">
        <div class="card-body">
          <h5>MALE </h5>
        </div>
      </div>
    </div>

  </div>
</div>

<br>

{% include alert.html text="These are three different categories to a computer." align="center" color="danger" %}

<br>

<br>

---

# 2. Type

<br>

{% include jumbotron.html heading="Data types determine behavior" text="The same values behave differently depending on how they are stored. Identifying the right category to place each value into is an essential step in the data cleaning process." border=true %}

<br>

<div class="container my-4">
  <div class="row row-cols-1 row-cols-md-3 g-4">

    <div class="col">
      <div class="card h-100 shadow-sm border-3 border-info">
        <div class="card-body">
          <h4 class="fw-bold">Categorical</h4>
          <ul>
            <li>Groups or labels</li>
            <li>Nominal vs. ordinal</li>
            <li>Inconsistently coded</li>
            <li>Integers ≠ numerics</li>
          </ul>
        </div>
      </div>
    </div>

    <div class="col">
      <div class="card h-100 shadow-sm border-3 border-info">
        <div class="card-body">
          <h4 class="fw-bold">Numeric</h4>
          <ul>
            <li>Numeric measures</li>
            <li>May contain symbols</li>
            <li>Check for impossible values</li>
            <li>Note the meaning of zero</li>
          </ul>
        </div>
      </div>
    </div>

    <div class="col">
      <div class="card h-100 shadow-sm border-3 border-info">
        <div class="card-body">
          <h4 class="fw-bold">Time & Space</h4>
          <ul>
            <li>Keep everything in context</li>
            <li>Date parsing matters</li>
            <li>Standardize coordinate systems</li>
          </ul>
        </div>
      </div>
    </div>

  </div>
</div>

<br>

---

## Data Dictionaries

<br>

{% capture text %}

A data dictionary tells you:

- What a variable claims to measure

- Units of measurement

- Allowed values

- Valid ranges

Cleaning without metadata creates false assumptions.

{% endcapture %}
{% include card.html text=text header="Context prevents mistakes" %}

<br>

<br>

---

# 3. Validity

<br>

> There's a difference between screening for errors and data validation. Failure to screen errors can prevent an analysis from happening. Failure to validate can make an analysis unreliable. 

<br>

{% include jumbotron.html heading="Trust but verify" text="Cleaning is quality control." border=true %}

<br>

## Missing Data Decisions

<br>

<div class="container my-4">
  <div class="row row-cols-1 row-cols-md-3 g-4">

    <div class="col">
      <div class="card h-100 text-center shadow-sm border-3 border-warning">
        <div class="card-body">
          <h4 class="fw-bold">Remove</h4>
          <p>Delete incomplete records.</p>
        </div>
      </div>
    </div>

    <div class="col">
      <div class="card h-100 text-center shadow-sm border-3 border-warning">
        <div class="card-body">
          <h4 class="fw-bold">Impute</h4>
          <p>Estimate missing values.</p>
        </div>
      </div>
    </div>

    <div class="col">
      <div class="card h-100 text-center shadow-sm border-3 border-warning">
        <div class="card-body">
          <h4 class="fw-bold">Flag</h4>
          <p>Preserve missingness as information.</p>
        </div>
      </div>
    </div>

  </div>
</div>

<br>

---

## Joins & Keys

<br>

{% capture text %}

When combining datasets:

- Do keys match exactly?

- Is the join one-to-one or one-to-many?

- Did row counts change?

Always check before and after.

{% endcapture %}
{% include card.html text=text header="Misalignment creates silent errors" %}

<br>

---

## Duplicate Records

<br>

{% include alert.html text="Duplicate IDs inflate your sample size and bias your results." align="center" color="danger" %}

<br>

---

