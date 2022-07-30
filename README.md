## Prometheus

Prometheus is a database optimized for time series data and an ideal way to store monitoring metrics
- Fully integrated time series DBMS and monitoring system
- Scraping, storing, querying, graphing, and alerting based on time series data; provides API endpoints for the data it holds
- Implemented in Go
- Data types handled Numeric
- Data collection: Active or pull
  
## InfluxDB
InfluxDB is a time series database designed for fast, high-availability storage and retrieval of time series data. It can work as a stand-alone solution, or it can be used to process data from Graphite
- Stores numeric time series data
- Implemented in Go
  

## Features
### Data Collection

InfluxDB is a push-based system. It requires an application to actively push data into InfluxDB.

Prometheus is a pull-based system. An application publishes the metrics at a given endpoint, and Prometheus fetches them periodically.

### Storage
InfluxDB is much more suitable for event logging. Prometheus is focused on metrics recording.

### Visualization and Dashboards

Both Prometheus and InfluxDB feature basic visualizations and dashboards. To truly shine, they should be deployed alongside dedicated visualization and dashboard solutions, such as OSS grafana or Chronograf.

## Key differences between Prometheus and InfluxDB

- The most notable difference is between the scopes of these platforms. Both systems could be used for monitoring and time-series data storing. However, InfluxDB is more known as a time-series database, while Prometheus has a broader scope of monitoring purposes.

- Actually, InfluxDB itself cannot be used for the tasks of data visualization or alerting. We should use other instruments from the TICK-stack: Kapacitor for alerting and Chronograf for visualization. At the same time, Prometheus also needs to use Alertmanager to send notifications, but defining the alerting and recording rules can be done directly in the Prometheus interface. Additionally, Alertmanager provides features for deduplication, grouping, and silencing. Prometheus has many components but they fit together seamlessly.

- InfluxDB uses its own query language - InfluxQL. It is very similar to the usual SQL, so if you know the latest, there shouldn’t be any problem to create an InfluxQL query. Prometheus provides a functional language for querying called PromQL.

- Somebody can consider InfluxQL simpler for people who worked previously with SQL, but PromQL is actually very easy and powerful. It was developed specifically for monitoring purposes, alerting and graphing. It is less wordy than InfluxQL and provides a range of convenient functions

- Prometheus servers, as well as InfluxDB, can be united in clusters to be able to process high load. But Prometheus servers (and servers running the open-source InfluxDB version) are independent of each other by default. This means each server uses its own local resources. When your processing requirements increase, you should take care to set up a cluster of servers (both for Prometheus and InfluxDB).

- But the commercial version of InfluxDB is different. It is a distributed cluster solution by default. So, it consists of many nodes that interact together. So, when the load increases, you don’t have to worry about scaling. On the other hand, you will have to manage a complex cluster from the very beginning, which may be difficult. If you don’t need to process high load, it can even be considered redundant. Prometheus and the open-sourced version of InfluxDB are easier to manage if your use case is standard and relatively simple.

- Anyway, remember that when you use our Hosted Prometheus solution, you avoid all the headache caused by setting up and maintaining the Prometheus cluster.

- InfluxDB supports float64, int64, bool, and string data types. The Prometheus’ main data type is float64 (however, it has limited support for strings).

- Prometheus can write data with the millisecond resolution timestamps. InfluxDB is more advanced in this regard and can work with even nanosecond timestamps.

- Prometheus uses an append-only file per time-series approach for storing data. InfluxDB uses another method of storing, that is considered better for working with events logging.

- Prometheus is developed to pull metrics periodically from the target system. Alternatively, InfluxDB expects that an application will be sending data to it. So, when working with InfluxDB, you should set up the target system to push data to the InfluxDB server. For similar situations, you can use Prometheus push gateway in situations where metrics cannot be pulled.
  
- Now there is a difference as well in the way we query on these platforms. Both have their only query language know as InflusQL and PromQL. InfluxQL is very much similar to traditional SQL, and querying is quite easy. PromQL is more of a functional language for querying. For associates with SQL, skills will be comfortable with InfluxQL, but PromQL is not that difficult. Thus bot querying Langues is efficient in querying the records from the stored data.

## Summary
Both of these products are excellent time series databases. They differ in their default mode (push for InfluxDB, pull for Prometheus). Some people argue that PromQL, Prometheus’ language, is simpler than the language used by InfluxDB, but, all in all, the decision to use one tool or the other will probably depend on your use case. If monitoring is what you’re most interested in, Prometheus is your safest bet because of its many integrations and scalable model. If you’re more likely to be using a time series database for IoT, sensors, or analytics, then you’ll probably want to choose InfluxDB.

### Where InfluxDB is better:

- If you're doing event logging.
- Commercial option offers clustering for InfluxDB, which is also better for long term data storage.
- Eventually consistent view of data between replicas.

### Where Prometheus is better:

- If you're primarily doing metrics.
- More powerful query language, alerting, and notification functionality.
- Higher availability and uptime for graphing and alerting.