# School-District-Data-Analytics

## Purpose

The purpose of this project was to understand the school data of the school district. The district data was provided by UC Berkeley extension to further master and practice analysis using Pandas. 

## Objective 
 
The analysis was peformed to understand the quantative data and indicate the outstanding school perfomances along with the schools that need the most attention for the district leadership to focus on.

## Approach
1. Data Cleaning (done in the backend)
    - Check for empty columns 
    - Drop the empty columns 
    - Check for value under each column and clean the data if needed
    - Rename Columns for better understanding

2. Perform Analysis 
    * Take each topic and perform quantative analysis. 
    * Put it into a summary table for display

3. Draw Conclusions 
    * Based on the analysis, summarize the conclusions. 

## Conclusions 
* As a whole, schools with higher budgets, did not yield better test results. By contrast, schools with higher spending per student actually (\$645-675) underperformed compared to schools with smaller budgets (<\$585 per student).

* As a whole, smaller and medium sized schools dramatically out-performed large sized schools on passing math performances (89-91% passing vs 67%).

* As a whole, charter schools out-performed the public district schools across all metrics. However, more analysis will be required to glean if the effect is due to school practices or the fact that charter schools tend to serve smaller student populations per school. 

## Actions
* The small/medium sized schools that outperformed larger schools indicated the ideal class size for optimal performance. Thus the maximum head count should be decreased.  

* The school with higher budget didn't out-performed, thus their budget should be audited and a proper distribution to high performing schools should be made. 

* These result can be used to set the upcoming budget for the year to focus on the schools that have not performed well while maintaining the success rate of the other schools. 

## Report 
`PDF/HTML can be found in the 'Reports' Folder.`

`Please see the HTML version for the best readability.`

**Below is the markdown version:**

## School District Report

### Importing Modules


```python
import os 
import pandas as pd
```

### Reading in Data Files 


```python
schools_data_csvpath = os.path.join('data','schools_complete.csv')
students_data_csvpath = os.path.join('data','students_complete.csv')
```

### School DataFrame Display


```python
schools_df = pd.read_csv(schools_data_csvpath)

schools_df.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>School ID</th>
      <th>name</th>
      <th>type</th>
      <th>size</th>
      <th>budget</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>Huang High School</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>Figueroa High School</td>
      <td>District</td>
      <td>2949</td>
      <td>1884411</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>Shelton High School</td>
      <td>Charter</td>
      <td>1761</td>
      <td>1056600</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>Hernandez High School</td>
      <td>District</td>
      <td>4635</td>
      <td>3022020</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>Griffin High School</td>
      <td>Charter</td>
      <td>1468</td>
      <td>917500</td>
    </tr>
  </tbody>
</table>
</div>



### Students DataFrame Display


```python
students_df = pd.read_csv(students_data_csvpath)

students_df.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Student ID</th>
      <th>name</th>
      <th>gender</th>
      <th>grade</th>
      <th>school</th>
      <th>reading_score</th>
      <th>math_score</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>Paul Bradley</td>
      <td>M</td>
      <td>9th</td>
      <td>Huang High School</td>
      <td>66</td>
      <td>79</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>Victor Smith</td>
      <td>M</td>
      <td>12th</td>
      <td>Huang High School</td>
      <td>94</td>
      <td>61</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>Kevin Rodriguez</td>
      <td>M</td>
      <td>12th</td>
      <td>Huang High School</td>
      <td>90</td>
      <td>60</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>Dr. Richard Scott</td>
      <td>M</td>
      <td>12th</td>
      <td>Huang High School</td>
      <td>67</td>
      <td>58</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>Bonnie Ray</td>
      <td>F</td>
      <td>9th</td>
      <td>Huang High School</td>
      <td>97</td>
      <td>84</td>
    </tr>
  </tbody>
</table>
</div>




```python
# changing names to merge
schools_df = schools_df.rename(columns={'name':'school'})

schools_df.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>School ID</th>
      <th>school</th>
      <th>type</th>
      <th>size</th>
      <th>budget</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>Huang High School</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>Figueroa High School</td>
      <td>District</td>
      <td>2949</td>
      <td>1884411</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>Shelton High School</td>
      <td>Charter</td>
      <td>1761</td>
      <td>1056600</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>Hernandez High School</td>
      <td>District</td>
      <td>4635</td>
      <td>3022020</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>Griffin High School</td>
      <td>Charter</td>
      <td>1468</td>
      <td>917500</td>
    </tr>
  </tbody>
</table>
</div>



### Merged DataFrame Display: District Data


```python
district_df = pd.merge(schools_df,students_df,on='school')

