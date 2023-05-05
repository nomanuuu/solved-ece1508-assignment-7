Download Link: https://assignmentchef.com/product/solved-ece1508-assignment-7
<br>



Over the past two decades, the emergence of IoT technologies and the pervasive use of small electronic devices in monitoring the urban infrastructure and services have transformed many aspects of modern human societies and set the foundation of “smart framework”. Connected devices generate large volumes of data which require sophisticated data collection and analysis methods to be effectively used. This lab builds upon the use of Open Data APIs and effective open source software components to enable you to collect environmental data and deploy a basic application to perform some data analytics tasks.

Two achieve this, we can use two different approaches. The first one is “<strong>pullbased approach</strong>” in which we use web protocols (HTTP or HTTPS) to connect to public API endpoints and collect data. The second mechanism is to use “<strong>push-based approach</strong>” in which we develop an IoT gateway that notifies applications and users whenever there is an update in the data.

This lab will use the Python programming language for the implementation requirements. The following links may provide related information to help you with your programming challenges. To complete the programming tasks, you only need to set up your computer to use Python.

<ul>

 <li><a href="https://www.tutorialspoint.com/python/">https://www.tutorialspoint.com/python/</a></li>

 <li><a href="https://www.learnpython.org/">https://www.learnpython.org/</a></li>

</ul>







<h1>Part 1: Traffic Flow Analysis (Pull-based Approach)</h1>

For this part of the lab, you will use the following APIs from the Connected Vehicles and Smart Transportation (CVST) IoT application platform to obtain realtime data about the traffic flow in GTA. To check the platform visualization tools and learn more about the current platform APIs, please navigate to <u>portal.cvst.ca</u>.

<ul>

 <li>CVST APIs that we use in this part of the lab:</li>

</ul>

o <strong>Traffic Sensor API:</strong> http://portal.cvst.ca/api/0.1/HW_speed  o <strong>Bixi Bicycle API:</strong> <a href="http://portal.cvst.ca/api/0.1/bixi">http://portal.cvst.ca/api/0.1/bixi</a>

<strong>Note 1:</strong> Any API call or data analytics tasks (including the data visualization) should be performed within your Python application.

<h1>Part 1.1: Flow Speed Analysis</h1>

For this part of the lab, you will use “Traffic Sensor” API to collect real-time traffic flow data for major roads, highways, and streets in GTA. To access to the API data, you need to call the API first. Upon calling, you will receive a JSON document that has four variables. The variables description are as follows:

<ul>

 <li><strong>_id</strong> → This is a platform specific ID which refers to the document ID in our fast Indexing service.</li>

 <li><strong>data[]</strong> → Contains a list of all the GTA traffic sensors and the associated traffic flow measurements. Currently, we are collecting measurements for 5448 sensors. The following shows the set of variables and measurements for a sample traffic sensor in the list.</li>

 <li><strong>date_time</strong> → Provides the date and time under which the measurements have been collected.</li>

 <li><strong>timestamp</strong>: Provides the number of seconds since January 1<sup>st</sup>, 1970 in UTC.</li>

</ul>

<strong>Note 1</strong>: You can use the online JSON viewer available at <a href="https://jsoneditoronline.org/">https://jsoneditoronline.org/</a> to see the JSON document and its structure before you use it in your code or you can install a JSON formatter extension on your browser.

<h1>Tasks to Complete</h1>

<ol>

 <li>You need to write a Python code to collect the Traffic Flow data from “Traffic Sensor” API and extract the following fields from it.

  <ul>

   <li><strong>data[]</strong>: For each sensor object data in the list, extract the items that are indicated by a red rectangle around them as shown in the figure above and eliminate the rest. The fields that need to be kept are “avg_speed_capped”, “free_flow_speed”, “main_road_name”, and “ref_road_name”.</li>

   <li><strong>date_time</strong>: keep this item to stamp your data with the time and date at which they are collected.</li>

  </ul></li>

 <li>You need to combine the “main_road_name” and “ref_road_name” together to create a single unique field to indicate the exact location of the Traffic Sensor. To do so, name the new field as “road_name” and use the following pattern to combine the two fields.</li>

</ol>

<ul>

 <li>road_name = main_road_name + “/” + ref_road_name</li>

</ul>

