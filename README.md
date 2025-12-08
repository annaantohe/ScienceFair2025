# Fitbit Sleep, Activity, and Heart Rate – Science Fair 2025

## 👋 Project Overview

This project uses **real Fitbit data** to explore how **sleep**, **daily activity**, and **heart rate** are connected.

All of the work is done in Jupyter notebooks. Each notebook focuses on one big question (hypothesis). The goal is to think like a scientist, not to “prove” anything, but to **test ideas carefully** and explain what the data actually shows.

The data comes from adults who wore Fitbits over about **two months** in 2016.

---

## 📂 Project Structure

Main notebooks in this repo:

1. `EDA.ipynb`
   *Exploratory Data Analysis (getting to know the data)*

2. `Good_Sleep_and_Next_Day_RHR.ipynb`
   *Does sleeping more lower your resting heart rate the next day?*

3. `Very_Active_Minutes_Have_Better_Sleep.ipynb`
   *Do people who exercise more each week sleep longer?*

4. `Weekend_vs_Weekday_Behavior.ipynb`
   *Do people sleep more and move less on weekends than on weekdays?*

There is also a `data/` folder that holds the Fitbit CSV files and a `visuals/` folder for saved graphs.

---

## 📊 Data Used

The project mainly uses these Fitbit exports:

* **Activity data**
  Daily steps, distances, and minutes in different activity levels (very active, fairly active, lightly active, sedentary).

* **Minute-by-minute sleep data**
  A row for each minute a person is asleep. This is turned into **total minutes asleep per night** and **hours of sleep per night**.

* **Heart-rate data** (for some people)
  Heart rate recorded every few seconds. This is used to estimate **resting heart rate**.

Not every person has every type of data. That’s important for how strong the results are.

---

## 📘 Notebook Summaries

### 1️⃣ `EDA.ipynb` – Getting to Know the Fitbit Data

This notebook:

* Lists all the Fitbit files and what they contain.
* Counts:

  * how many **rows** (measurements) are in each file
  * how many **participants** appear in each dataset
* Shows how many people have:

  * **activity only**
  * **sleep only**
  * **heart rate only**
  * or **all three** (activity + sleep + heart rate)
* Points out data problems, like:

  * Missing daily sleep file for the first month
  * Much smaller heart-rate group (only about 15 people)
  * Uneven sample sizes between files

**Key takeaway:**
We have **lots of activity data**, **pretty good sleep data**, and **limited heart-rate data**.
Only a small group has **all three**, so any results using heart rate must be treated carefully.

---

### 2️⃣ `Good_Sleep_and_Next_Day_RHR.ipynb`

*Do people who sleep longer have lower resting heart rate the next day?*

**Question:**

> If someone sleeps more hours in a night, do they have a **lower resting heart rate (RHR)** the next day?

What the notebook does:

* Uses sleep data to split nights into three groups:

  * **< 6 hours of sleep**
  * **6–7 hours of sleep**
  * **≥ 7 hours of sleep**
* Uses heart-rate data to **approximate resting heart rate** by taking a low part of the heart-rate values (like the 15th percentile) for each day.
* Compares the **average next-day RHR** across the three sleep groups.
* Runs a **t-test** between:

  * short sleep (< 6 hours) and
  * long sleep (≥ 7 hours)
* Makes boxplots and tables to show how similar the groups are.

**Result:**

* The average resting heart rates of the three sleep groups are **very close**.
* The t-test p-value is **much higher than 0.05**, which means the small differences we see are likely due to **random chance**.

**Conclusion in simple terms:**
In this dataset, **sleeping longer did *not* clearly lower next-day resting heart rate**. The data wasn’t strong enough to support the original hypothesis.

---

### 3️⃣ `Very_Active_Minutes_Have_Better_Sleep.ipynb`

*Do people who exercise more sleep longer?*

**Question:**

> Do people who get at least **150 minutes of “very active” exercise per week** sleep more hours per night than people who don’t?

What the notebook does:

* Combines Fitbit data across two months.
* For each **person-week**, it calculates:

  * **WeeklyActiveMin** = total “VeryActiveMinutes” that week
  * **SleepHours** = average nightly sleep (hours) for that week
* Creates two groups:

  * **“≥150 min/week”** – meets the recommended very active minutes
  * **“<150 min/week”** – does not meet that level
