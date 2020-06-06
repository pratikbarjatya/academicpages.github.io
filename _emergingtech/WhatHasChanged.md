---
title: "Emerging Tech - Data Story: What has Changed?"
collection: emergingtech
type: "Data Story: What has Changed?"
permalink: /emergingtech/WhatHasChanged
date: 2019-05-24
location: "Mumbai, India"
---


Data Story: What has Changed?
======

- Business Intelligence -> Big Data
- Traditional Data Warehouse -> Data Lake
- Applications -> Microservices
- ETL ->  ETL is next on list of obsolete terms
- Rise of Spark -> Spark provides an ideal middleware framework for writing code that gets the job done fast, reliable, readable.

The Future of ETL Tools?
======
- Only develop connectors for integration?
- Re-build entire backend to Hadoop/Spark/Flink?
- Provide a GUI with code genration?

What is ETL Hell?
======
- Data getting out of sync
- Performance issues
- Waste of server resources (peak performance)
- Plain text codes in hidden stages
- Click, click, click, click (RSI danger!)
- CSV files are not type safe
- All-or-nothing approach in batch jobs
- Legacy code

Is NoETL the future?
======
Why NoETL? ETL is an intermediary step, and at each ETL step you can introduce errors and risk:
- ETL can lose data
- ETL can duplicate data after failover
- ETL tools can cost millions of dollars
- ETL decreases throughput
- ETL increases the complexity of the pipeline <br>
source: [noetl.org](https://noetl.org/)

Key Takeaways
=======
- Pick one: ETL, ELTm ELTL,..
- Treat all data equal: batch and stream
- Continuous ETL: don't wait for a phase to complete
- Don't just transform: enrich, alert, predict
- Build for scale: distribute data nad logic
- Automate everything
- Think about NoETL: each copy is a risk!