<strong>Note 2: </strong>The Python code you developed in step 1 and step 2 is called a <strong>Parser</strong>. The main role of the Parser module is to retrieve data from an external source and transform it into your platform specific format.

<ol start="3">

 <li>You need to run your Parser code for a <strong>continuous duration of 24 hours and call the “Traffic Sensor” API every 1 hour</strong>. Each time you call the API, you need to perform steps 1 and 2 as well. Feel free to use any methods you are familiar with to save the data you collected.</li>

</ol>

<strong>Note 3</strong>: Please avoid calling the platform APIs more than the required frequency.

<strong>Important Point</strong>: We only need a subset of the collected data to perform the following analysis. Please choose the first ten Traffic Sensors (roads name) from the collected data and eliminate the rest. Each time you call the API, you receive a JSON document that contains a variable called “data”. The variable is a list that contains data for all the traffic sensors in the GTA. To keep some of the traffic sensors data and eliminate the rest, you need to apply the changes in this part of the JSON document. <strong>For efficiency and better performance achievement of your application</strong>, you can first select the first ten traffic sensors and then proceed with Steps 1 to 3.

<ol start="4">

 <li>After collecting the data in Step 3, you need to perform the following analysis on the data.

  <ul>

   <li>Create a graph and plot the “avg_speed_capped” for all the selected traffic sensors independently from each other as a function of time (24 hours). Use vertical axis for the speed and horizontal axis for the time. Can you find any specific pattern in the data?</li>

  </ul></li>

</ol>

<strong>Note 4</strong>: You can plot all the sensors data in one graph or you can plot them separately.

<strong>In your report</strong>, include the graph(s) and explain your answer.

<ul>

 <li>Divide “avg_speed_capped” by “free_flow_speed” and name it as “ρ”. Create a graph and plot the parameter “ρ” as a function of time (24 hours) for the same roads you used in step 4.1 and answer the following questions?

  <ul>

   <li>Can you explain what does the graph specify?</li>

   <li>Can you find any specific trends in the data?</li>

   <li>Can you explain what does it mean if the value of “ρ” is bigger than one?</li>

   <li>Can you also find an example of this event in your graph?</li>

  </ul></li>

</ul>

<strong>In your report</strong>, include the graph(s) and explain your answers.

<h1>Part 1.2: Bixi Data Analysis</h1>

For this part of the lab, you will use the “Bixi Bicycle” API to collect real-time data about the Bicycles in GTA from the CVST platform. You need to call the API first to retrieve the data. Upon calling the API, the platform will provide you with a JSON document that contains the following data items.

<strong>Important Point</strong>: The above image shows state data for a single Bixi station in the GTA. Each time you call the API, you will get update for all the installed stations.

<strong>Note 5</strong>: It is possible that you will receive data for changing number of stations in each API call. For accuracy of your analysis, <strong>keep the data for the first 30 stations and eliminate the rest</strong> each time you collect data.

<strong>Note 6</strong>: You can use the online JSON viewer available at <a href="https://jsoneditoronline.org/">https://jsoneditoronline.org/</a> to see the JSON document and its structure before you use it in your code or you can install a JSON formatter extension on your browser.

<h1>Tasks to Complete</h1>

<ol>

 <li>You need to write a Parser code by using Python and collect the API data <strong>for a continuous duration of 24 hours with a frequency of one API call per hour</strong>. Each time you receive the JSON digest from the API, you need to keep the data items that are circled in red from the above picture and eliminate the rest. You need to do this for every single station you selected (first thirty). Feel free to use whatever mechanisms you like to keep your data for future steps.</li>

</ol>

<strong>Note 7</strong>: The date_time variable denotes the exact time when the station reported its status to the platform. Stations are not sending their data at the same time and that’s why you may see a time variation of (+- 45mins) between the stations reported time. However, every single station reports its status at least once per hour. Therefore, you can ignore the time variation and assume that each time you call the API, you get new updates.

<ol start="2">

 <li>The sum of the values for “bikes” and “empty_docks” denote the maximum capacity of each station. The “empty_docks” value also shows the number of bikes which are taken from the station. For each station, create a new parameter and name it as “station_capacity”. You need to calculate the value for “station_capacity” according to the formula below.</li>

</ol>

<ul>

 <li>station_capacity = empty_docks + bikes</li>

</ul>

