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
