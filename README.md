# Advancement-Donations-data-handling
# introduction 
🎓📊 Data-Driven Insights into Advancement &amp; Donations 📈💡 I recently worked on a data analysis project using Python to explore patterns in advancement, giving, and donation behavior. Leveraging libraries like pandas, matplotlib, and seaborn, I visualized key insights to better understand donor trends and institutional support. 

#code
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

# Load your CSV file
df = pd read_csv("advancement_donations_and_giving_demo.csv")
df['Gift Date'] = pd.to_datetime(df['Gift Date'], errors='coerce')

#1.Optional: Set seaborn style
sns.set(style="whitegrid")
plt.figure(figsize=(12, 6))
college_totals = df.groupby('College')['Gift Amount'].sum().sort_values(ascending=False)
sns.barplot(x=college_totals.values, y=college_totals.index, palette="viridis")
plt.title('Total Gift Amount by College')
plt.xlabel('Total Gift Amount')
plt.tight_layout()
plt.show()

#2.Donation Count by State bar graph
plt.figure(figsize=(10, 6))
state_counts = df['State'].value_counts()
sns.barplot(x=state_counts.index, y=state_counts.values, palette="magma")
plt.title('Number of Donations by State')
plt.ylabel('Number of Donations')
plt.xlabel('State')
plt.tight_layout()
plt.show()

#3.Monthly Donation Trends line graph
df['Month'] = df['Gift Date'].dt.to_period('M')
monthly_totals = df.groupby('Month')['Gift Amount'].sum()

plt.figure(figsize=(14, 6))
monthly_totals.plot(kind='line', marker='o', color='teal')
plt.title('Monthly Donation Trends')
plt.ylabel('Total Gift Amount')
plt.xlabel('Month')
plt.xticks(rotation=45)
plt.tight_layout()
plt.show()

#4.Average Donation by Major (Top 10) pie chart

major_avg = df.groupby('Major')['Gift Amount'].mean().sort_values(ascending=False).head(10)
plt.figure(figsize=(8, 8))
plt.pie(
    major_avg.values,
    labels=major_avg.index,
    autopct='%1.1f%%',
    startangle=140,
    colors=plt.cm.Paired.colors
)
plt.title('Top 10 Majors by Average Donation')
plt.axis('equal')  # Equal aspect ratio ensures that pie is drawn as a circle.
plt.tight_layout()
plt.show()

#5.Top 10 Cities by Total Gift Amount heat map

city_totals = df.groupby('City')['Gift Amount'].sum().sort_values(ascending=False).head(10)
city_df = city_totals.to_frame().sort_values('Gift Amount', ascending=True)  # reverse for better gradient
plt.figure(figsize=(10, 6))
sns.heatmap(city_df, annot=True, fmt=".0f", cmap="YlGnBu", linewidths=0.5, cbar=True)

plt.title("Top 10 Cities by Total Gift Amount (Heatmap Style)")
plt.xlabel("Donation")
plt.ylabel("City")
plt.tight_layout()
plt.show()
# end

