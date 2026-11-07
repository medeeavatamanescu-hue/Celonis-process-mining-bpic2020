# Celonis-process-mining-bpic2020
# Building a Process Mining Model in Celonis

Step-by-step guide to build a process model in Celonis from a public event log ("Request For Payment").
University project, course "Artificial Intelligence and Business Intelligence".

## What you need
- A free Celonis account
- An event log with three key columns: **Case ID**, **Activity**, **Timestamp**

## Step 0. Get and prepare the data
1. Download the "Request For Payment" event log (BPI Challenge 2020) from Kaggle.
2. The file is in XES format. Celonis can read it, but we converted it to CSV to check the columns easily.
3. Check the columns: Case ID, Activity, Timestamp, Resource, Role, Project, OrgUnit, RequestedAmount.

## Step 1. Create a Data Pool
1. In Celonis, open **Data** (Data Integration).
2. Go to **Data Pools** and click **Create data pool**.
3. Name it `BPIC2020`.

A Data Pool is a workspace where the data is stored and organised.

## Step 2. Import the file
1. Open the Data Pool.
2. Go to **Data Connections**, then **Add data connection**.
3. Choose **Upload files**.
4. Upload the CSV file and check the preview: the columns must be correctly separated.
5. Set the **Timestamp** column as a date (Datetime). Without this, Celonis cannot calculate durations.
6. Start the import and wait for the confirmation.

## Step 3. Create the Data Model
1. In the Data Pool, go to **Data Models** and click **Create data model**.
2. Name it and add the imported table.
3. Define it as the **Activity table**.
4. Map the three key columns:
   - **Case ID**: the request (one case = one request)
   - **Activity**: the step
   - **Timestamp**: the date and time
5. Validate, then click **Load data model** and wait until the loading is finished.

## Step 4. Create an Analysis in Studio
1. Open **Studio**.
2. Create a **Space** if asked.
3. Create a new **Analysis** and link it to the loaded Data Model.

## Step 5. Add the Process Explorer
1. In the Analysis, open a new sheet.
2. Add the **Process Explorer** component.
3. The process map appears automatically: nothing is drawn by hand.

## Step 6. Explore the map
- **Activities slider**: controls how many steps (boxes) are shown. A low value shows the main path. A higher value shows rarer steps such as rejections, extra validations and drafts.
- **Connections slider**: controls how many paths (arrows) are shown. A higher value shows rarer paths such as loops and skipped steps.

## Step 7. Show the time between steps
1. In the Process Explorer, open the view menu and choose **Throughput time**.
2. Select **Median**.
3. Go back to the simple view (few activities) and read the time between steps.

## Results
- The main path is simple, but the real process contains rejection loops and rework.
- On the main path, the longest wait is at the end, between the payment request and the payment.

## Limits
Public dataset and free Celonis access. This does not show how Celonis performs inside a real company.
