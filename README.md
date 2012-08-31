[dl_jar]: https://github.com/downloads/mcclaskc/statsmix_jar/statsmix.jar
[dl_dep]: https://github.com/downloads/mcclaskc/statsmix_jar/statsmix-lib-dependencies.tar.gz
[track_exmpl]: https://github.com/mcclaskc/statsmix_jar/blob/master/examples/Track.java

StatsMix
========
This java library offers easy access to the StatsMix API. See www.statsmix.com/developers/documentation for more information.
Download and Install
--------------------
The jar file: [statsmix.jar] [dl_jar] <br />
It's dependencies: [statsmix-lib-dependencies.] [dl_dep] <br />  

Usage 
------
###Initialize
Create a new StatsMix Client
```java
import com.statsmix.*
Client smClient = new Client("YOUR_API_KEY");
```
###Track
The track method sends a request to the track API, and returns the XML response as a string. The following snippets were taken from [this example file.] [track_exmpl] 

Basic Tracking.  Adds a new stat with default value of 1 to the metric.
```java
smClient.track("metric_name");
```

Track with a value other than one
```java
smClient.track("metric_name", 5.2);
```

Track with additional properties
```java
List<NameValuePair> properties = new ArrayList<NameValuePair>(2);
properties.add(new BasicNameValuePair("value", "5.2"));  //if you do not include the value, it will default to 1
properties.add(new BasicNameValuePair("ref_id", "java01"));
properties.add(new BasicNameValuePair("generated_at", getDateTime()));
smClient.track("metric_name", properties);
```

Track with meta data
```java
JSONObject meta = new JSONObject();
meta.put("food", "icecream");
meta.put("calories", 500);
smClient.track("metric_name", properties, meta);
```

A method for formating the date
```java
public String getDateTime() {
    DateFormat dateFormat = new SimpleDateFormat("yyyy/MM/dd HH:mm:ss");
    Date date = new Date();
    return dateFormat.format(date);
}
```