district_df.head(5)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>School ID</th>
      <th>school</th>
      <th>type</th>
      <th>size</th>
      <th>budget</th>
      <th>Student ID</th>
      <th>name</th>
      <th>gender</th>
      <th>grade</th>
      <th>reading_score</th>
      <th>math_score</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>Huang High School</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>0</td>
      <td>Paul Bradley</td>
      <td>M</td>
      <td>9th</td>
      <td>66</td>
      <td>79</td>
    </tr>
    <tr>
      <th>1</th>
      <td>0</td>
      <td>Huang High School</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>1</td>
      <td>Victor Smith</td>
      <td>M</td>
      <td>12th</td>
      <td>94</td>
      <td>61</td>
    </tr>
    <tr>
      <th>2</th>
      <td>0</td>
      <td>Huang High School</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>2</td>
      <td>Kevin Rodriguez</td>
      <td>M</td>
      <td>12th</td>
      <td>90</td>
      <td>60</td>
    </tr>
    <tr>
      <th>3</th>
      <td>0</td>
      <td>Huang High School</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>3</td>
      <td>Dr. Richard Scott</td>
      <td>M</td>
      <td>12th</td>
      <td>67</td>
      <td>58</td>
    </tr>
    <tr>
      <th>4</th>
      <td>0</td>
      <td>Huang High School</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>4</td>
      <td>Bonnie Ray</td>
      <td>F</td>
      <td>9th</td>
      <td>97</td>
      <td>84</td>
    </tr>
  </tbody>
</table>
</div>



### District Summary

**High level snapshot (in table form) of the district's key metrics, including:**
* Total Schools
* Total Students
* Total Budget
* Average Math Score
* Average Reading Score
* % Passing Math
* % Passing Reading
* Overall Passing Rate (Average of the above two)


```python
 total_schools = len(district_df['school'].unique())
total_students = district_df['Student ID'].count()
total_budget = schools_df['budget'].sum()
avg_math_score = students_df['math_score'].mean()
avg_reading_score= students_df['reading_score'].mean()
percent_passing_reading =(students_df.loc[students_df['reading_score']>70]['reading_score'].count())/students_df['reading_score'].count()*100
percent_passing_math = students_df.loc[students_df['math_score']>70]['math_score'].count()/students_df['math_score'].count()*100
overall_passing_rate = (percent_passing_math + percent_passing_reading)/2


district_summary_df = pd.DataFrame({
    'Total Schools': total_schools,
    'Total Students':total_students,
    'Total budget': total_budget,
    'Average Math Score': avg_math_score,
    'Average Reading Score': avg_reading_score,
    '% Passing Reading': percent_passing_reading,
    '% Passing Math': percent_passing_math,
    'Overall Passing Rate': overall_passing_rate
}, index = [0])

district_summary_df['Total Students'] = district_summary_df['Total Students'].map(" {:,.0f}".format)
district_summary_df['Total budget'] = district_summary_df['Total budget'].map(" ${:,.0f}".format)
district_summary_df['Average Math Score'] = district_summary_df['Average Math Score'].map(" {:,.1f}".format)
district_summary_df['Average Reading Score'] = district_summary_df['Average Reading Score'].map(" {:,.1f}".format)
district_summary_df['% Passing Reading'] = district_summary_df['% Passing Reading'].map(" {:,.1f}%".format)
district_summary_df['% Passing Math'] = district_summary_df['% Passing Math'].map(" {:,.1f}%".format)
district_summary_df['Overall Passing Rate'] = district_summary_df['Overall Passing Rate'].map(" {:,.1f}%".format)

district_summary_df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Total Schools</th>
      <th>Total Students</th>
      <th>Total budget</th>
      <th>Average Math Score</th>
      <th>Average Reading Score</th>
      <th>% Passing Reading</th>
      <th>% Passing Math</th>
      <th>Overall Passing Rate</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>15</td>
      <td>39,170</td>
      <td>$24,649,428</td>
      <td>79.0</td>
      <td>81.9</td>
      <td>83.0%</td>
      <td>72.4%</td>
      <td>77.7%</td>
    </tr>
  </tbody>
</table>
</div>



### School Summary

**An overview table that summarizes key metrics about each school, including:**
* School Name
* School Type
* Total Students
* Total School Budget
* Per Student Budget
* Average Math Score
* Average Reading Score
* % Passing Math
* % Passing Reading
* Overall Passing Rate (Average of the above two)


```python
total_students = district_df.groupby('school').count()['Student ID']
total_budget = district_df.groupby('school').mean()['budget']
per_student_budget = total_budget/total_students
avg_math_score = district_df.groupby('school').mean()['math_score']
avg_reading_score = district_df.groupby('school').mean()['reading_score']
percent_passing_math = district_df.loc[district_df['math_score'] >70].groupby('school').count()['math_score'] / total_students * 100
percent_passing_reading = district_df.loc[district_df['reading_score'] >70].groupby('school').count()['reading_score'] / total_students * 100
percent_total = (percent_passing_math + percent_passing_reading)/2
school_types = schools_df.set_index(["school"])["type"]

