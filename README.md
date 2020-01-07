## Which not-for-profits are at the highest risk for fraud?

"One area in which nonprofit organizations seem particularly vulnerable is billing schemes, in which an employee fraudulently submits invoices to obtain payments he or she is not entitled to receive. According to the most recent ACFE survey, billing schemes were among the most common fraud methods in the cases studied for the 2012 report.

Billing schemes often involve the creation of a shell company. In such a fraud, a dishonest employee sets up a fake identity that bills for good or services the organization does not receive. In some instances, goods or services may be delivered but are marked up excessively, with the proceeds diverted to the employee."

https://nonprofitrisk.org/resources/articles/a-violation-of-trust-fraud-risk-in-nonprofit-organizations/

### Data source:

The data for this project was aquired from Open990(https://www.open990.org/catalog/), an organization that aggregates and provides not-for-profit tax return data made public by the IRS.  This dataset has great documentation about what the attributes mean, however this only includes data for 1 year(2016).  The organization that provides this data also provides analytics services with this data for a fee. (https://appliednonprofitresearch.com/customdata/)

Overview of data provided by open990
(https://medium.com/@open990/the-irs-990-e-file-dataset-getting-to-the-chocolatey-center-of-data-deliciousness-90f66097a600)

### Target Feature Creation:

1. Employees and Volunteers as a percentage of over 100K contractors
    - Employees and volunteers count / count of contractors over 100K
    - fewer employees can translate to weaker controls over vetting and payment of contractors

1. Share of contractor expense as a percentage of total expenses
    - (average contractor payment * count of contractors over $100K) / total expenses
    - this will help identify organizations that spend a high percentage of their funds on contractors
    
### ML Classification Goal:
Can I predict not-for-profits that lie within the top quartile for the above two synthetic features, and therefore might be at a higher risk for contractor fraud?

### Results:
Gradient Boost Classifier was the most successful model.  Using a combination of 38 features, this model was able to classify not-for-profits at a higher risk for fraud:
 - 8.54% Type II error rate (the rate at which the model incorrectly categorized an organization as negative, when it should have been categorized as positive) 
 - 1.3% Type I error rate (the rate at which the model incorrectly categorized an organization as positive, when it should have been categorized as negative)
 
 ### Contractor Count & Employee Count Visualization with Type I & Type II Errors
 ____
 ![](https://github.com/mrkjhsn/Supervised_Learning_990_Contractors/blob/master/visualizations/test_set_cont_count_emp_count.png)
 ![](https://github.com/mrkjhsn/Supervised_Learning_990_Contractors/blob/master/visualizations/cont_count_emp_count_target_feature.png)
 ![](https://github.com/mrkjhsn/Supervised_Learning_990_Contractors/blob/master/visualizations/cont_count_emp_count_type_I_type_II.png)
  
  ### Contractor Count & Expenses Visualization with Type I & Type II Errors
  ____
 ![](https://github.com/mrkjhsn/Supervised_Learning_990_Contractors/blob/master/visualizations/test_set_cont_count_expenses.png)
 ![](https://github.com/mrkjhsn/Supervised_Learning_990_Contractors/blob/master/visualizations/cont_count_expenses_target_feature.png)
 ![](https://github.com/mrkjhsn/Supervised_Learning_990_Contractors/blob/master/visualizations/cont_count_expenses_type_I_type_II.png)
   
