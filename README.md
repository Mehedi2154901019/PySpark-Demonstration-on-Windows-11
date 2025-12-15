# PySpark Demonstration on Windows 11

This project demonstrates how to install, configure, and run PySpark locally on Windows 11 using Java JDK 17, Apache Spark 3.5.7, and Python 3.10 inside a Conda virtual environment.

---

## Author
Md Mehedi Hassan  
ID: 25542607009  

---

## Prerequisites

- Windows 11  
- Java Development Kit (JDK) 17  
- Python 3.10.x  
- Anaconda / Miniconda  
- Apache Spark 3.5.7  
- Hadoop winutils for Windows compatibility  

> Note: Java, Spark, and Hadoop are system-level dependencies and are not installed via pip.

---

## Java Setup

1. Install JDK 17 (Windows x64)
2. Install location:
   ```
   C:\jdk17
   ```
3. Set system environment variables:
   - JAVA_HOME = C:\jdk17
   - Add to Path:
     ```
     C:\jdk17\bin
     ```

Verify installation:
```bash
java --version
```

---

## Apache Spark Setup

1. Download Apache Spark version **3.5.7**
2. Choose package type: **Apache Hadoop 3.3 and later**
3. Extract Spark to a local directory (for example: `C:\spark`)

Verify later using:
```bash
pyspark --version
```

---

## Hadoop Windows Fix (winutils)

1. Create directories:
   ```
   C:\hadoop\bin
   ```
2. Download the following files and place them inside `C:\hadoop\bin`:
   - winutils.exe
   - hadoop.dll

3. Set system environment variables:
   - HADOOP_HOME = C:\hadoop
   - Add to Path:
     ```
     C:\hadoop\bin
     ```

---

## Python Environment Setup

Create a Conda virtual environment:
```bash
conda create -n pyspark310 python=3.10
```

Activate the environment:
```bash
conda activate pyspark310
```

Install Python dependencies:
```bash
pip install -r requirements.txt
```

Verify Python version:
```bash
python --version
```

---

## requirements.txt

```
pyspark==3.5.7
findspark
```

---

## Running PySpark

Example Spark session initialization:

```python
from pyspark.sql import SparkSession

spark = SparkSession.builder \
    .appName("PySpark Demo") \
    .master("local[*]") \
    .getOrCreate()
```

- `local[*]` uses all available CPU cores
- Spark Web UI: http://localhost:4040

---

## Features Demonstrated

### RDD Operations
- count()
- collect()
- first()
- take()
- map()
- filter()
- sortBy()

### DataFrame Operations
- Reading text and CSV files
- Schema inference (inferSchema)
- Column selection
- Filtering
- Sorting
- Distinct values
- Creating new columns (withColumn)
- SQL queries using spark.sql()

---

## Spark SQL Example

```python
spark.sql("""
SELECT gender, AVG(attendance) AS avg_attendance
FROM students
GROUP BY gender
""").show()
```

---

## Stopping Spark

Always stop the Spark session after use:

```python
spark.stop()
```

---

## Notes

- Python 3.10.x is required for compatibility with Spark 3.5.7
- Activate the pyspark310 environment before running any Spark code
- Ensure no conflicting Java or Hadoop paths exist in system environment variables

---

## License

This project is for educational and academic purposes only.
