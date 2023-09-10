# Low_cost_Data_pipeline
Data pipeline with service on google cloud platform (gcp)

## 1. Introduction
Using existing resources efficiently and cost-effectively is crucial to increase the return on investment in managing your data in today's digital age, where rapid analysis and decision-making are required in all aspects of your business, including the swift development of new, high-quality products and services. With a Low Cost Data Pipeline, you can achieve this more easily.

![enter image description here](https://www.dbs.com.sg/documents/portlet_file_entry/276102/low-cost-business-pd-1404x630.jpg/fb63749e-24b2-8f4e-a807-4aa7c96cb753)


## 2.Objective
**Create a Data Pipeline for analyst and forcast**   In  order to send cryptocurrency price data to a data warehouse and analyze it from a business perspective, while keeping costs to a minimum.

 ![image](https://github.com/mphothanachai/Project_Data_pipeline/assets/137395742/6c9cec96-68af-4346-95c7-aad194a3312a)

## 3.Design

Let design **pipeline**
![image](https://github.com/mphothanachai/Project_Data_pipeline/assets/137395742/b9f6c415-1e8c-4741-a838-930757eb6a08)

## 4. Prepare (before use service on gcp)

1.  Account  [Google cloud platfrom](https://console.cloud.google.com/)  (gcp) if you have it you can use service on gcp (Cloud Functions , Cloud Scheduler , Pub/Sub , BigQuery).
2.  Cloud Functions (you can run code on cloud Python , Node.js , Go , Java).
3.  Cloud Scheduler (For scheduling commands (jobs) that are similar to cron jobs.).
4.  Google Cloud Pub/Sub (Used to send data to run a function at the scheduled cron time.).
5. BigQuery (Use for store data)
6. Looker studio (Dashboard)

## 5. BigQuery
1. First of all create dataset.
![image](https://github.com/mphothanachai/Low_cost_Data_pipeline/assets/137395742/9a6cc8d3-f4db-4c57-ad82-dfc90275601f)
2. Second one create table.
![image](https://github.com/mphothanachai/Low_cost_Data_pipeline/assets/137395742/6ff43035-4718-4e55-b867-8ae79debcfd3)

And then setup schema for support data
![image](https://github.com/mphothanachai/Low_cost_Data_pipeline/assets/137395742/e9381b50-767a-4b04-9a86-7b1fc4552050)
I Will create 3 table (Btc, Eth, Doge).

## 6. Cloud Functions
1. Create function => Trigger (Pub/Sub) => environment variables (keep credential)
![image](https://github.com/mphothanachai/Low_cost_Data_pipeline/assets/137395742/7722e602-44eb-4211-82c3-394903fa662c)

2. Add Trigger => Create topic
![image](https://github.com/mphothanachai/Low_cost_Data_pipeline/assets/137395742/337db957-0a7a-4655-95e6-3059309d649e)
3. Add environment variable for save all credentials
![image](https://github.com/mphothanachai/Low_cost_Data_pipeline/assets/137395742/93370739-98ed-4165-8ecd-7b6accad7705)
4. choose python => main.py (put your code) => requirements.txt (package) => entry point (main function)
![image](https://github.com/mphothanachai/Low_cost_Data_pipeline/assets/137395742/e119cda6-2dfe-4ca5-b18f-8b26b8b6f137)
5. I choose to explain the code briefly because it's quite similar. It starts by creating a class to fetch values from environment variables. The first function, `get_data_btc`, retrieves data from `btc_url` using the `requests` library and converts it to JSON. The next function, `btc_insert_data`, takes the retrieved data and inserts it into BigQuery, referencing the `btc_dataset_id` and the record.
```
import base64
import datetime
import os
import requests
from google.cloud import bigquery

  
class Config:
	dataset_id = os.environ.get("dataset_id")
	table_name = os.environ.get("table_name")
	btc_url = os.environ.get("btc_url")
	eth_url = os.environ.get("eth_url")
	doge_url = os.environ.get("doge_url")

def get_data_btc(url: str) -> dict:
response = requests.get(btc_url)
return response.json()

def btc_insert_data(event, context):
	client = bigquery.Client()
	dataset_ref = client.dataset(Config.btc_dataset_id)

	raw = get_data(Config.btc_url)
	record = [(
		raw["time"]["updatedISO"],
		raw["bpi"]["THB"]["rate_float"],
		raw["bpi"]["USD"]["rate_float"]
		)]
	table_ref = dataset_ref.table(Config.btc_table_name)
	table = client.get_table(table_ref)
	result = client.insert_rows(table, record)
	return result
```
## 7. Cloud Scheduler
Create cron job => target (pub/sub) => topic
![image](https://github.com/mphothanachai/Low_cost_Data_pipeline/assets/137395742/58431a1a-7f80-404c-9717-93b02aed3127)