school_summary_df = pd.DataFrame({
    'Type':school_types,
    'Total Students': total_students,
    'Total Budget': total_budget,
    'Per Student Budget': per_student_budget,
    'Avg. Math Score': avg_math_score,
    'Avg. Reading Score': avg_reading_score,
    '% Passing Math': percent_passing_math,
    '% Passing Reading': percent_passing_reading,
    'Overall Passing Rate': percent_total
})

school_summary_df['Total Budget'] = school_summary_df['Total Budget'].map(" ${:,.0f}".format)
#school_summary_df['Per Student Budget'] = school_summary_df['Per Student Budget'].map(" ${:,.0f}".format)
#school_summary_df['Avg. Math Score'] = school_summary_df['Avg. Math Score'].map(" {:,.1f}".format)
#school_summary_df['Avg. Reading Score'] = school_summary_df['Avg. Reading Score'].map(" {:,.1f}".format)
# school_summary_df['% Passing Reading'] = school_summary_df['% Passing Reading'].map(" {:,.1f}%".format)
# school_summary_df['% Passing Math'] = school_summary_df['% Passing Math'].map(" {:,.1f}%".format)
# school_summary_df['Overall Passing Rate'] = school_summary_df['Overall Passing Rate'].map(" {:,.1f}%".format)
school_summary_df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Type</th>
      <th>Total Students</th>
      <th>Total Budget</th>
      <th>Per Student Budget</th>
      <th>Avg. Math Score</th>
      <th>Avg. Reading Score</th>
      <th>% Passing Math</th>
      <th>% Passing Reading</th>
      <th>Overall Passing Rate</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Bailey High School</th>
      <td>District</td>
      <td>4976</td>
      <td>$3,124,928</td>
      <td>628.0</td>
      <td>77.048432</td>
      <td>81.033963</td>
      <td>64.630225</td>
      <td>79.300643</td>
      <td>71.965434</td>
    </tr>
    <tr>
      <th>Cabrera High School</th>
      <td>Charter</td>
      <td>1858</td>
      <td>$1,081,356</td>
      <td>582.0</td>
      <td>83.061895</td>
      <td>83.975780</td>
      <td>89.558665</td>
      <td>93.864370</td>
      <td>91.711518</td>
    </tr>
    <tr>
      <th>Figueroa High School</th>
      <td>District</td>
      <td>2949</td>
      <td>$1,884,411</td>
      <td>639.0</td>
      <td>76.711767</td>
      <td>81.158020</td>
      <td>63.750424</td>
      <td>78.433367</td>
      <td>71.091896</td>
    </tr>
    <tr>
      <th>Ford High School</th>
      <td>District</td>
      <td>2739</td>
      <td>$1,763,916</td>
      <td>644.0</td>
      <td>77.102592</td>
      <td>80.746258</td>
      <td>65.753925</td>
      <td>77.510040</td>
      <td>71.631982</td>
    </tr>
    <tr>
      <th>Griffin High School</th>
      <td>Charter</td>
      <td>1468</td>
      <td>$917,500</td>
      <td>625.0</td>
      <td>83.351499</td>
      <td>83.816757</td>
      <td>89.713896</td>
      <td>93.392371</td>
      <td>91.553134</td>
    </tr>
    <tr>
      <th>Hernandez High School</th>
      <td>District</td>
      <td>4635</td>
      <td>$3,022,020</td>
      <td>652.0</td>
      <td>77.289752</td>
      <td>80.934412</td>
      <td>64.746494</td>
      <td>78.187702</td>
      <td>71.467098</td>
    </tr>
    <tr>
      <th>Holden High School</th>
      <td>Charter</td>
      <td>427</td>
      <td>$248,087</td>
      <td>581.0</td>
      <td>83.803279</td>
      <td>83.814988</td>
      <td>90.632319</td>
      <td>92.740047</td>
      <td>91.686183</td>
    </tr>
    <tr>
      <th>Huang High School</th>
      <td>District</td>
      <td>2917</td>
      <td>$1,910,635</td>
      <td>655.0</td>
      <td>76.629414</td>
      <td>81.182722</td>
      <td>63.318478</td>
      <td>78.813850</td>
      <td>71.066164</td>
    </tr>
    <tr>
      <th>Johnson High School</th>
      <td>District</td>
      <td>4761</td>
      <td>$3,094,650</td>
      <td>650.0</td>
      <td>77.072464</td>
      <td>80.966394</td>
      <td>63.852132</td>
      <td>78.281874</td>
      <td>71.067003</td>
    </tr>
    <tr>
      <th>Pena High School</th>
      <td>Charter</td>
      <td>962</td>
      <td>$585,858</td>
      <td>609.0</td>
      <td>83.839917</td>
      <td>84.044699</td>
      <td>91.683992</td>
      <td>92.203742</td>
      <td>91.943867</td>
    </tr>
    <tr>
      <th>Rodriguez High School</th>
      <td>District</td>
      <td>3999</td>
      <td>$2,547,363</td>
      <td>637.0</td>
      <td>76.842711</td>
      <td>80.744686</td>
      <td>64.066017</td>
      <td>77.744436</td>
      <td>70.905226</td>
    </tr>
    <tr>
      <th>Shelton High School</th>
      <td>Charter</td>
      <td>1761</td>
      <td>$1,056,600</td>
      <td>600.0</td>
      <td>83.359455</td>
      <td>83.725724</td>
      <td>89.892107</td>
      <td>92.617831</td>
      <td>91.254969</td>
    </tr>
    <tr>
      <th>Thomas High School</th>
      <td>Charter</td>
      <td>1635</td>
      <td>$1,043,130</td>
      <td>638.0</td>
      <td>83.418349</td>
      <td>83.848930</td>
      <td>90.214067</td>
      <td>92.905199</td>
      <td>91.559633</td>
    </tr>
    <tr>
      <th>Wilson High School</th>
      <td>Charter</td>
      <td>2283</td>
      <td>$1,319,574</td>
      <td>578.0</td>
      <td>83.274201</td>
      <td>83.989488</td>
      <td>90.932983</td>
      <td>93.254490</td>
      <td>92.093736</td>
    </tr>
    <tr>
      <th>Wright High School</th>
      <td>Charter</td>
      <td>1800</td>
      <td>$1,049,400</td>
      <td>583.0</td>
      <td>83.682222</td>
      <td>83.955000</td>
      <td>90.277778</td>
      <td>93.444444</td>
      <td>91.861111</td>
    </tr>
  </tbody>
