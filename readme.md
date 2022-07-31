
# Machine Learning: Customer Segmentation for Product Optimization

Customer Segmentation for Product Optimization is a project based on python which aims to create an AI which predicts the sample’s potential as market. This project aims to help the small medium enterprises of the target partnered community of Mapua University by optimising the data collected in the community and using it as a tool to enhance their products and business. By doing so, businesses can focus on specific products and services that will be successful based on the data produced by our AI.


## Acknowledgements

 - Professor Dionis A. Padilla [ CPE126_C1 Instructor]
 - Professor Cyrel O. Manlises [Project Adviser]


## Installation

Install python on your machine

```bash
  $ pip install python-doc
```

 Install Anaconda 

```bash
  https://www.anaconda.com/products/distribution
```
Install other dependencies

Orange

```bash
  !conda install -y orange3
```
Pandasql

```bash
  pip install pandasql
```

Orange 3

```bash
  pip install Orange3
```

Orange3-Associate

```bash
  pip install Orange3-Associate
```
## Run Locally

Create a working directory

Clone the project

```bash
  git clone https://github.com/garchompers08/CPE126C1_G1_MP.git
```

Run the Python Notebook in Jupyter Notebook


```bash
  Search for Jupyter Notebook, then navigate the file
```


## Deployment

Load your dependencies

```Bash
    Go to the code ``import os...`` then press run on the
    navbar of jupyter notebook
```
Read the excel file
```Bash
    Run cs_df = pd.read_excel(io=r'Online Retail.xlsx')
```
Run 

```Bash
    cs_df.describe()
```

Initialize values by running the 4 cells below

```Bash
    # Remove register withou CustomerID
    cs_df = cs_df[~(cs_df.CustomerID.isnull())]

    # Remove negative or return transactions
    cs_df = cs_df[~(cs_df.Quantity<0)]
    cs_df = cs_df[cs_df.UnitPrice>0]


```

```Bash
    cat_des_df = cs_df.groupby(["StockCode","Description"]).count().reset_index()
    display(cat_des_df.StockCode.value_counts()[cat_des_df.StockCode.value_counts()>1].reset_index().head())
    cs_df[cs_df['StockCode'] == cat_des_df.StockCode.value_counts()[cat_des_df.StockCode.value_counts()>1]
      .reset_index()['index'][4]]['Description'].unique()

```

```Bash
    unique_desc = cs_df[["StockCode", "Description"]].groupby(by=["StockCode"]).\
                apply(pd.DataFrame.mode).reset_index(drop=True)
    q = '''
    select df.InvoiceNo, df.StockCode, un.Description, df.Quantity, df.InvoiceDate,
       df.UnitPrice, df.CustomerID, df.Country
    from cs_df as df INNER JOIN 
     unique_desc as un on df.StockCode = un.StockCode
    '''

    cs_df = pysqldf(q)
```

```Bash
    cs_df.InvoiceDate = pd.to_datetime(cs_df.InvoiceDate)
    cs_df['amount'] = cs_df.Quantity*cs_df.UnitPrice
    cs_df.CustomerID = cs_df.CustomerID.astype('float32')

```


## Exploring the Data

Run the different codes below to see charts with their explanation
## Market Basket Analysis Explanation

Still Waiting
## Screenshots

![App Screenshot](https://via.placeholder.com/468x300?text=App+Screenshot+Here)


## Authors

- [@garchompers08](https://github.com/garchompers08)


## Exploring the Data

Run the different codes below to see charts with their explanation
