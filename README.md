
# HousePricePrediction-Data-Pipeline-Curation-


## Architecture Overview

![](https://raw.githubusercontent.com/saLeox/photoHub/main/20210501101750.png)

 **1. Ingest Layer**
 
[Set up the Kafka cluster](https://github.com/saLeox/kafka-cluster-docker-setup) with monitoring tools in the form of Docker compose.
Collect the house transation data as an event and send to Kafka topic.
	
 **2. [Speed Layer](https://github.com/saLeox/HousePricePrediction-Streaming-Data-Pipeline)**
 
 Kafka producer & consumer.
 Streaming ETL that will sink to Big Query.
 Materialize the KTable of count based on the tumbling timewindow.
 
 **3. [Batch Layer](https://github.com/saLeox/HousePricePrediction-BatchTraining)**
 
Train the Regression Model by machine learning API provided by Spark MLlib and persist into GCS.
Use metrics to evaluate the performance of each Model.

 **4. Serving Layer:**
 
Load the ML model inside [SpringBoot application](https://github.com/saLeox/HousePricePrediction-ServingAPI) to provide prediction function.
Provide [interactive query](https://github.com/saLeox/HousePricePrediction-Streaming-Data-Pipeline/blob/main/src/main/java/com/gof/springcloud/streams/query/InteractiveQueryController.java) based Kafka Timewindow Streaming.

## Limitation and Future Enhancement

 - [ ] Integrate the Neural Network to solve regression problem by using
       deeplearning4j.
 - [ ] Use Flink & Alink to achieve the unified online & offline machine
       learning, since the Spark MLlib only provide the streaming linear regression model for the regression problem.
 - [ ] Embed the pre-processing and feature engineering into pipeline
       and make them automatically.