* Compares the **average sleep hours** between the two groups.
* Runs an independent **t-test** to see if the difference is statistically significant.
* Also draws a scatterplot with a regression line to see if more very active minutes are related to more sleep.

**Result:**

* **<150 min/week group:**

  * ~**7.68 hours** of sleep per night
* **≥150 min/week group:**

  * ~**7.09 hours** of sleep per night

So the “less active” weeks actually slept **a bit more**, but the difference is small.

* The t-test gives a **p-value ≈ 0.18**, which is **not** below 0.05.

**Conclusion in simple terms:**
This dataset **does not show** that people who reach 150 very active minutes per week sleep more.
The small differences we see could easily be **random**, so the hypothesis is **not supported** by this data.

---

### 4️⃣ `Weekend_vs_Weekday_Behavior.ipynb`

*Do people sleep more and move less on weekends?*

**Question:**

> On weekends, do people **sleep longer** and **move less** than on weekdays?

What the notebook does:

* Turns minute-by-minute sleep data into **daily** sleep:

  * **TotalMinutesAsleep** and **SleepHours** for each person and day.
* Keeps daily activity data:

  * **VeryActiveMinutes**
  * **TotalSteps**
* Merges sleep and activity into one table with:

  * **Id**, **Date**, **SleepHours**, **VeryActiveMinutes**, **TotalSteps**
* Adds:

  * **DayOfWeek** (Monday–Sunday)
  * **IsWeekend** (True for Saturday/Sunday, False otherwise)
* Compares **average SleepHours** and **VeryActiveMinutes** for:

  * **Weekdays (Mon–Fri)**
  * **Weekends (Sat–Sun)**
* Runs t-tests to check if differences are statistically significant.
* Builds graphs to show:

  * Weekend vs weekday **sleep hours**
  * Weekend vs weekday **very active minutes**

**Result:**

* **Sleep:**

  * Weekdays: about **7.7 hours** of sleep per night
  * Weekends: about **8.6 hours** of sleep per night
    → Roughly **1 extra hour of sleep** on weekends
    → p-value ≈ **0.003**, which **is** below 0.05 → **statistically significant**

* **Very Active Minutes:**

  * Weekdays: about **23 minutes**
  * Weekends: about **22 minutes**
    → Almost no difference
    → p-value ≈ **0.81**, **not** significant

**Conclusion in simple terms:**
The data **supports** the sleep part of the hypothesis:

> People really do **sleep more on weekends**.

But it **does not** support the activity part:

> People are **not clearly less active** on weekends. Their very active minutes stay about the same.

---

## 🧠 What This Project Shows Overall

Across all notebooks:

* Real data is **messy**.
  Some people have missing days, some forget to wear their devices, and heart-rate data is limited.

* Not every good idea is confirmed.
  Two main hypotheses (better sleep → lower resting HR, and more exercise → more sleep) **were not supported** by this dataset.

* One pattern did show up clearly.
  People **sleep more on weekends**, but their activity time doesn’t change much.

* Statistics matter.
  Just seeing different averages isn’t enough.
  We use **p-values** and **t-tests** to decide if differences are likely real or just random noise.

---

## 🧪 How to Run the Notebooks

1. Create and activate a Python virtual environment.

2. Install dependencies (example):

   ```bash
   pip install -r requirements.txt
   # or, if no file:
   pip install pandas numpy matplotlib seaborn scipy jupyterlab
   ```

3. Make sure the Fitbit CSV files are in the `data/` folder with the same paths used in the notebooks.

4. Start JupyterLab:

   ```bash
   jupyter lab
   ```

5. Open the notebooks in this order for the story to make sense:

   1. `EDA.ipynb`
   2. `Good_Sleep_and_Next_Day_RHR.ipynb`
   3. `Very_Active_Minutes_Have_Better_Sleep.ipynb`
   4. `Weekend_vs_Weekday_Behavior.ipynb`

---

## ✅ Plain-English Summary

This project is a science-fair-style investigation using Fitbit data. It asks:

* Does more sleep lower resting heart rate? → **Not shown here**
* Does more weekly intense exercise lead to more sleep? → **Not shown here**
* Do people sleep more on weekends? → **Yes, by about 1 hour**

Overall, the project shows how to:

* work with real-world data,
* build clear hypotheses,
* run basic statistics,
* and explain results honestly, even when the data does **not** match the original guess.