</table>
</div>



### Top Performing Schools (By Passing Rate)

**Table that highlights the *TOP 5* performing schools based on Overall Passing Rate. Include:**
* School Name
* School Type
* Total Students
* Total School Budget
* Per Student Budget
* Average Math Score
* Average Reading Score
* % Passing Math
* % Passing Reading
* Overall Passing Rate (Average of the above two)


```python
school_summary_df = school_summary_df.sort_values('Overall Passing Rate',ascending=False)
school_summary_df.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Type</th>
      <th>Total Students</th>
      <th>Total Budget</th>
      <th>Per Student Budget</th>
      <th>Avg. Math Score</th>
      <th>Avg. Reading Score</th>
      <th>% Passing Math</th>
      <th>% Passing Reading</th>
      <th>Overall Passing Rate</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Wilson High School</th>
      <td>Charter</td>
      <td>2283</td>
      <td>$1,319,574</td>
      <td>578.0</td>
      <td>83.274201</td>
      <td>83.989488</td>
      <td>90.932983</td>
      <td>93.254490</td>
      <td>92.093736</td>
    </tr>
    <tr>
      <th>Pena High School</th>
      <td>Charter</td>
      <td>962</td>
      <td>$585,858</td>
      <td>609.0</td>
      <td>83.839917</td>
      <td>84.044699</td>
      <td>91.683992</td>
      <td>92.203742</td>
      <td>91.943867</td>
    </tr>
    <tr>
      <th>Wright High School</th>
      <td>Charter</td>
      <td>1800</td>
      <td>$1,049,400</td>
      <td>583.0</td>
      <td>83.682222</td>
      <td>83.955000</td>
      <td>90.277778</td>
      <td>93.444444</td>
      <td>91.861111</td>
    </tr>
    <tr>
      <th>Cabrera High School</th>
      <td>Charter</td>
      <td>1858</td>
      <td>$1,081,356</td>
      <td>582.0</td>
      <td>83.061895</td>
      <td>83.975780</td>
      <td>89.558665</td>
      <td>93.864370</td>
      <td>91.711518</td>
    </tr>
    <tr>
      <th>Holden High School</th>
      <td>Charter</td>
      <td>427</td>
      <td>$248,087</td>
      <td>581.0</td>
      <td>83.803279</td>
      <td>83.814988</td>
      <td>90.632319</td>
      <td>92.740047</td>
      <td>91.686183</td>
    </tr>
  </tbody>
</table>
</div>



### Top Performing Schools (By Passing Rate)

**Table that highlights the *Bottom 5* performing schools based on Overall Passing Rate. Include all of the same metrics as above.**



```python
school_summary_df = school_summary_df.sort_values('Overall Passing Rate',ascending=True)
school_summary_df.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Type</th>
      <th>Total Students</th>
      <th>Total Budget</th>
      <th>Per Student Budget</th>
      <th>Avg. Math Score</th>
      <th>Avg. Reading Score</th>
      <th>% Passing Math</th>
      <th>% Passing Reading</th>
      <th>Overall Passing Rate</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Rodriguez High School</th>
      <td>District</td>
      <td>3999</td>
      <td>$2,547,363</td>
      <td>637.0</td>
      <td>76.842711</td>
      <td>80.744686</td>
      <td>64.066017</td>
      <td>77.744436</td>
      <td>70.905226</td>
    </tr>
    <tr>
      <th>Huang High School</th>
      <td>District</td>
      <td>2917</td>
      <td>$1,910,635</td>
      <td>655.0</td>
      <td>76.629414</td>
      <td>81.182722</td>
      <td>63.318478</td>
      <td>78.813850</td>
      <td>71.066164</td>
    </tr>
    <tr>
      <th>Johnson High School</th>
      <td>District</td>
      <td>4761</td>
      <td>$3,094,650</td>
      <td>650.0</td>
      <td>77.072464</td>
      <td>80.966394</td>
      <td>63.852132</td>
      <td>78.281874</td>
      <td>71.067003</td>
    </tr>
    <tr>
      <th>Figueroa High School</th>
      <td>District</td>
      <td>2949</td>
      <td>$1,884,411</td>
      <td>639.0</td>
      <td>76.711767</td>
      <td>81.158020</td>
      <td>63.750424</td>
      <td>78.433367</td>
      <td>71.091896</td>
    </tr>
    <tr>
      <th>Hernandez High School</th>
      <td>District</td>
      <td>4635</td>
      <td>$3,022,020</td>
      <td>652.0</td>
      <td>77.289752</td>
      <td>80.934412</td>
      <td>64.746494</td>
      <td>78.187702</td>
      <td>71.467098</td>
    </tr>
  </tbody>
