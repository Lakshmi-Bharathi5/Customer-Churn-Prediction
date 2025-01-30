What is Churn?
Churn refers to the rate at which customers stop doing business with a company or service, typically expressed as a percentage of the customer base.

What is a Churn Rate?
Churn Rate, sometimes known as attrition rate, is the rate at which customers stop doing business with a company over a given period. Churn may also apply to the number of subscribers who cancel or don’t renew a subscription. The higher your churn rate, the more customers stop buying from your business. The lower your churn rate, the more customers you retain. Typically, the lower your churn rate, the better.
Churn Rate = (Churned Customers / Total Number of Customers) x 100%

What is Customer Churn?
Customer Churn refers to the natural business cycle of losing and acquiring customers. Every company — no matter the quality of its products or customer service experiences churn. In the context of businesses, customer churn can occur due to factors such as dissatisfaction with the product or service, competitive offerings, or changes in circumstances or preferences of the customer. Generally speaking, the less churn a company has, the more customers they keep.

About the Data
The dataset is a Microsoft Excel file that contains one table, consisting of 7,043 rows and 23 columns of PhoneNow Telecoms customer information, which includes, customer Demographics, Account Information, and Service Subscriptions.

Data Preparation
The data transformation was finished using Power Query, and now the dataset is loaded into Microsoft Power BI Desktop for modeling purposes.

The Customer Churn dataset is given table named:
ChurnDataset which has 7043 rows and 23 columns of observation.
Data Cleaning for the dataset was done in the Power Query Editor as follows:
Changed the Data type of customerID, gender, SeniorCitizen as given below:
= Table.TransformColumnTypes(#"Promoted Headers",{{"customerID", type text}, {"gender", type text}, {"SeniorCitizen", Int64.Type},

Replaced Value names of Mailed check, Electronic check, Bank transfer (automatic), Credit card (automatic) in the columns as given below:
1. = Table.ReplaceValue(#"Changed Type","Mailed check","Mailed Check",Replacer.ReplaceText,{"PaymentMethod"})
2. = Table.ReplaceValue(#"Replaced Value","Electronic check","Electronic Check",Replacer.ReplaceText,{"PaymentMethod"})
3. = Table.ReplaceValue(#"Replaced Value1","Bank transfer (automatic)","Bank Transfer",Replacer.ReplaceText,{"PaymentMethod"})
4. = Table.ReplaceValue(#"Replaced Value2","Credit card (automatic)","Credit Card",Replacer.ReplaceText,{"PaymentMethod"})
Replaced Column Names of customerID, gender, tenure as given below:
= Table.RenameColumns(#"Replaced Value3",{{"customerID", "CustomerID"}, {"gender", "Gender"}, {"tenure", "Tenure"}})
In the new table, two additional conditional columns were added using M-formula:
1. = CitizenshipStatus = IF('ChurnDataset'[SeniorCitizen] = 0, "Young Citizen", "Senior Citizen")
2. = ChurnStatus = IF('ChurnDataset'[Churn] = "Yes", "Churned", "Retained")

Measures used in all visualization are:
Total Customers = COUNT(ChurnDataset[CustomerID])
Churned Customers = CALCULATE(COUNTA('ChurnDataset'[CustomerID]), 'ChurnDataset'[Churn] IN { "Yes" })
Retained Customers = CALCULATE(COUNTA('ChurnDataset'[CustomerID]), 'ChurnDataset'[Churn] IN { "No" })
Percent of Churned Customer = (ChurnDataset[Churned Customers] / [Total Customers])
Percent of Retained Customers = ([Retained Customers] / [Total Customers])
Churn Rate % = ChurnDataset[Churned Customers] / COUNT(ChurnDataset[CustomerID])
ChurnStatus = IF('ChurnDataset'[Churn] = "Yes", "Churned", "Retained")
Monthly Revenue Loss = CALCULATE(SUM(ChurnDataset[MonthlyCharges]), ChurnDataset[Churn] = "Yes")
Revenue Loss % = DIVIDE([Monthly Revenue Loss], SUM('ChurnDataset'[MonthlyCharges]), 0)
CitizenshipStatus = IF('ChurnDataset'[SeniorCitizen] = 0, "Young Citizen", "Senior Citizen")
PaymentMode = IF(OR('ChurnDataset'[PaymentMethod] = "Electronic Check", 'ChurnDataset'[PaymentMethod] = "Mailed Check"), "Manual", "Automatic")
