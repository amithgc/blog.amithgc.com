---
title: "How to keep Elastic Search Clean"
date: 2023-01-20T16:12:51+05:30
description: How to keep Elastic Search Clean
authorbox: true
sidebar: false
thumbnail: "img/ess.jpeg"
pager: true
categories:
  - "Development"
  - "Automation"
tags:
  - "LINUX"
  - "CODE"
  - "ELASTIC SEARCH"
  - "DEV-OPS"
---

Elasticsearch is a powerful search engine that can help you search, analyze, and visualize your data. However, as you add more and more data to your Elasticsearch indices, they can become cluttered and difficult to manage. In this blog, we will discuss how to keep your Elasticsearch indices clean and organized, as well as provide some shell scripts to help you automate the process.

First, let's define what we mean by "clean" Elasticsearch indices. Clean indices are well-organized, with data that is easy to search, analyze, and visualize. They also use minimal storage space and resources, which can help improve the performance of your Elasticsearch cluster.

There are several ways to keep your Elasticsearch indices clean:

- **Use appropriate mapping**: When you create an index in Elasticsearch, you need to specify the mapping, which defines the fields in your documents and their data types. Using the appropriate mapping can help ensure that your data is stored in an efficient and organized way. For example, if you are storing dates, you should use the "date" data type rather than a string.
- **Use the right number of shards**: When you create an index, you can specify the number of shards that it should have. Shards are used to distribute the data in an index across multiple nodes in your Elasticsearch cluster. Having the right number of shards can help improve the performance and scalability of your cluster. However, having too many shards can also cause problems, such as increased resource usage and slower search performance.
- **Use the right number of replicas**: Similar to shards, you can also specify the number of replicas for each index. Replicas are used to provide fault tolerance in case a node goes down. However, having too many replicas can also cause problems, such as increased resource usage and slower search performance.
- **Use aliases**: Aliases are like "pointers" to specific indices or groups of indices. You can use aliases to simplify your search queries, as well as to perform actions such as updating mapping or changing the number of replicas on a group of indices.
Use index templates: Index templates are used to define the settings and mapping for new indices that match a specific pattern. You can use index templates to ensure that all of your indices have the same settings and mapping, which can make it easier to manage your Elasticsearch cluster.
- **Use time-based indices**: If you are storing data that has a time component, such as log data, you can use time-based indices to store your data. This can make it easier to search and analyze your data, as well as to delete old data that is no longer needed.

Now that we've covered some best practices for keeping your Elasticsearch indices clean, let's look at some shell scripts that you can use to automate the process.

---

### Script 1: Delete old indices

```bash
#!/bin/bash

# Set the number of days after which an index should be deleted
num_days=30

# Get the current date and time in UTC
now=$(date -u +"%Y.%m.%d")

# Get a list of indices
indices=$(curl -X GET "localhost:9200/_cat/indices?v" | awk '{print $3}')

# Loop through the indices
for index in $indices
do
  # Get the index creation date
  index_date=$(echo $index | grep -oP '(?<=\.)\d{4}\.\d{2}\.\d{2}')

  # Calculate the difference in days between the index creation date and the current date
  diff=$((($(date -d "$now" +%s) - $(date -d "$index_date" +%s)) / 86400))

  # If the index is older than the specified number of days, delete it
  if [[ $diff -gt $num_days ]]
  then
    curl -X DELETE "localhost:9200/$index"
  fi
done
```

---

### Script 2: Close and delete indices

This script will close and delete indices that are older than a certain number of days. This can be useful if you want to free up resources on your Elasticsearch cluster, but you still want to keep the data available for reference:

```bash

#!/bin/bash

# Set the number of days after which an index should be closed and deleted
num_days=30

# Get the current date and time in UTC
now=$(date -u +"%Y.%m.%d")

# Get a list of indices
indices=$(curl -X GET "localhost:9200/_cat/indices?v" | awk '{print $3}')

# Loop through the indices
for index in $indices
do
  # Get the index creation date
  index_date=$(echo $index | grep -oP '(?<=\.)\d{4}\.\d{2}\.\d{2}')

  # Calculate the difference in days between the index creation date and the current date
  diff=$((($(date -d "$now" +%s) - $(date -d "$index_date" +%s)) / 86400))

  # If the index is older than the specified number of days, close and delete it
  if [[ $diff -gt $num_days ]]
  then
    curl -X POST "localhost:9200/$index/_close"
    curl -X DELETE "localhost:9200/$index"
  fi
done
```

--- 

### Script 3: Optimize indices

Over time, Elasticsearch indices can become fragmented, which can affect their performance. You can use the following script to optimize your indices by merging the segments in each index:

```bash
#!/bin/bash

# Set the number of segments that should be merged
max_num_segments=1

# Get a list of indices
indices=$(curl -X GET "localhost:9200/_cat/indices?v" | awk '{print $3}')

# Loop through the indices
for index in $indices
do
  # Get the number of segments in the index
  num_segments=$(curl -X GET "localhost:9200/$index/_segments" | jq '.indices | .[].segments | length')

  # If the index has more than the specified number of segments, optimize it
  if [[ $num_segments -gt $max_num_segments ]]
  then
    curl -X POST "localhost:9200/$index/_forcemerge?max_num_segments=$max_num_segments"
  fi
done
```

### Script 4: Update mapping

If you need to update the mapping for one or more indices, you can use the following script to do so:

```bash
#!/bin/bash

# Set the name of the index
index_name="my_index"

# Set the new mapping
new_mapping='{
  "properties": {
    "field1": {
      "type": "text"
    },
    "field2": {
      "type": "integer"
    }
  }
}'
```