<ol start="3">

 <li>After preparing your data in step 1 and 2, you need to write a Python code that performs the following simple analysis.

  <ul>

   <li>For each time you collect the data (every hour) calculate the total number of Bixi bicycles and the total number of bicycles which are currently in use in the whole GTA.</li>

   <li>Divide the total number of bicycles in use by the total number of bicycles in GTA for every time you receive data (every hour) and name it as</li>

  </ul></li>

</ol>

“bicycle_load”.

<ul>

 <li>Create a graph and plot the “bicycle_load” as a function of time (24 hours). Can you explain what does the graph specify? Can you find any pattern in the data?</li>

</ul>

<strong>In your report</strong>, include the graph and explain your answers.




<h1>Part 2: Create an Event-based IoT Gateway (Push-based Approach)</h1>

In this lab, you will create an event-based IoT gateway that collects data from multiple data sources and notifies the interested users if an event occurs in the system. To achieve this, we will take the advantage of a publish subscribe messaging system that uses MQTT protocol and enables multiple users to subscribe for event notifications. Upon the occurrence of an event, the message broker informs the subscribers of that event. The following event demonstrates a very high-level architecture of what a publish subscribe system may look like.

The publishers and subscribers use a naming scheme to communicate with each other. In this lab you will use a hierarchical URI-based naming scheme. For instance, <strong>“utoronto/GB119/sensor1/temperature”</strong> is a hierarchical name that specifies the temperature data which belongs to a geographical location. Names also refer as Topics in such systems. Each document and subscriber with a different color in the above figure refers to a specific topic in the system.

In this lab, we will collect the Air Pollution and Weather Information data from two open IoT data platform APIs.

<ul>

 <li>Air Quality API accessible at: <a href="https://aqicn.org/api/">https://aqicn.org/api/</a></li>

 <li>Current Weather API accessible at: <a href="https://openweathermap.org/price">https://openweathermap.org/</a></li>

</ul>

To access to these APIs, you need to get a token. For Air Quality API, navigate to <a href="https://aqicn.org/data-platform/token/#/">https://aqicn.org/data</a><a href="https://aqicn.org/data-platform/token/#/">–</a><a href="https://aqicn.org/data-platform/token/#/">platform/token/#/</a> and fill your email and preferred name to get your token.

For Current Weather API navigate to <a href="https://openweathermap.org/appid">https://openweathermap.org/appid</a> and click on Sign up and create an account to get your token. You can always have access to your tokens and create more by navigating to the token page available at <a href="https://home.openweathermap.org/api_keys">https://home.openweathermap.org/api_keys</a><a href="https://home.openweathermap.org/api_keys">.</a>

<strong>After successfully receiving your tokens</strong> you can use the following API calls to retrieve data from the specified data sources.

<ul>

 <li>Air Quality API:</li>

 <li><a href="http://api.waqi.info/feed/tehran/?token=d43e9f02fcff197a80275c71fc4a73fa787c972c">http://api.waqi.info/feed/”The City Name”/?token=”Your Token”</a> &#x25aa; Please replace the items in quotation mark with your values.</li>

 <li>Current Weather API:</li>

 <li><a href="https://api.openweathermap.org/data/2.5/weather?q=Toronto,ca&amp;appid=f7f9042c24d383d023efdd0b2394453f">https://api.openweathermap.org/data/2.5/weather?q=”City</a></li>

</ul>

<a href="https://api.openweathermap.org/data/2.5/weather?q=Toronto,ca&amp;appid=f7f9042c24d383d023efdd0b2394453f">Name”,”Country Code”&amp;appid=”Your Token”</a>

&#x25aa; Please replace the items in quotation mark with your values.  &#x25aa; For instance, you can use “ca” to refer to Canada.

Upon calling each API, you will receive a JSON document that provides you with the latest update of the platform data with reference to your input parameters. The followings show an example of the two APIs digest.

<ul>

 <li>Current Weather API:</li>

</ul>










<ul>

 <li>Air Quality API:</li>

</ul>

<strong>Note 8</strong>: Please refer to <a href="https://aqicn.org/">http://aqicn.org</a> and <a href="https://api.openweathermap.org/">https://api.openweathermap.org</a> for more information about the APIs.

<h1>Tasks to Complete</h1>

<ol>

 <li>For this part of the lab, you need to create two publishers.</li>

</ol>

