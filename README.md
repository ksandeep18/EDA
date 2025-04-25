
# YouTube Trending Videos - PySpark EDA

This project leverages **Apache Spark** (PySpark) to perform **Exploratory Data Analysis (EDA)** on the **YouTube Trending Videos dataset**. It analyzes trends across multiple countries to uncover insights about video popularity, user engagement, and trending patterns.

### Project Overview:
- **Dataset:** YouTube Trending Videos from Kaggle
- **Tools Used:** PySpark, Google Colab, Pandas, Matplotlib, Seaborn
- **Objective:** To analyze and extract valuable insights from the YouTube Trending Videos dataset using distributed computing with PySpark.

---

## 🎯 Project Goals:

1. Analyze the most popular video categories and countries.
2. Discover trends in likes, dislikes, and comments on trending videos.
3. Investigate how video title length, tags, and publishing time affect viewership.
4. Visualize the insights using graphs and charts.

---

## 💻 Setup and Installation:

### 1. **Environment Setup**:
   - Use **Google Colab** for running PySpark code.
   - Install PySpark using the following:
   ```python
   !pip install pyspark
   ```

### 2. **Mount Google Drive**:
   - Mount Google Drive to access the dataset from Kaggle:
   ```python
   from google.colab import drive
   drive.mount('/content/drive')
   ```

### 3. **Dataset**:
   - **Dataset Link:** [YouTube Trending Videos Dataset on Kaggle](https://www.kaggle.com/datasets/datasnaek/youtube-new)
   - Download and upload the dataset (CSV files like `USvideos.csv`) to Google Drive.

---

## 🔍 Analysis Questions:

The project explores various questions that help uncover trends in YouTube's video data:

1. **What are the most viewed videos in each country?**
2. **Which video categories get the most views on average?**
3. **What is the distribution of likes, dislikes, and comments on trending videos?**
4. **Which videos have the highest like-to-dislike ratios?**
5. **How long do videos stay trending?**
6. **Which countries have the longest trending durations?**
7. **Are there any common tags that frequently appear in trending videos?**
8. **Do longer titles tend to get more views?**

---

## 📊 Visualizations:
- **Matplotlib/Seaborn** was used to visualize key insights, including:
  - Bar charts for views by category
  - Histograms for like/dislike distributions
  - Correlation heatmaps between views, likes, and comments
  - Time series for trending durations and views over time

---

## 🛠️ Key Code Snippets:

### 1. **Setup and Load Data:**
```python
from pyspark.sql import SparkSession

spark = SparkSession.builder.appName("YouTubeEDA").getOrCreate()

df = spark.read.csv("/content/drive/MyDrive/youtube-new/USvideos.csv", header=True, inferSchema=True)
df.show(5)
```

### 2. **Top 5 Most Liked Videos:**
```python
df.orderBy("likes", ascending=False).select("title", "likes", "channel_title").show(5)
```

### 3. **Average Views by Category:**
```python
df.groupBy("category_id").avg("views").orderBy("avg(views)", ascending=False).show()
```

### 4. **Correlation Between Views and Likes/Comments:**
```python
df.select("views", "likes", "dislikes", "comment_count").toPandas().corr()
```

---

## 📝 Project Structure:
```
YouTube_EDA_PySpark/
│
├── YouTube_EDA_Colab_Notebook.ipynb  ← Main Jupyter notebook for analysis
├── README.md                         ← Project summary + insights
├── dataset/                          ← Kaggle CSVs 
└── visuals/                          ← Saved plots 
```

---

## 💡 Future Improvements:
- Integrate **more countries** for a global comparison.
- Use **machine learning** techniques to predict video success based on features.
- Implement **streaming data analysis** for real-time YouTube trends.

---

## 📣 Acknowledgements:
- **Dataset:** [YouTube Trending Dataset by Datasnaek on Kaggle](https://www.kaggle.com/datasets/datasnaek/youtube-new)
- **Libraries:** PySpark, Pandas, Matplotlib, Seaborn

---

