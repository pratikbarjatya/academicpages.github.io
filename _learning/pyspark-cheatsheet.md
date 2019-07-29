---
title: "PySpark Cheat Sheet"
excerpt: "PySpark Cheat Sheet"
collection: learning
date: 2019-07-29
---

🐍 📄 PySpark Cheat Sheet
======

- A quick reference guide to the most commonly used patterns and functions in PySpark SQL.

    - Importing Functions & Types
        - Easily reference these as F.my_function() and T.my_type() below
        {% highlight ruby %}
        from pyspark.sql import functions as F, types as T
        {% endhighlight %}

    - Filtering
        - # Filter on equals condition
        {% highlight ruby %}
         df = df.filter(df.is_adult == 'Y')
        {% endhighlight %}

        - # Filter on >, <, >=, <= condition
        {% highlight ruby %}
         df = df.filter(df.age > 25)
        {% endhighlight %}

        - # Multiple conditions require parens around each
        {% highlight ruby %}
         df = df.filter((df.age > 25) & (df.is_adult == 'Y'))
        {% endhighlight %}

    - Joins
        - # Left join in another dataset
        {% highlight ruby %}
         df = df.join(person_lookup_table, 'person_id', 'left')
        {% endhighlight %}

        - # Useful for one-liner lookup code joins if you have a bunch
        {% highlight ruby %}
         def lookup_and_replace(df1, df2, df1_key, df2_key, df2_value):
            return (
                df1
                .join(df2[[df2_key, df2_value]], df1[df1_key] == df2[df2_key], 'left')
                .withColumn(df1_key, F.coalesce(F.col(df2_value), F.col(df1_key)))
                .drop(df2_key)
                .drop(df2_value)
            )

         df = lookup_and_replace(people, pay_codes, id, pay_code_id, pay_code_desc)
        {% endhighlight %}

    - Creating New Columns
        - # Add a new static column
        {% highlight ruby %}
         df = df.withColumn('status', F.lit('PASS'))
        {% endhighlight %}

        - # Construct a new dynamic column
        {% highlight ruby %}
         df = df.withColumn('full_name', F.when(
            (df.fname.isNotNull() & df.lname.isNotNull()), F.concat(df.fname, df.lname)
         ).otherwise(F.lit('N/A'))
        {% endhighlight %}

    - Coalescing Values
        - # Take the first value that is not null
        {% highlight ruby %}
         df = df.withColumn('last_name', F.coalesce(df.last_name, df.surname, F.lit('N/A')))
        {% endhighlight %}

    - Casting, Nulls & Duplicates
        - # Cast a column to a different type
        {% highlight ruby %}
         df = df.withColumn('price', df.price.cast(T.DoubleType()))
        {% endhighlight %}

        - # Replace all nulls with a specific value
        {% highlight ruby %}
         df = df.fillna({
            'first_name': 'Tom',
            'age': 0,
         })
        {% endhighlight %}

        - # Drop duplicate rows in a dataset (distinct)
        {% highlight ruby %}
         df = df.dropDuplicates()
        {% endhighlight %}

        - # Drop duplicate rows, but consider only specific columns
        {% highlight ruby %}
         df = df.dropDuplicates(['name', 'height'])
        {% endhighlight %}

    - Column Operations
        - # Pick which columns to keep, optionally rename some
        {% highlight ruby %}
         df = df.select(
            'name',
            'age',
            F.col('dob').alias('date_of_birth'),
         )
        {% endhighlight %}

        - # Remove columns
        {% highlight ruby %}
         df = df.drop('mod_dt', 'mod_username')
        {% endhighlight %}

        - # Rename a column
        {% highlight ruby %}
         df = df.withColumnRenamed('dob', 'date_of_birth')
        {% endhighlight %}

        - # Keep all the columns which also occur in another dataset
        {% highlight ruby %}
         df = df.select(*(F.col(c) for c in df2.columns))
        {% endhighlight %}

        - # Batch Rename/Clean Columns
        {% highlight ruby %}
         for col in df.columns:
            df = df.withColumnRenamed(col, col.lower().replace(' ', '_').replace('-', '_'))
        {% endhighlight %}

    - String Operations
        String Filters
        - # Contains - col.contains(string)
        {% highlight ruby %}
         df = df.filter(df.name.contains('o'))
        {% endhighlight %}

        - # Starts With - col.startswith(string)
        {% highlight ruby %}
         df = df.filter(df.name.startswith('Al'))
        {% endhighlight %}

        - # Ends With - col.endswith(string)
        {% highlight ruby %}
         df = df.filter(df.name.endswith('ice'))
        {% endhighlight %}

        - # Is Null - col.isNull()
        {% highlight ruby %}
         df = df.filter(df.is_adult.isNull())
        {% endhighlight %}

        - # Is Not Null - col.isNotNull()
        {% highlight ruby %}
         df = df.filter(df.first_name.isNotNull())
        {% endhighlight %}

        - # Like - col.like(string_with_sql_wildcards)
        {% highlight ruby %}
         df = df.filter(df.name.like('Al%'))
        {% endhighlight %}

        - # Regex Like - col.rlike(regex)
        {% highlight ruby %}
         df = df.filter(df.name.rlike('[A-Z]*ice$'))
        {% endhighlight %}

        - # Is In List - col.isin(*cols)
        {% highlight ruby %}
         df = df.filter(df.name.isin('Bob', 'Mike'))
        {% endhighlight %}

    - String Functions
        - # Substring - col.substr(startPos, length)
        {% highlight ruby %}
         df = df.withColumn('short_id', df.id.substr(0, 10))
        {% endhighlight %}

        - # Trim - F.trim(col)
        {% highlight ruby %}
         df = df.withColumn('name', F.trim(df.name))
        {% endhighlight %}

        {% highlight ruby %}
         # Left Pad - F.lpad(col, len, pad)
         # Right Pad - F.rpad(col, len, pad)
         df = df.withColumn('id', F.lpad('id', 4, '0'))
        {% endhighlight %}

        {% highlight ruby %}
         # Left Trim - F.ltrim(col)
         # Right Trim - F.rtrim(col)
         df = df.withColumn('id', F.ltrim('id'))
        {% endhighlight %}

        - # Concatenate - F.concat(*cols)
        {% highlight ruby %}
         df = df.withColumn('full_name', F.concat('fname', F.lit(' '), 'lname'))
        {% endhighlight %}

        - # Concatenate with Separator/Delimiter - F.concat_ws(*cols)
        {% highlight ruby %}
         df = df.withColumn('full_name', F.concat_ws('-', 'fname', 'lname'))
        {% endhighlight %}

        - # Regex Replace - F.regexp_replace(str, pattern, replacement)[source]
        {% highlight ruby %}
         df = df.withColumn('id', F.regexp_replace(id, '0F1(.*)', '1F1-$1'))
        {% endhighlight %}

        - # Regex Extract - F.regexp_extract(str, pattern, idx)
        {% highlight ruby %}
         df = df.withColumn('id', F.regexp_extract(id, '[0-9]*', 0))
        {% endhighlight %}

    - Number Operations
        - # Round - F.round(col, scale=0)
        {% highlight ruby %}
         df = df.withColumn('price', F.round('price', 0))
        {% endhighlight %}

        - # Floor - F.floor(col)
        {% highlight ruby %}
         df = df.withColumn('price', F.floor('price'))
        {% endhighlight %}

        - # Ceiling - F.ceil(col)
        {% highlight ruby %}
         df = df.withColumn('price', F.ceil('price'))
        {% endhighlight %}

    - Array Operations
        - # Column Array - F.array(*cols)
        {% highlight ruby %}
         df = df.withColumn('full_name', F.array('fname', 'lname'))
        {% endhighlight %}

        - # Empty Array - F.array(*cols)
        {% highlight ruby %}
         df = df.withColumn('empty_array_column', F.array([]))
        {% endhighlight %}

    - Aggregation Operations
        {% highlight ruby %}
         # Count - F.count()
         # Sum - F.sum(*cols)
         # Mean - F.mean(*cols)
         # Max - F.max(*cols)
         # Min - F.min(*cols)
         df = df.groupBy('gender').agg(F.max('age').alias('max_age_by_gender'))
        {% endhighlight %}

        {% highlight ruby %}
         # Collect Set - F.collect_set(col)
         # Collect List - F.collect_list(col)
         df = df.groupBy('age').agg(F.collect_set('name').alias('person_names'))
        {% endhighlight %}

    - Advanced Operations
        Repartitioning
        - # Repartition – df.repartition(num_output_partitions)
        {% highlight ruby %}
         df = df.repartition(1)
        {% endhighlight %}

        UDFs (User Defined Functions)
        - # Multiply each row's age column by two
        {% highlight ruby %}
         times_two_udf = F.udf(lambda x: x * 2)
         df = df.withColumn('age', times_two_udf(df.age))
        {% endhighlight %}

        - # Randomly choose a value to use as a row's name
        {% highlight ruby %}
         import random

         random_name_udf = F.udf(lambda: random.choice(['Bob', 'Tom', 'Amy', 'Jenna']))
         df = df.withColumn('name', random_name_udf())
        {% endhighlight %}