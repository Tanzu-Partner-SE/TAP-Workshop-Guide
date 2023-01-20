Sometimes an application isn't behaving quite like we'd expect after deployment, and we want to get more information about its runtime behavior, for diagnostics and troubleshooting. Is our application running out of memory? What was the response time for HTTP Requests?

Tanzu Application Platform provides Live View to help a developer like Cody gather that information. Let's take a look. We're going to access the Web UI known as TAP GUI, which can observe the deployment we just created:

```dashboard:open-url
url: https://tap-gui.{{ ENV_VIEW_CLUSTER_DOMAIN }}/catalog/default/component/partnertapdemo/workloads
```

###### In Tap GUI, Click on deployment resource as shown below: 

![Component View](images/live-21.png)

Here we are looking at running deployments of `partnertapdemo`, our application. There's a good chance that you see more than one deployment listed! That's because we are in a multitenant development environment, and different developers (or different workshop sessions) are each working on their own branch of the code. In a multi-tenant development cluster (also known as an Iterate cluster in TAP), each developer works in their own namespace for isolation.

Your developer namespace is **``tap-install``**. You can identify which `partnertapdemo` app is yours by checking against the namespace column. Click on the partnertapdemo hyperlink in the row that corresponds to your namespace. This will bring you to a detail view of your app:

![Component View](images/component-view.png)

If you scroll down in this screen, you will see the Kubernetes resources associated with your app. At the bottom of the screen, you'll find Pods. In Kubernetes, a Pod is where your application container runs. Your pod will have a long, funny name, click on it:

![Pod View](images/pod-view.png)

Scroll down a little bit, and you'll find our Live View pane. It has a menu drop-down called Information Category that allows you to navigate all sorts of data in your Application Runtime.

![Live View](images/live-view.png)

##### Health page

To navigate to the Health page, select the Health option from the Information Category drop-down. The health page provides detailed information about the health of the app.

The page includes the following features:

  - View a list of all the components that make up the health of the app, such as readiness, liveness, and disk space.
  - View a display of the status and details associated with each of the components.

![Local host](images/Live-1.png)

##### Environment page

To navigate to the Environment page, select the Environment option from the Information Category drop-down. The environment page contains details of the app's environment. It contains properties including, but not limited to, system properties, environment variables, and configuration properties such as application.properties in a Spring Boot app.

![Local host](images/Live-2.png)
    
##### Log Levels page

To navigate to the Log Levels page, select the Log Levels option from the Information Category drop-down. The log levels page provides access to the app's loggers and the configuration of their levels.

The page includes the following features:

   - Configure the log levels, such as INFO, DEBUG, TRACE, in real-time from the UI.
   - Search for a package and edit its respective log level.
   - Configure the log levels at a specific class and package.
   - Deactivate all the log levels by modifying the log level of root logger to OFF.
   - Display the changed log levels using the Changes Only toggle.
   - Search by logger name using the search feature.
   - Reset the log levels to the original state clicking Reset.
   - Reset all the loggers to default state by clicking Reset All at the top right corner of the page.

![Local host](images/Live-3.png)

##### Threads page

To navigate to the Threads page, select the Threads option from the Information Category drop-down. This page displays all details related to JVM threads and running processes of the app. This tracks live threads and daemon threads real-time. It is a snapshot of different thread states.

The page includes the following features:

   - Navigate to a thread state to display all the information about a particular thread and its stack trace.
   - Search for threads by thread ID or state using the search feature.
   - Refresh to the latest state of the threads using the refresh icon.
   - View more thread details by clicking on the thread ID.
   - Download a thread dump for analysis purposes.

![Local host](images/Live-4.png)

##### Memory page

To navigate to the Memory page, select the Memory option from the Information Category drop-down.

The memory page highlights the memory use inside of the JVM. It displays a graphical representation of the different memory regions within heap and non-heap memory. For Spring Boot apps running on a JVM, this visualizes data from inside of the JVM, and therefore provides memory insights into the app in contrast to "outside" information about the Kubernetes pod level.

