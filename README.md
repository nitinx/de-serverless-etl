# Data Engineering
## Project: Serverless ETL

## Project Overview
India's National Stock Exchange (NSE) historical data spanning close to 20 years has been sourced in CSV format. Historical data is grouped/divided by stocks and there are in excess of 1300 stocks. Going forward, data would be sourced monthly. To support analytics, data is to be transformed into columnar Parquet format. 

Processing of historical data is not in scope of this project. Going forward, incremental source data would be made available on S3; this needs to be transformed into Parquet and loaded back into S3.

### Architecture

- Representation	
![Representation](https://github.com/nitinx/de-serverless-etl/blob/master/architecture.png)

- <To Do>
	- <To Do>
	- <To Do>


### Pre-requisites

An Amazon Web Services [AWS] account with access to following services: 

- [AWS DataSync](https://aws.amazon.com/datasync/)
- [AWS Lambda](https://aws.amazon.com/lambda/)
- [AWS Glue](https://aws.amazon.com/glue/)
- [AWS SES](https://aws.amazon.com/ses/)
- [AWS CloudWatch](https://aws.amazon.com/cloudwatch/)
- [AWS IAM](https://aws.amazon.com/iam/)
- [Amazon S3](https://aws.amazon.com/s3/)
- [Amazon Athena](https://aws.amazon.com/athena/)

Additionally, code base would be on **Python 3.7**.

### Code

This project contains three Python files:

- `lambda-trigger-glue-job.py`: Lambda function to trigger Glue Job and send out out notifications.
- `lambda-trigger-glue-job.py`: Lambda function to trigger Glue Crawler and send out out notifications.
- `gllue-etl.py`: Glue ETL to transform CSV into partitioned Parquets.

### Setup

- <To Do>


### Data
Source data is in CSV format and is in the form of multiple files - each stock file has records for a single stock from 2000 onwards. There are 1386 files in all. Additionally, there is one static file mapping the stock symbol to the company.

Dataset has been obtained from Kaggle (https://www.kaggle.com/abhishekyana/nse-listed-1384-companies-data).

Dataset contains two categories of data:

1. **Stock Data**: 1386 files in CSV format which contains stock prices for 1364 NSE stocks from 2000 onwards. One record/stock for each trading day. In all, there are 3,758,123 records. Columns include Date, Open, Close, High, Low and Volume.
   - `File Count: 1386`

2. **Companies Data**: 1 file in CSV format which maps the Stock Symbol to the Company. Contains 1384 records.
   - `File Count: 1`

### Schema for NSE Stocks
Star Schema made up of one fact and two dimensions would be built. Details:

#### Fact Table
1. **stocks** - stock prices
   - id, symbol, open, high, low, close, adj_close, volume

#### Dimension Tables
2. **date** - date dimension
   - date, year, quarter, month, week, day
3. **companies** - companies to stock mapping
   - id, symbol, company
