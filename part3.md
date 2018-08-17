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

Note that the IP adress of your LinuxONE cloud Linux VM is different, you must adapt the following accordingly. You can access to the Kibana landing page using the following URL: http://your_ip_adress:5601

A reachable kibana web interface should look like as follow:
![alt text](https://github.com/guikarai/ELK-CPACF/blob/master/images/kibana-landingpage.png)

Now, let's see how Kibana can connect to a source of data (in our case the Elasticsearch DB).

# Sourcing the ElasticSearch DataSource

It is time to create an Index Pattern to Connect to Elasticsearh. To use Kibana, you have to tell it about the Elasticsearch indices that you want to explore by configuring one or more index patterns. 

**Action:** Click on the left tab bar to **"Management"**.

![alt text](https://github.com/guikarai/ELK-CPACF/blob/master/images/kibana-index-creation0.png)

**Action:** Then Click on **Index patterns**.

## Creating your first "Index"

An index pattern identifies one or more Elasticsearch indices that you want to explore with Kibana. Kibana looks for index names that match the specified pattern. An asterisk (*) in the pattern matches zero or more characters. For example, the pattern myindex-* matches all indices whose names start with myindex-, such as myindex-1 and myindex-2.

An index pattern can also simply be the name of a single index.

**Action:** Click on Index pattern area, and fill the tab with **monitor-vmstat*** as follow. 

![alt text](https://github.com/guikarai/ELK-CPACF/blob/master/images/kibana-index-creation1.png)

**Action:** Then click to **Next Step**.
  
Your index contains a timestamp field that you want to use to perform time-based comparisons, select the Index contains time-based events option and select the index field that contains the timestamp. Kibana reads the index mapping to list all of the fields that contain a timestamp.

**Action:** In configure settings panel, please select **@Timestamp**.

![alt text](https://github.com/guikarai/ELK-CPACF/blob/master/images/kibana-index-creation2.png)

**Action:**  Then validate by clicking on **Create index pattern**.

Here you are, you just sourced Kibana to your crypto monitoring Elasticsearch DB and its content. The structure of the index monitor-vmstat is displayed front of you.

![alt text](https://github.com/guikarai/ELK-CPACF/blob/master/images/kibana-index-creation4.png)

## Creating a second index about Linux crypto data

You just create your first index about vmstat. Not, please create a new index about Linux encryption activity the with the following information:

* **Action:** Click on the left tab bar to **"Management"**.
* **Action:** Then Click on **Index patterns**.
* **Action:** Click on Index pattern area, and fill the tab with **monitor-icastats***.
* **Action:** Then click to **Next Step**.
* **Action:** In configure settings panel, please select **@Timestamp**.
* **Action:**  Then validate by clicking on **Create index pattern**.

Cool, you have now two created indexes. One named monitor-vmstat and one named monitor-icastats.

It is now time to discovert, search, and filter sent information to the Elasticsearch DB thanks to a "Search".

**Action:** Click on the left tab bar on **"Discover"**. 

# Creating your first "Searchs"

## Creating a search about Linux VMSTAT data

You can interactively explore your data from the Discover page. You have access to every document in every index that matches the selected index pattern. You can submit search queries, filter the search results, and view document data. You can also see the number of documents that match the search query and get field value statistics. If a time field is configured for the selected index pattern, the distribution of documents over time is displayed in a histogram at the top of the page.

![alt text](https://github.com/guikarai/ELK-CPACF/blob/master/images/kibana-search-creation0.png)

Let's start to discover and to explore VMSTAT data sent by LinuxONE virtual machine. When you submit a search request, the histogram, Documents table, and Fields list are updated to reflect the search results. The total number of hits (matching documents) is shown in the toolbar. The Documents table shows the first five hundred hits. 

By default, the hits are listed in reverse chronological order, with the newest documents shown first. You can reverse the sort order by clicking the Time column header. You can also sort the table by the values in any indexed field.

**Action:** On Available field MODE, on the line of "Host", Click on "add" field MODE. It result the following:

![alt text](https://github.com/guikarai/ELK-CPACF/blob/master/images/kibana-search-creation1.png)

Now we are good. Let's save this search with a name we can refer later. Saving searches enables you to reload them into Discover and use them as the basis for visualizations. Saving a search saves both the search query string and the currently selected index pattern.

**Action:** Now on the top right bar, click on **Save**, and name your save **vmstat-host** as follow:

![alt text](https://github.com/guikarai/ELK-CPACF/blob/master/images/kibana-search-creation2.png)

If successful, you must see the following message on top of the Kibana interface:

![alt text](https://github.com/guikarai/ELK-CPACF/blob/master/images/kibana-search-creation3.png)

## Creating a second search about Linux crypto data

You just create your first index about vmstat. Not, please create a new index about Linux encryption activity the with the following information:

* **Action:** Click on the left tab bar on **"Discover"**. 

* **Action:** Select the index **monitor-icastats** as follow:

![alt text](https://github.com/guikarai/ELK-CPACF/blob/master/images/kibana-search-creation5.png)

The name of the index **monitor-icastats** should be visible as follow:

![alt text](https://github.com/guikarai/ELK-CPACF/blob/master/images/kibana-search-creation4.png)

* **Action:** On **Available field MODE**, on the line of **Host**, Click on **add** field MODE.

* **Action:** Now on the top right bar, click on **Save**, and name your save **icastats-host**.

# Creating your first visualizations

## Creating your first visualization charts for VMSTAT data
A Kibana dashboard displays a collection of visualizations and searches. You can arrange, resize, and edit the dashboard content and then save the dashboard so you can share it.

**Action:** Click on **Visualize** in the side navigation.

**Action:** Click the Create new visualization button or the + button:

![alt text](https://github.com/guikarai/ELK-CPACF/blob/master/images/kibana-visualize-creation0.png)

** Action:** Choose the visualization type: Visual Builder
![alt text](https://github.com/guikarai/ELK-CPACF/blob/master/images/kibana-visualize-creation1.png)

To build a visualization from a saved search, click the name of the saved search you previously saved (icastats). This opens the visualization builder and loads the selected query. When you build a visualization from a saved search, any subsequent modifications to the saved search are automatically reflected in the visualization. To disable automatic updates, you can disconnect a visualization from the saved search.

** Action:** Specify a search query to retrieve the data for your visualization.
![alt text](https://github.com/guikarai/ELK-CPACF/blob/master/images/kibana-visualize-creation2.png)

![alt text](https://github.com/guikarai/ELK-CPACF/blob/master/images/kibana-visualize-creation3.png)

![alt text](https://github.com/guikarai/ELK-CPACF/blob/master/images/kibana-visualize-creation4.png)

![alt text](https://github.com/guikarai/ELK-CPACF/blob/master/images/kibana-visualize-creation5.png)

![alt text](https://github.com/guikarai/ELK-CPACF/blob/master/images/kibana-visualize-creation6.png)

You should be able to visualize incoming crypto metrics with a nice visual live updated.

**Action:** Now on the top right bar, click on Save.

## Creating your first dashboard


![alt text](https://github.com/guikarai/ELK-CPACF/blob/master/images/kibana-dashboard-creation1.png)

![alt text](https://github.com/guikarai/ELK-CPACF/blob/master/images/kibana-dashboard-creation2.png)

![alt text](https://github.com/guikarai/ELK-CPACF/blob/master/images/kibana-dashboard-creation3.png)

![alt text](https://github.com/guikarai/ELK-CPACF/blob/master/images/kibana-dashboard-creation4.png)

