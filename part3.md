# Welcome in the Step 4 about building a crypto dashboard with Kibana.

In this part, you will use the ELK microservices to create your first crypto dashboard with Kibana.

The agenda of this section is about:
1. Accessing to Kibana
2. Sourcing the ElasticSearch DataSource
3. Creating your first search with Kibana
4. Creating your first charts with Kibana
5. Creating your first dashboard with Kibana
6. Sharing your first crypto dashboard
In this part, you will create your first crypto dashboard with Kibana. 

Kibana is a window into the Elastic Stack. It enables visual exploration and real-time analysis of your data in Elasticsearch. This video is perfect for users that are new to Kibana and are looking for a primer on data exploration, visualization, and dashboarding. Watch Alex Francoeur give a demo of going from a Kibana installation to a full dashboard in matter of minutes. 

# Accessing to Kibana

Note that your IP adress is different, you must adapt the following accordingly. You can access to the Kibana landing page using the following URL: http://10.3.57.112:5601

A reachable kibana web interface should look like as follow:
![alt text](https://github.com/guikarai/ELK-CPACF/blob/master/images/kibana-landingpage.png)

That is a good start. You can connect to Kibana. Now, let's see how Kibana can connect to a source of data (in our case the Elasticsearch DB).

# Sourcing the ElasticSearch DataSource

It is time to create an Index Pattern to Connect to Elasticsearh. To use Kibana, you have to tell it about the Elasticsearch indices that you want to explore by configuring one or more index patterns. 

**Action:** Click on the left tab bar to **"Management"**.

**Action:** Then Click on **Index pattern**.

![alt text](https://github.com/guikarai/ELK-CPACF/blob/master/images/kibana-index-creation0.png)


## Creating your first index

### A. Define an index pattern named "monitor*"

An index pattern identifies one or more Elasticsearch indices that you want to explore with Kibana. Kibana looks for index names that match the specified pattern. An asterisk (*) in the pattern matches zero or more characters. For example, the pattern myindex-* matches all indices whose names start with myindex-, such as myindex-1 and myindex-2.

An index pattern can also simply be the name of a single index.

![alt text](https://github.com/guikarai/ELK-CPACF/blob/master/images/kibana-index-creation1.png)

**Action:** Click on Index pattern area, and fill the tab with **monitor-vmstat*** as follow. 

**Action:** Then click to **Next Step**.
  
### B. Save your defined an index pattern

Your index contains a timestamp field that you want to use to perform time-based comparisons, select the Index contains time-based events option and select the index field that contains the timestamp. Kibana reads the index mapping to list all of the fields that contain a timestamp.

**Action:** In configure settings panel, please select **@Timestamp**.

**Action:**  Then validate by clicking on **Create index pattern**.

![alt text](https://github.com/guikarai/ELK-CPACF/blob/master/images/kibana-index-creation2.png)

### C. Check your new defined pattern

Here you are, you just sourced Kibana to your crypto monitoring Elasticsearch DB and its content. The structure of the index monitor* is displayed front of you.

![alt text](https://github.com/guikarai/ELK-CPACF/blob/master/images/kibana-index-creation4.png)

## Creating a second index index about Linux crypto data

According to previous step, create a new index with the following informaton.
* Index pattern: monitor-icastats
* Add timestamp: @Timestamp

It is now time to capture a set of information from the DB thanks to a search.

**Action:** Click on the left tab bar on **"Discover"**. 

# Creating your first searchs

## Creating a search about Linux VMSTAT data
You can interactively explore your data from the Discover page. You have access to every document in every index that matches the selected index pattern. You can submit search queries, filter the search results, and view document data. You can also see the number of documents that match the search query and get field value statistics. If a time field is configured for the selected index pattern, the distribution of documents over time is displayed in a histogram at the top of the page.

### 1. Click on the left tab bar to "Discover". 
![alt text](https://github.com/guikarai/ELK-CPACF/blob/master/images/kibana-search-creation0.png)

### 2. Let's start to discover and to explore crypto data sent by LinuxONE virtual machine.
When you submit a search request, the histogram, Documents table, and Fields list are updated to reflect the search results. The total number of hits (matching documents) is shown in the toolbar. The Documents table shows the first five hundred hits. 

By default, the hits are listed in reverse chronological order, with the newest documents shown first. You can reverse the sort order by clicking the Time column header. You can also sort the table by the values in any indexed field.

**Action:** On Available field MODE, on the line of "Host", Click on "add" field MODE. It result the following:
![alt text](https://github.com/guikarai/ELK-CPACF/blob/master/images/kibana-search-creation1.png)

Now we are good. Let's save this search with a name we can refer later. Saving searches enables you to reload them into Discover and use them as the basis for visualizations. Saving a search saves both the search query string and the currently selected index pattern.

**Action:** Now on the top right bar, click on Save as follow:
![alt text](https://github.com/guikarai/ELK-CPACF/blob/master/images/kibana-search-creation2.png)

If successful, you must see the following message on top of the Kibana interface:
![alt text](https://github.com/guikarai/ELK-CPACF/blob/master/images/kibana-search-creation3.png)

## Creating a search about Linux crypto ICASTATS data

Same as above with the following informations:

**Pattern-index :** monitor-icastats

**Available-field :** Host

**Save search as :** icastats-host

# Creating your first visualizations

## Creating your first visualization charts for VMSTAT data
A Kibana dashboard displays a collection of visualizations and searches. You can arrange, resize, and edit the dashboard content and then save the dashboard so you can share it.

#### 1. Click on Visualize in the side navigation.
![alt text](https://github.com/guikarai/ELK-CPACF/blob/master/images/Capture%20d%E2%80%99%C3%A9cran%202018-05-24%20%C3%A0%2011.47.40%20(2).png)

#### 2. Click the Create new visualization button or the + button.
![alt text](https://github.com/guikarai/ELK-CPACF/blob/master/images/Capture%20d%E2%80%99%C3%A9cran%202018-05-24%20%C3%A0%2011.47.40%20(2).png)

#### 3. Choose the visualization type: Vertical Bar
![alt text](https://github.com/guikarai/ELK-CPACF/blob/master/images/Capture%20d%E2%80%99%C3%A9cran%202018-05-24%20%C3%A0%2011.48.41%20(2).png)

#### 4. Specify a search query to retrieve the data for your visualization.
To build a visualization from a saved search, click the name of the saved search you previously saved (icastats). This opens the visualization builder and loads the selected query. When you build a visualization from a saved search, any subsequent modifications to the saved search are automatically reflected in the visualization. To disable automatic updates, you can disconnect a visualization from the saved search.
![alt text](https://github.com/guikarai/ELK-CPACF/blob/master/images/Capture%20d%E2%80%99%C3%A9cran%202018-05-24%20%C3%A0%2011.48.53%20(2).png)

#### 5. Vizualization builder
In the visualization builder, choose the metric aggregation for the visualization’s Y axis: Average
In the visualization builder, choose the metric field for the visualization’s Y axis: AES CBC
For the visualizations X axis, select a bucket aggregation: Date Histogram
For the visualizations X axis, select a bucket field: @Timestamp
For the visualizations X axis, select a bucket interval: Auto

Now click on play button as follow:
![alt text](https://github.com/guikarai/ELK-CPACF/blob/master/images/Capture%20d%E2%80%99%C3%A9cran%202018-05-24%20%C3%A0%2011.49.17%20(2).png)

You should be able to visualize incoming crypto metrics with a bar chart.

#### 6. Now on the top right bar, click on Save.

#### 7. Save as "AES" your first vizualization chart.
![alt text](https://github.com/guikarai/ELK-CPACF/blob/master/images/Capture%20d%E2%80%99%C3%A9cran%202018-05-24%20%C3%A0%2011.47.40%20(2).png)

Repeat the creation of visualization with DES, TDES, SHA-1 and DRBG-SHA-512. Your visualization collection should look like the following:
Capture d’écran 2018-05-24 à 11.51.53 (2)

## Creating your first dashboard

Capture d’écran 2018-05-24 à 11.52.10 (2)

Capture d’écran 2018-05-24 à 11.52.15 (2)

Capture d’écran 2018-05-24 à 11.52.32 (2)

Capture d’écran 2018-05-24 à 11.52.55 (2)