<ul>

 <li><strong>Air Quality Publisher: </strong>Your publisher performs two important tasks.</li>

 <li><strong>Data collection</strong>: Your publisher calls the Air Quality API for the following cities in the world and collect their Air Quality Index every hour for a continues duration of 24 hours. Cities are: {Toronto, Vancouver, Newyork, Shanghai, Tehran, London, Seoul, Jakarta, Istanbul, and Tokyo}.</li>

</ul>

<strong>Example:</strong> <a href="http://api.waqi.info/feed/newyork/?token=%22Your%20Token%22">http://api.waqi.info/feed/newyork/?token=”Your Token”</a>

<ul>

 <li><strong>Event notification</strong>: Your publisher must publish each cities Air Quality Index with its associated city name as the message topic to the message broker. Use the following naming scheme to publish Air Quality data for each city.</li>

</ul>

&#x25aa; ece1508/city_name/aqi → Example: ece1508/toronto/aqi

<strong>Note 9: </strong>You must publish the data for every city once you call the API every hour. <strong>Do not save</strong> the whole data and send them at once.

<ul>

 <li><strong>Current Weather Publisher</strong>: Your publisher performs three important tasks.</li>

 <li><strong>Data Collection</strong>: Your publisher calls the Current Weather API for the following cities in the world and collect their temperature and humidity every hour for a continuous duration of 24 hours. Cities are: {Toronto, Vancouver, Newyork, Shanghai, Tehran, London, Seoul, Jakarta, Istanbul, and Tokyo}.</li>

</ul>

<strong>Example:</strong><a href="https://api.openweathermap.org/data/2.5/weather?q=toronto,ca&amp;appid=%22Your%20Token%22">https://api.openweathermap.org/data/2.5/weather?q=toro </a><a href="https://api.openweathermap.org/data/2.5/weather?q=toronto,ca&amp;appid=%22Your%20Token%22">nto,ca&amp;appid=”Your Token”</a>

<ul>

 <li><strong>Calculating the Heat Index</strong>: You need to calculate the Heat Index according to the following formula for each time you collect data (every hour) and for each city separately. The Heat Index indicates what we know as <strong>“feels like”</strong>.</li>

</ul>




In the above formula use the following values for the variables.

T = Ambient dry-bulb temperature (in degrees of Celsius) → You need to convert the temperature from Kelvin (API-Specific measurement) to Celsius according to the following formula.




R = Relative humidity in percentage (between 0-100)

HI = Heat index in degrees of Celsius

For the values of co-efficient parameters please use the followings:




<ul>

 <li><strong>Event notification</strong>: Your publisher must publish each cities Heat Index with the city name as the message topic to the message broker. Use the following naming scheme to publish Heat Index for each city.</li>

</ul>

&#x25aa; ece1508/city_name/hi → Example: ece1508/toronto/hi

<strong>Note 10: </strong>You must publish the data for every city once you call the API every hour and calculate the Heat Index. <strong>Do not save</strong> the whole data and send them at once.

<ol start="2">

 <li>For this part of the lab, you need to create two subscribers to receive the publisher’s data and <strong>plot the hourly changes as a function of time (24 hours) for each city independently</strong>.

  <ul>

   <li><strong>Air Quality Subscriber</strong>: The subscriber must subscribe for the same topics that you specified to publish your data. In the event of an update, the subscriber receives the data from the message broker. Can you find any specific pattern in the graphs?</li>

  </ul></li>

</ol>

<strong>In you report</strong>: Include your graphs and explain your answer.

<ul>

 <li><strong>Current Weather Subscriber</strong>: The same as above, you need to create a subscriber to receive the Heat Index of each city. In the event of an update, the subscriber gets notified by the message broker and will receive the data. Can you find any specific pattern in the graphs? <strong>In you report</strong>: Include your graphs and explain your answer.</li>

</ul>

<ol start="3">

 <li>Can you see any specific cross-relationship in the movement pattern of Heat Index and Air Pollution Index for the specified cities? <strong>In your report</strong>: Explain your answer.</li>

</ol>

<strong>Note 11</strong>: In addition to your answers and graphs that you provided for each section, you must include your Publishers and Subscribers code. For verification, we run our publishers with your subscribers to test the outcomes.

<strong>Important Point</strong>: For this lab, you need to use the following pieces of information to connect publishers and subscribers to the message broker.