</table>
</div>



### Math Scores by Grade

**Table that lists the average Math Score for students of each grade level (9th, 10th, 11th, 12th) at each school.**


```python
grade_9 = students_df.loc[students_df['grade']=='9th'].groupby('school').mean()['math_score']
grade_10 = students_df.loc[students_df['grade']=='10th'].groupby('school').mean()['math_score']
grade_11 = students_df.loc[students_df['grade']=='11th'].groupby('school').mean()['math_score']
grade_12 = students_df.loc[students_df['grade']=='12th'].groupby('school').mean()['math_score']
    
grade_summary_math = pd.DataFrame({
    '9th': grade_9,
    '10th': grade_10,
    '11th': grade_11,
    '12th': grade_12
})

grade_summary_math['9th'] = grade_summary_math['9th'].map(" {:,.1f}".format)
grade_summary_math['10th'] = grade_summary_math['10th'].map(" {:,.1f}".format)
grade_summary_math['11th'] = grade_summary_math['11th'].map(" {:,.1f}".format)
grade_summary_math['12th'] = grade_summary_math['12th'].map(" {:,.1f}".format)

grade_summary_math
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>9th</th>
      <th>10th</th>
      <th>11th</th>
      <th>12th</th>
    </tr>
    <tr>
      <th>school</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Bailey High School</th>
      <td>77.1</td>
      <td>77.0</td>
      <td>77.5</td>
      <td>76.5</td>
    </tr>
    <tr>
      <th>Cabrera High School</th>
      <td>83.1</td>
      <td>83.2</td>
      <td>82.8</td>
      <td>83.3</td>
    </tr>
    <tr>
      <th>Figueroa High School</th>
      <td>76.4</td>
      <td>76.5</td>
      <td>76.9</td>
      <td>77.2</td>
    </tr>
    <tr>
      <th>Ford High School</th>
      <td>77.4</td>
      <td>77.7</td>
      <td>76.9</td>
      <td>76.2</td>
    </tr>
    <tr>
      <th>Griffin High School</th>
      <td>82.0</td>
      <td>84.2</td>
      <td>83.8</td>
      <td>83.4</td>
    </tr>
    <tr>
      <th>Hernandez High School</th>
      <td>77.4</td>
      <td>77.3</td>
      <td>77.1</td>
      <td>77.2</td>
    </tr>
    <tr>
      <th>Holden High School</th>
      <td>83.8</td>
      <td>83.4</td>
      <td>85.0</td>
      <td>82.9</td>
    </tr>
    <tr>
      <th>Huang High School</th>
      <td>77.0</td>
      <td>75.9</td>
      <td>76.4</td>
      <td>77.2</td>
    </tr>
    <tr>
      <th>Johnson High School</th>
      <td>77.2</td>
      <td>76.7</td>
      <td>77.5</td>
      <td>76.9</td>
    </tr>
    <tr>
      <th>Pena High School</th>
      <td>83.6</td>
      <td>83.4</td>
      <td>84.3</td>
      <td>84.1</td>
    </tr>
    <tr>
      <th>Rodriguez High School</th>
      <td>76.9</td>
      <td>76.6</td>
      <td>76.4</td>
      <td>77.7</td>
    </tr>
    <tr>
      <th>Shelton High School</th>
      <td>83.4</td>
      <td>82.9</td>
      <td>83.4</td>
      <td>83.8</td>
    </tr>
    <tr>
      <th>Thomas High School</th>
      <td>83.6</td>
      <td>83.1</td>
      <td>83.5</td>
      <td>83.5</td>
    </tr>
    <tr>
      <th>Wilson High School</th>
      <td>83.1</td>
      <td>83.7</td>
      <td>83.2</td>
      <td>83.0</td>
    </tr>
    <tr>
      <th>Wright High School</th>
      <td>83.3</td>
      <td>84.0</td>
      <td>83.8</td>
      <td>83.6</td>
    </tr>
  </tbody>
</table>
</div>



### Reading Scores by Grade

**Table that lists the average Reading Score for students of each grade level (9th, 10th, 11th, 12th) at each school.**


```python
grade_9 = students_df.loc[students_df['grade']=='9th'].groupby('school').mean()['reading_score']
grade_10 = students_df.loc[students_df['grade']=='10th'].groupby('school').mean()['reading_score']
grade_11 = students_df.loc[students_df['grade']=='11th'].groupby('school').mean()['reading_score']
grade_12 = students_df.loc[students_df['grade']=='12th'].groupby('school').mean()['reading_score']
    