The page includes the following features:

   - View real-time graphs that display a stacked overview of the different spaces in memory along with the total memory used and total memory size.
   - View graphs to display the GC pauses and GC events.
   - Download heap dump data using the Heap Dump button at the top right corner.

![Local host](images/Live-5.png)

##### Request Mappings page

To navigate to the Request Mappings page, select the Request Mappings option from the Information Category drop-down. This page provides information about the app's request mappings. For each mapping, the page displays the request handler method.

The page includes the following features:

   - View more details about the request mapping, such as the header metadata of the app including the produces, consumes, and HTTP methods, by clicking on the mapping.
   - Search on the request mapping or the method.
   - View the actuator related mappings for the app using the toggle /actuator/** Request Mappings

![Local host](images/Live-6.png)

##### HTTP Requests page

To navigate to the HTTP Requests page, select the HTTP Requests option from the Information Category drop-down. The HTTP Requests page provides information about HTTP request-response exchanges to the app. The graph visualizes the requests per second indicating the response status of all the requests.

The page includes the following features:

   - Filter on the response statuses which include info, success, redirects, client-errors, and server-errors.
   - View the trace data, captured in detail in a tabular format with metrics such as timestamp, method, path, status, content-type, length, and time.
   - Filter the traces based on the search field value using the search feature on the table
   - View more details of the request such as method, headers, and response of the app by clicking on the timestamp.
   - Click the refresh icon above the graph to load the latest traces for the app.
   - Display the actuator related traces for the app using the toggle /actuator/** at the top right corner of the page.

![Local host](images/Live-7.png)

##### Configuration Properties page

To navigate to the Configuration Properties page, select the Configuration Properties option from the Information Category drop-down. The configuration properties page provides information about the configuration properties of the app. For Spring Boot, it displays the app's @ConfigurationProperties beans. It gives a snapshot of all the beans and their associated configuration properties.

The page includes the following feature:

 - Look up a key-value for a property or bean name using the search feature.

![Local host](images/Live-8.png)

##### Conditions page

To navigate to the Conditions page, select the Conditions option from tthe Information Category drop-down. The conditions evaluation report provides information about the evaluation of conditions on configuration and auto-configuration classes. For Spring Boot, this gives the user a clear view of all the beans configured in the app.

The page includes the following features:

   - Click on the bean name to view the conditions and the reason for the conditional match. If beans are not configured, it shows both the matched and unmatched conditions of the bean if any. In addition to this, it also displays names of unconditional auto configuration classes if any.
   - Filter on the beans and the conditions using the search feature.

![Local host](images/Live-9.png)

##### Beans page

To navigate to the Beans page, select the Beans option from the Information Category drop-down. The beans page provides information about a list of all app beans and its dependencies. It displays the information about the bean type, dependencies, and its resource.

The page includes the following feature:

   - Search by the bean name or its corresponding fields.

![Local host](images/liveview-23.png)

##### Metrics Page

To navigate to the Metrics page, select the Metrics option from the Information Category drop-down. The metrics page provides access to app metrics information.

The page includes the following features:

   - Choose from the list of various metrics available for the app such as jvm.memory.used, jvm.memory.max, http.server.request. After you choose the metric, you can view the associated tags.
   - Choose the value of each of the tags based on filtering criteria.
   - Click Add Metric to add the metric, which is refreshed every five seconds by default.
   - Pause the auto refresh feature by disabling the Auto Refresh toggle.
   - Refresh the metrics manually by clicking Refresh All.
   - Change the format of the metric value according to your needs.
   - Delete a particular metric by clicking on the minus symbol in the same row.

![Local host](images/Live-11.png)

##### Actuator Page
To navigate to the Actuator page, select the Actuator option from the Information Category drop-down. The actuator page provides a tree view of the actuator data.

The page includes the following feature:

   - Choose from a list of actuator endpoints and parse through the raw actuator data.

![Local host](images/Live-12.png)



