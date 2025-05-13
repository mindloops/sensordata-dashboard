# Sensordata Dashboard

## Prerequisites

- Docker installed (or similar e.g. Rancher, Colima, Podman)
- Internet access

## Run

Execute: `docker compose up`
Now open http://localhost:3000

To terminate, execute: `docker compose down -v`

## Hosted version

See https://sensordata-dashboard.mindloops.io 

## Development Guide

### Preparing for Changes
1. Ensure the application is running locally and accessible at http://localhost:3000.
2. Open the application in your browser and sign in using the admin account (admin / admin) via the "Sign In" button in the top-right corner.
3. You may skip changing the password — it will automatically revert to the default (admin / admin) upon dashboard restart.

### Examples of changes
1. [Dashboard changes](#grafana-dashboard)
2. [Datasource configuration changes](#grafana-datasource-configuration)
3. [Datasource query changes](#grafana-panel-with-infinity-datasource-query)

### Finalizing Your Changes
1. Verify that your changes are persisted by stopping the application with `docker compose down -v`, 
then restarting it using `docker compose up`. Once the application is running, check whether your changes are still present.
2. Commit/Push the changed files to your repository.

### Grafana Dashboard
1. Make your changes to one of the dashboards — for example, add a description to "Details sensordata" by opening the dashboard, 
clicking Edit, and entering text in the Description field.
2. To save your changes, click the Save dashboard button in the top-right corner.
3. Then click Copy JSON to clipboard, and replace the contents of the corresponding dashboard file under /dashboards.
For this example, update the file: [dashboard-details.json](./dashboards/dashboard-details.json).
4. Use version control to verify that the changes compared to the previous version are as expected.

### Grafana Datasource Configuration
1. Navigate to the **Connections** section in Grafana.
2. Open the **Data sources** page.
3. Select the datasource you want to modify — for example, the **RIVM Samen Meten API**.
4. Update the desired configuration property. For instance, at **URL, Headers & Params**, enable **Allow dangerous HTTP methods**.
5. To proceed, click on the **Main** section.
6. Then select **Provisioning Script** to view the YAML representation of the datasource configuration.
7. Copy the relevant updated property and paste it into the corresponding datasource entry in the file [datasource.yaml](./datasource.yaml).

### Grafana Panel with Infinity Datasource Query
1. Navigate to the panel you want to edit — for example, the first panel in **Details sensordata**.
2. Click the three vertical dots in the top-right corner of the panel, then select **Edit**.
3. On the **Edit panel** page, you’ll find many configuration options. In our experience, most of these are well-documented. 
Additionally, AI tools like ChatGPT, Claude.. can often provide helpful explanations and guidance.
4. In the **Queries** section, configure the URL query to be executed. For example:  
   `/Datastreams(${datastreams:text})/Observations`  
   This path will be prefixed by the `url` property of the datasource defined in [**datasource.yaml**](./datasource.yaml).
5. In the **Headers, Request params** section, you can provide additional options for the API call — such as sorting the entries in the response.
6. In the **Parsing options & Result fields** section, you can map the JSON response to fields used in the graph. For example: `value.phenomenonTime`.
7. To save your changes, click the **Save dashboard** button in the top-right corner.
8. Then click **Copy JSON to clipboard**, and overwrite the contents of the corresponding dashboard file under `/dashboards`.  
   For this example, update the file: [**dashboard-details.json**](./dashboards/dashboard-details.json).
9. Use version control to verify that the changes compared to the previous version are as expected.