grade_summary_reading = pd.DataFrame({
    '9th': grade_9,
    '10th': grade_10,
    '11th': grade_11,
    '12th': grade_12
})

grade_summary_reading['9th'] = grade_summary_reading['9th'].map(" {:,.1f}".format)
grade_summary_reading['10th'] = grade_summary_reading['10th'].map(" {:,.1f}".format)
grade_summary_reading['11th'] = grade_summary_reading['11th'].map(" {:,.1f}".format)
grade_summary_reading['12th'] = grade_summary_reading['12th'].map(" {:,.1f}".format)

grade_summary_reading
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>9th</th>
      <th>10th</th>
      <th>11th</th>
      <th>12th</th>
    </tr>
    <tr>
      <th>school</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Bailey High School</th>
      <td>81.3</td>
      <td>80.9</td>
      <td>80.9</td>
      <td>80.9</td>
    </tr>
    <tr>
      <th>Cabrera High School</th>
      <td>83.7</td>
      <td>84.3</td>
      <td>83.8</td>
      <td>84.3</td>
    </tr>
    <tr>
      <th>Figueroa High School</th>
      <td>81.2</td>
      <td>81.4</td>
      <td>80.6</td>
      <td>81.4</td>
    </tr>
    <tr>
      <th>Ford High School</th>
      <td>80.6</td>
      <td>81.3</td>
      <td>80.4</td>
      <td>80.7</td>
    </tr>
    <tr>
      <th>Griffin High School</th>
      <td>83.4</td>
      <td>83.7</td>
      <td>84.3</td>
      <td>84.0</td>
    </tr>
    <tr>
      <th>Hernandez High School</th>
      <td>80.9</td>
      <td>80.7</td>
      <td>81.4</td>
      <td>80.9</td>
    </tr>
    <tr>
      <th>Holden High School</th>
      <td>83.7</td>
      <td>83.3</td>
      <td>83.8</td>
      <td>84.7</td>
    </tr>
    <tr>
      <th>Huang High School</th>
      <td>81.3</td>
      <td>81.5</td>
      <td>81.4</td>
      <td>80.3</td>
    </tr>
    <tr>
      <th>Johnson High School</th>
      <td>81.3</td>
      <td>80.8</td>
      <td>80.6</td>
      <td>81.2</td>
    </tr>
    <tr>
      <th>Pena High School</th>
      <td>83.8</td>
      <td>83.6</td>
      <td>84.3</td>
      <td>84.6</td>
    </tr>
    <tr>
      <th>Rodriguez High School</th>
      <td>81.0</td>
      <td>80.6</td>
      <td>80.9</td>
      <td>80.4</td>
    </tr>
    <tr>
      <th>Shelton High School</th>
      <td>84.1</td>
      <td>83.4</td>
      <td>84.4</td>
      <td>82.8</td>
    </tr>
    <tr>
      <th>Thomas High School</th>
      <td>83.7</td>
      <td>84.3</td>
      <td>83.6</td>
      <td>83.8</td>
    </tr>
    <tr>
      <th>Wilson High School</th>
      <td>83.9</td>
      <td>84.0</td>
      <td>83.8</td>
      <td>84.3</td>
    </tr>
    <tr>
      <th>Wright High School</th>
      <td>83.8</td>
      <td>83.8</td>
      <td>84.2</td>
      <td>84.1</td>
    </tr>
  </tbody>
