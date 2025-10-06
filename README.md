# Overview

Welcome to my analysis of the data job market, focusing on data analyst roles. This project was created out of a desire to navigate and understand the job market more effectively. It delves into the top-paying and in-demand skills to help find optimal job opportunities for data analysts.

The data sourced from [Luke Barousse's Python Course](https://lukebarousse.com/python) which provides a foundation for my analysis, containing detailed information on job titles, salaries, locations, and essential skills. Through a series of Python scripts, I explore key questions such as the most demanded skills, salary trends, and the intersection of demand and salary in data analytics.

# The Questions

Below are the questions I want to answer in my project:

1. What are the skills most in demand for the top 3 most popular data roles?
2. How are in-demand skills trending for Data Analysts?
3. How well do jobs and skills pay for Data Analysts?
4. What are the optimal skills for data analysts to learn? (High Demand AND High Paying) 

# Tools I Used

For my deep dive into the data analyst job market, I harnessed the power of several key tools:

- **Python:** The backbone of my analysis, allowing me to analyze the data and find critical insights.I also used the following Python libraries:
    - **Pandas Library:** This was used to analyze the data. 
    - **Matplotlib Library:** I visualized the data.
    - **Seaborn Library:** Helped me create more advanced visuals. 
- **Jupyter Notebooks:** The tool I used to run my Python scripts which let me easily include my notes and analysis.
- **Visual Studio Code:** My go-to for executing my Python scripts.
- **Git & GitHub:** Essential for version control and sharing my Python code and analysis, ensuring collaboration and project tracking.

# Data Preparation and Cleanup

This section outlines the steps taken to prepare the data for analysis, ensuring accuracy and usability.

## Import & Clean Up Data

I start by importing necessary libraries and loading the dataset, followed by initial data cleaning tasks to ensure data quality.

```python
# Importing Libraries
import ast
import pandas as pd
import seaborn as sns
from datasets import load_dataset
import matplotlib.pyplot as plt  

# Loading Data
dataset = load_dataset('lukebarousse/data_jobs')
df = dataset['train'].to_pandas()

# Data Cleanup
df['job_posted_date'] = pd.to_datetime(df['job_posted_date'])
df['job_skills'] = df['job_skills'].apply(lambda x: ast.literal_eval(x) if pd.notna(x) else x)
```

## Filter India Jobs

To focus my analysis on the Indian job market, I apply filters to the dataset, narrowing down to roles based in the United States.

```python
df_US = df[df['job_country'] == 'India']

```

# The Analysis

Each Jupyter notebook for this project aimed at investigating specific aspects of the data job market. Here’s how I approached each question:

## 1. What are the most demanded skills for the top 3 most popular data roles?

To find the most demanded skills for the top 3 most popular data roles. I filtered out those positions by which ones were the most popular, and got the top 5 skills for these top 3 roles. This query highlights the most popular job titles and their top skills, showing which skills I should pay attention to depending on the role I'm targeting. 

View my notebook with detailed steps here: [2_skills_demand](3_Project\2_skills_demand.ipynb)

### Visualize Data

```python
fig, ax = plt.subplots(len(job_titles), 1)


for i, job_title in enumerate(job_titles):
    df_plot = df_skills_perc[df_skills_perc['job_title_short'] == job_title].head(5)[::-1]
    sns.barplot(data=df_plot, x='skill_percent', y='job_skills', ax=ax[i], hue='skill_count', palette='dark:b_r')

plt.show()
```

# Results

![Visualization of Top Skills For Job Roles in India](3_Project\Images\skill_demand.png)


# Insights 

## 📊 Insights from Job Posting Skill Analysis (India)

This analysis highlights the **likelihood of specific skills being requested** across three major data roles in India: **Data Analyst, Data Engineer, and Data Scientist**.  
The findings provide a clear view of how skill demands shift depending on the role.

---

<details>
<summary>🔑 Cross-role Trends</summary>

- **SQL + Python are universal**: Both appear across all roles, but their weight changes:  
  - Analysts → SQL-heavy  
  - Engineers → SQL + Python balanced  
  - Scientists → Python-dominant  
- **Visualization tools** (Excel, Tableau, Power BI) are **analyst-centric**, rarely emphasized for engineers or scientists.  
- **Cloud & big data tools** (AWS, Azure, Spark) are **engineer-centric**, reflecting the infrastructure-heavy nature of the role.  
- **Statistical tools** (R) remain relevant only for scientists, showing their focus on modeling and research-driven analysis.  

</details>

---

<details>
<summary>📌 Role-specific Insights</summary>

**1. Data Analyst**  
- SQL (52%) is the backbone skill, with Python (36%) rising as a secondary requirement.  
- Excel (35%) remains surprisingly strong, showing that traditional tools still matter.  
- Visualization (Tableau 27%, Power BI 21%) is a **key differentiator** for analysts.  

**2. Data Engineer**  
- SQL (68%) and Python (61%) are nearly universal requirements.  
- Spark (38%) and cloud platforms (AWS 37%, Azure 36%) highlight the **pipeline + infrastructure focus**.  
- Engineers are expected to **build and scale**, not just analyze.  

**3. Data Scientist**  
- Python (70%) is the undisputed core skill — higher than for any other role.  
- SQL (48%) remains important but secondary.  
- R (33%) shows that **statistical modeling** still has a niche.  
- Cloud (AWS 19%) and visualization (Tableau 18%) are **supporting skills**, not primary.  

</details>

---

<details>
<summary>🚀 Strategic Takeaways</summary>

- **Career progression path:**  
  Analyst → Engineer → Scientist shows a natural shift from **querying & visualization → infrastructure & scaling → modeling & advanced analytics**.  

- **For career pivots:**  
  - Analysts moving to engineering should **add Spark + cloud**.  
  - Engineers moving to science should **deepen Python + statistics (R, ML libraries)**.  

- **For employers:**  
  Job descriptions should be sharper — while overlap exists, the dataset shows **clear skill clusters** that can guide hiring.  

</details>

---

<details>
<summary>🧭 Why This Matters</summary>

For learners and professionals, this dataset provides a **roadmap for skill-building**:  
- Start with **SQL + Python** as the foundation.  
- Layer on **visualization tools** if targeting analyst roles.  
- Add **cloud + big data tools** for engineering.  
- Deepen **statistics + modeling** for data science.  

</details>

---

<details>
<summary>✨ Personal Relevance </summary>

For my own journey, this validates my current focus on **SQL + Python** for analytics, while also highlighting the importance of visualization tools (Power BI/Tableau) for my data professional journey. 
As I expand into engineering and data science, **Spark, cloud, and advanced modeling** will become the next milestones.  

</details>


## 2.How are in-demand skills trending for Data Analysts?

To find how skills are trending in 2023 for Data Analysts, I filtered data analyst positions and grouped the skills by the month of the job postings. This got me the top 5 skills of data analysts by month, showing how popular skills were throughout 2023.

### Visualize Data

```python

from matplotlib.ticker import PercentFormatter

df_plot = df_DA_I_percent.iloc[:, :5]
sns.lineplot(data=df_plot, dashes=False, legend='full', palette='tab10')

plt.gca().yaxis.set_major_formatter(PercentFormatter(decimals=0))

plt.show()

```

### Results

![Trending Top Skills for Data Analysts in India](3_Project\Images\skill_trends.png)  
*Line Graph visualizing the trending top skills for data analysts in India in 2023.*


This visualization tracks the **percentage of job postings requiring specific skills** for Data Analyst roles in India across 2023.  
Skills analyzed: **SQL, Python, Excel, Tableau, Power BI**.

---

<details>
<summary>🔑 Key Observations</summary>

- **SQL dominates** throughout the year, peaking in May (~70%), confirming its role as the backbone skill.  
- **Python demand is steady** (30–45%), with a mid-year peak in June, reflecting its growing importance for automation and scripting.  
- **Excel shows volatility**, with a major spike in June (~60%), proving it remains indispensable for business-facing analysis.  
- **Tableau demand rises mid-year**, peaking in July (~45%), showing visualization tools gain traction seasonally.  
- **Power BI consistently trails** (20–30%), suggesting it’s valued but less frequently required compared to Tableau.  

</details>

---

<details>
<summary>📌 Deeper Insights</summary>

- **SQL as a constant**: Employers consistently prioritize SQL, making it the safest foundational skill.  
- **Python’s upward momentum**: Its mid-year peak signals a shift toward analysts who can handle larger datasets and automation.  
- **Excel’s resilience**: Despite newer tools, Excel’s June surge shows it’s still central to many workflows.  
- **Visualization split**: Tableau outpaces Power BI in demand, but both remain secondary to SQL/Python.  
- **Seasonal hiring patterns**: Peaks in SQL, Excel, and Tableau around mid-year may align with hiring cycles or project launches.  

</details>

---

<details>
<summary>🚀 Strategic Takeaways</summary>

- **For learners**:  
  - Start with **SQL + Excel** for quick entry.  
  - Add **Python** to future-proof your profile.  
  - Layer on **Tableau/Power BI** for visualization credibility.  

- **For career pivots**:  
  - Analysts aiming for advanced roles should strengthen **Python + visualization**.  
  - Those targeting engineering/data science should expand into **cloud + big data tools**.  

- **For employers**:  
  - The steady rise in postings highlights a competitive market.  
  - Clearer job descriptions can help attract candidates with the right skill mix.  

</details>

---

<details>
<summary>✨ Personal Relevance (Optional)</summary>

For my own journey, this trend validates my focus on **SQL + Python** as the backbone of my analytics dashboard project.  
It also highlights why I’m adding **Power BI/Tableau** for visualization — even if demand is lower, it differentiates my profile.   

</details>