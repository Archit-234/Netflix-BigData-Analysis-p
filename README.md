# Netflix-BigData-Analysis-p
Big Data analytics project using Apache Spark on Netflix dataset
from google.colab import files
files.upload()

import zipfile

with zipfile.ZipFile("archive.zip", 'r') as zip_ref:
    zip_ref.extractall("data")

print("Dataset Extracted Successfully")
from pyspark.sql import SparkSession

spark = SparkSession.builder \
    .appName("Netflix Big Data Project") \
    .getOrCreate()
data = spark.read.csv(
    "data/netflix_titles.csv",
    header=True,
    inferSchema=True
)

data.show(5)
print("Total Rows:", data.count())
data.printSchema()
data.groupBy("type").count().show()
data.groupBy("country").count().orderBy("count", ascending=False).show()