</table>
</div>



### Scores by School Spending

**Table that breaks down school performances based on average Spending Ranges (Per Student). Use 4 reasonable bins to group school spending. Include in the table each of the following:**
* Average Math Score
* Average Reading Score
* % Passing Math
* % Passing Reading
* Overall Passing Rate (Average of the above two)


```python
spending_bins = [0, 585, 615, 645, 675]
group_names = ["<$585", "$585-615", "$615-645", "$645-675"]
school_summary_df['Student Budget Range'] = pd.cut(school_summary_df['Per Student Budget'],bins=spending_bins,labels=group_names)
school_spending = school_summary_df.groupby('Student Budget Range').mean()[['Avg. Math Score','Avg. Reading Score','% Passing Math','% Passing Reading','Overall Passing Rate']]

school_spending['Avg. Math Score'] = school_spending['Avg. Math Score'].map(" {:,.1f}".format)
school_spending['Avg. Reading Score'] = school_spending['Avg. Reading Score'].map(" {:,.1f}".format)
school_spending['% Passing Math'] = school_spending['% Passing Math'].map(" {:,.1f}%".format)
school_spending['% Passing Reading'] = school_spending['% Passing Reading'].map(" {:,.1f}%".format)
school_spending['Overall Passing Rate'] = school_spending['Overall Passing Rate'].map(" {:,.1f}%".format)


school_spending
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Avg. Math Score</th>
      <th>Avg. Reading Score</th>
      <th>% Passing Math</th>
      <th>% Passing Reading</th>
      <th>Overall Passing Rate</th>
    </tr>
    <tr>
      <th>Student Budget Range</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>&lt;$585</th>
      <td>83.5</td>
      <td>83.9</td>
      <td>90.4%</td>
      <td>93.3%</td>
      <td>91.8%</td>
    </tr>
    <tr>
      <th>$585-615</th>
      <td>83.6</td>
      <td>83.9</td>
      <td>90.8%</td>
      <td>92.4%</td>
      <td>91.6%</td>
    </tr>
    <tr>
      <th>$615-645</th>
      <td>79.1</td>
      <td>81.9</td>
      <td>73.0%</td>
      <td>83.2%</td>
      <td>78.1%</td>
    </tr>
    <tr>
      <th>$645-675</th>
      <td>77.0</td>
      <td>81.0</td>
      <td>64.0%</td>
      <td>78.4%</td>
      <td>71.2%</td>
    </tr>
  </tbody>
</table>
</div>



### Scores by School Size

**Repeated the above breakdown, but this time group schools based on a reasonable approximation of school size (Small, Medium, Large).**


```python
size_bins = [0, 1000, 2000, 5000]
group_names = ["Small (<1000)", "Medium (1000-2000)", "Large (2000-5000)"]

