# Statistics
# Mini Project: From Data Collection to Statistical Insights

import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
from scipy import stats

# -----------------------------
# Step 1: Simulated Data Collection
# -----------------------------

np.random.seed(42)

# Satisfaction scores (1-10 scale)
satisfaction_scores = np.random.normal(loc=7.8, scale=1.5, size=200)

# Keep scores between 4 and 10
satisfaction_scores = np.clip(satisfaction_scores, 4, 10)

# UI completion times
old_ui_times = np.random.normal(loc=60, scale=8, size=100)
new_ui_times = np.random.normal(loc=45, scale=6, size=100)

# -----------------------------
# Step 2: Descriptive Statistics
# -----------------------------

mean_score = np.mean(satisfaction_scores)
median_score = np.median(satisfaction_scores)
mode_score = stats.mode(np.round(satisfaction_scores))
std_dev = np.std(satisfaction_scores)
data_range = (np.min(satisfaction_scores), np.max(satisfaction_scores))

print("Descriptive Statistics:")
print("Mean:", round(mean_score, 2))
print("Median:", round(median_score, 2))
print("Mode:", mode_score.mode[0])
print("Standard Deviation:", round(std_dev, 2))
print("Range:", data_range)

# -----------------------------
# Step 3: Inferential Statistics (t-test)
# -----------------------------

t_stat, p_value = stats.ttest_ind(old_ui_times, new_ui_times)

print("\nInferential Statistics:")
print("T-statistic:", round(t_stat, 3))
print("P-value:", round(p_value, 4))

if p_value < 0.05:
    print("Result: Statistically Significant Difference")
else:
    print("Result: No Significant Difference")

# -----------------------------
# Step 4: Visualization
# -----------------------------

# Histogram of Satisfaction
plt.hist(satisfaction_scores, bins=10)
plt.title("Histogram of User Satisfaction Scores")
plt.xlabel("Satisfaction Score")
plt.ylabel("Frequency")
plt.show()

# Boxplot of UI Completion Times
plt.boxplot([old_ui_times, new_ui_times], labels=["Old UI", "New UI"])
plt.title("Completion Time Comparison")
plt.ylabel("Time (seconds)")
plt.show()
