# CHNIP Data Dictionary

## 1. Purpose

This Data Dictionary defines the fields contained in the CHNIP MEAL dataset.

It provides a standardized description of each variable, including its meaning, data type, expected values and role in the analysis.

The purpose is to support consistent data entry, cleaning, analysis and interpretation.

---

## 2. Dataset Fields

| Field Name          | Description                                            | Data Type   | Example                            | Required    |
| ------------------- | ------------------------------------------------------ | ----------- | ---------------------------------- | ----------- |
| Reporting Month     | Month in which the activity or result was reported     | Text/Date   | January 2026                       | Yes         |
| Month Date          | Standardized date representing the reporting month     | Date        | 2026-01-01                         | Yes         |
| Community           | Community where the activity was implemented           | Text        | Community A                        | Yes         |
| Indicator ID        | Unique identifier assigned to the indicator            | Text        | CHN-OUT-001                        | Yes         |
| Indicator           | Name of the monitored indicator                        | Text        | Children screened for malnutrition | Yes         |
| Indicator Level     | Results-framework level of the indicator               | Categorical | Output                             | Yes         |
| Unit                | Unit used to measure the indicator                     | Categorical | Number                             | Yes         |
| Target              | Expected result for the reporting period               | Numeric     | 100                                | Yes         |
| Actual              | Reported result achieved during the reporting period   | Numeric     | 92                                 | Yes         |
| Male                | Number of male beneficiaries, where applicable         | Numeric     | 45                                 | Conditional |
| Female              | Number of female beneficiaries, where applicable       | Numeric     | 47                                 | Conditional |
| Achievement %       | Percentage of target achieved                          | Numeric     | 92.0                               | Yes         |
| Status              | Performance classification based on achievement        | Categorical | On Track                           | Yes         |
| Data Source         | Primary source from which the reported data originated | Text        | Screening Register                 | Yes         |
| Report Submitted    | Whether the expected report was submitted              | Categorical | Yes                                | Yes         |
| Verification Status | Status of data verification                            | Categorical | Verified                           | Yes         |

---

# 3. Field-Level Definitions

## Reporting Month

**Definition:**
The month corresponding to the reporting period in which the activity or result was recorded.

**Expected format:**
Month and year.

**Example:**
January 2026

---

## Month Date

**Definition:**
A standardized date representing the first day of the reporting month.

**Purpose:**
Used for sorting, time-series analysis and Power BI visualizations.

**Example:**

`2026-01-01`

---

## Community

**Definition:**
The geographic community where the monitored activity took place.

**Allowed values:**

* Community A
* Community B
* Community C
* Community D
* Community E

**Data-quality requirement:**
Community names must be standardized. Variations such as `community c`, `Community-C` or spelling errors should be corrected during data cleaning.

---

## Indicator ID

**Definition:**
A unique code assigned to each indicator.

**Examples:**

* CHN-OUT-001
* CHN-OUT-002
* CHN-OUT-003

**Purpose:**
Prevents ambiguity when indicators have similar names and supports consistent database management.

---

## Indicator

**Definition:**
The formal name of the indicator being monitored.

**Example:**

`Children screened for malnutrition`

**Data-quality requirement:**
Indicator names should match the approved Indicator Reference Sheet.

---

## Indicator Level

**Definition:**
The position of the indicator within the project's results framework.

**Allowed values:**

* Output
* Outcome

---

## Unit

**Definition:**
The measurement unit used to report the indicator.

**Allowed values:**

* Number
* Percentage

---

## Target

**Definition:**
The expected level of achievement for the indicator during the reporting period.

**Data type:**
Numeric

**Example:**

`100`

---

## Actual

**Definition:**
The result reported as achieved during the relevant reporting period.

**Data type:**
Numeric

**Example:**

`92`

**Data-quality requirement:**
Actual values should be supported by appropriate source documentation.

---

## Male

**Definition:**
Number of male beneficiaries represented in the reported result where sex disaggregation applies.

**Data type:**
Numeric

**Conditional field:**
Only applicable to indicators for which sex-disaggregated beneficiary data are collected.

---

## Female

**Definition:**
Number of female beneficiaries represented in the reported result where sex disaggregation applies.

**Data type:**
Numeric

**Conditional field:**
Only applicable to indicators for which sex-disaggregated beneficiary data are collected.

---

## Achievement %

**Definition:**
Percentage of the reporting-period target achieved.

### Calculation

For numerical output indicators:

`Achievement % = Actual ÷ Target × 100`

**Example:**

Actual = 92

Target = 100

Achievement = 92%

---

## Status

**Definition:**
Classification of indicator performance based on the achievement percentage.

### Classification

|          Achievement | Status          |
| -------------------: | --------------- |
|                 ≥90% | On Track        |
|               70–89% | Needs Attention |
|                 <70% | Off Track       |
| Missing/invalid data | Data Issue      |

**Important:**
Performance status should not be interpreted as program performance until relevant data-quality checks have been completed.

---

## Data Source

**Definition:**
The primary document or system from which the reported result was obtained.

**Examples:**

* Screening Register
* Outreach Register
* Referral Register
* Activity Report
* Training Attendance
* Service Records

---

## Report Submitted

**Definition:**
Indicates whether the expected reporting submission was received for the reporting period.

**Allowed values:**

* Yes
* No

---

## Verification Status

**Definition:**
Indicates whether the reported information has undergone the required verification process.

**Allowed values:**

* Verified
* Pending
* Requires Correction

---

# 4. Data Validation Rules

The following validation rules should be applied during data cleaning:

1. Indicator IDs must correspond to the approved Indicator Reference Sheet.
2. Community names must use standardized naming conventions.
3. Target values must be numeric and greater than zero where applicable.
4. Actual values must be numeric where a result has been reported.
5. Actual values should not be negative.
6. Achievement percentages should be recalculated rather than blindly accepted from source files.
7. Male and female totals should be checked against the corresponding reported total where applicable.
8. Duplicate records should be identified and investigated.
9. Missing values should be flagged rather than silently replaced.
10. Reports marked as not submitted should not automatically be interpreted as zero performance.
11. Indicator definitions should remain consistent across reporting periods.
12. Records requiring verification should be clearly flagged.

---

# 5. Data Cleaning Principles

The cleaning process will follow these principles:

### Preserve the raw data

The original dataset should never be overwritten.

### Document corrections

Important corrections should be recorded so that changes can be traced.

### Standardize categorical fields

Variables such as community, indicator and status should use controlled values.

### Investigate anomalies

Unusually high, low or inconsistent values should be investigated rather than automatically deleted.

### Separate data quality from program performance

A missing or questionable value is a data-quality issue and should not automatically be interpreted as poor program performance.

---

# 6. Dataset Workflow

```text
Raw Data
   ↓
Data Validation
   ↓
Data Cleaning
   ↓
Data Quality Assessment
   ↓
Indicator Calculation
   ↓
Performance Analysis
   ↓
Dashboard
   ↓
Findings & Recommendations
```

---

## 7. Version Control

Changes to the dataset should be documented through GitHub version control.

Each major update should indicate:

* What was changed
* Why it was changed
* Date of change
* Person responsible for the change

This supports transparency and reproducibility within the MEAL workflow.