school_summary_df['Size Range'] = pd.cut(school_summary_df['Total Students'],bins=size_bins,labels=group_names)
school_sizing = school_summary_df.groupby('Size Range').mean()[['Avg. Math Score','Avg. Reading Score','% Passing Math','% Passing Reading','Overall Passing Rate']]

school_sizing['Avg. Math Score'] = school_sizing['Avg. Math Score'].map(" {:,.1f}".format)
school_sizing['Avg. Reading Score'] = school_sizing['Avg. Reading Score'].map(" {:,.1f}".format)
school_sizing['% Passing Math'] = school_sizing['% Passing Math'].map(" {:,.1f}%".format)
school_sizing['% Passing Reading'] = school_sizing['% Passing Reading'].map(" {:,.1f}%".format)
school_sizing['Overall Passing Rate'] = school_sizing['Overall Passing Rate'].map(" {:,.1f}%".format)


school_sizing
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Avg. Math Score</th>
      <th>Avg. Reading Score</th>
      <th>% Passing Math</th>
      <th>% Passing Reading</th>
      <th>Overall Passing Rate</th>
    </tr>
    <tr>
      <th>Size Range</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Small (&lt;1000)</th>
      <td>83.8</td>
      <td>83.9</td>
      <td>91.2%</td>
      <td>92.5%</td>
      <td>91.8%</td>
    </tr>
    <tr>
      <th>Medium (1000-2000)</th>
      <td>83.4</td>
      <td>83.9</td>
      <td>89.9%</td>
      <td>93.2%</td>
      <td>91.6%</td>
    </tr>
    <tr>
      <th>Large (2000-5000)</th>
      <td>77.7</td>
      <td>81.3</td>
      <td>67.6%</td>
      <td>80.2%</td>
      <td>73.9%</td>
    </tr>
  </tbody>
</table>
</div>



### Scores by School Type

**Repeating the above breakdown, but this time group schools based on school type (Charter vs. District).**


```python
avg_math = district_df.groupby('type').mean()['math_score']
avg_reading = district_df.groupby('type').mean()['reading_score']
percent_passing_math = school_summary_df.groupby(["Type"]).mean()["% Passing Math"]
percent_passing_reading = school_summary_df.groupby(["Type"]).mean()["% Passing Reading"]
overall_passing_rate = (percent_passing_math + percent_passing_reading)/2

school_type_df = pd.DataFrame({
    'Avg. Math Score': avg_math,
    'Avg. Reading Score': avg_reading,
    '% Passing Math' : percent_passing_math,
    '% Passing Reading': percent_passing_reading,
    'Overall Passing Rate': overall_passing_rate
})

school_type_df['Avg. Math Score'] = school_type_df['Avg. Math Score'].map(" {:,.1f}".format)
school_type_df['Avg. Reading Score'] = school_type_df['Avg. Reading Score'].map(" {:,.1f}".format)
school_type_df['% Passing Math'] = school_type_df[ '% Passing Math'].map(" {:,.1f}%".format)
school_type_df['% Passing Reading'] = school_type_df['% Passing Reading'].map(" {:,.1f}%".format)
school_type_df['Overall Passing Rate'] = school_type_df['Overall Passing Rate'].map(" {:,.1f}%".format)

school_type_df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Avg. Math Score</th>
      <th>Avg. Reading Score</th>
      <th>% Passing Math</th>
      <th>% Passing Reading</th>
      <th>Overall Passing Rate</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Charter</th>
      <td>83.4</td>
      <td>83.9</td>
      <td>90.4%</td>
      <td>93.1%</td>
      <td>91.7%</td>
    </tr>
    <tr>
      <th>District</th>
      <td>77.0</td>
      <td>81.0</td>
      <td>64.3%</td>
      <td>78.3%</td>
      <td>71.3%</td>
    </tr>
  </tbody>
</table>
</div>