<ul>

 <li><strong>MQTT Message Broker IP address</strong>: 142.150.208.252</li>

 <li><strong>Port Number</strong>: TCP 1883</li>

</ul>

<strong>Note 12</strong>: Please run your subscribers before the publishers.




<ul>

 <li><strong>A .pdf document</strong> that contains the answer to all the questions in the lab.</li>

 <li><strong>The code you developed</strong> for the publishers and subscribers. Please note that you must use Python to create the publishers and subscribers. Your final submission should include two publishers and two subscribers with the following names with reference with the API endpoints they work with.</li>

</ul>

o <strong>Air Quality API: </strong>

<ul>

 <li>Publisher name →py</li>

 <li>Subscriber name →py o <strong>Current Weather API: </strong></li>

 <li>Publisher name →py</li>

 <li>Subscriber name →py</li>

</ul>

<strong>Note 13</strong>: Please provide informative comments on your code, if it is necessary to understand a part of it.

<strong>Important Note</strong>: The implementation of MQTT protocol for a sample publisher and subscriber will be provided to you. You can use them as a function in your code to establish communication with the MQTT message broker.

<strong>             </strong>

<h1>Useful Material</h1>

Since we use the MQTT protocol on publishers and subscribers to communicate with the message broker, it might be useful to know how to work with the protocol. The following links provide additional information that may help you while you are writing your code.

<ul>

 <li><a href="https://github.com/mqtt/mqtt.github.io/wiki">https://github.com/mqtt/mqtt.github.io/wiki</a></li>

 <li><a href="http://www.steves-internet-guide.com/into-mqtt-python-client/">http://www.steves</a><a href="http://www.steves-internet-guide.com/into-mqtt-python-client/">–</a><a href="http://www.steves-internet-guide.com/into-mqtt-python-client/">internet</a><a href="http://www.steves-internet-guide.com/into-mqtt-python-client/">–</a><a href="http://www.steves-internet-guide.com/into-mqtt-python-client/">com/into</a><a href="http://www.steves-internet-guide.com/into-mqtt-python-client/">–</a><a href="http://www.steves-internet-guide.com/into-mqtt-python-client/">mqtt</a><a href="http://www.steves-internet-guide.com/into-mqtt-python-client/">–</a><a href="http://www.steves-internet-guide.com/into-mqtt-python-client/">python</a><a href="http://www.steves-internet-guide.com/into-mqtt-python-client/">–</a><a href="http://www.steves-internet-guide.com/into-mqtt-python-client/">client/</a></li>

</ul>

During this lab, you may need to visualize data and create plots in your program. The “matplotlib” is a powerful plotting library which you can use to create plots in your program. The following links may help you to use the library and its features.

<ul>

 <li><a href="https://matplotlib.org/users/pyplot_tutorial.html">https://matplotlib.org/users/pyplot_tutorial.html</a></li>

 <li><a href="https://swcarpentry.github.io/python-novice-gapminder/09-plotting/">https://swcarpentry.github.io/python</a><a href="https://swcarpentry.github.io/python-novice-gapminder/09-plotting/">–</a><a href="https://swcarpentry.github.io/python-novice-gapminder/09-plotting/">novice</a><a href="https://swcarpentry.github.io/python-novice-gapminder/09-plotting/">–</a><a href="https://swcarpentry.github.io/python-novice-gapminder/09-plotting/">gapminder/09</a><a href="https://swcarpentry.github.io/python-novice-gapminder/09-plotting/">–</a><a href="https://swcarpentry.github.io/python-novice-gapminder/09-plotting/">plotting/</a></li>

</ul>

The following link may also be helpful in setting you up to work with the external APIs in Python. You may find more useful resources on Internet as well.

<ul>

 <li><a href="https://www.dataquest.io/blog/python-api-tutorial/">https://www.dataquest.io/blog/python</a><a href="https://www.dataquest.io/blog/python-api-tutorial/">–</a><a href="https://www.dataquest.io/blog/python-api-tutorial/">api</a><a href="https://www.dataquest.io/blog/python-api-tutorial/">–</a><a href="https://www.dataquest.io/blog/python-api-tutorial/">tutorial/</a></li>

</ul>

<strong>Note 14</strong>: You are not limited to use any libraries in this lab. Feel free to take the advantage of any library that you are familiar with to do this assignment.





