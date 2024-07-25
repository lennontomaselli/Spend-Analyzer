# Spend-Analyzer
This script provides a detailed overview of spending patterns over time, allowing you to see how spending varies by category and year.
import pandas as pd
import matplotlib.pyplot as plt

# Define a function to analyze spending
def analyze_spending(data):
    # Convert data into a DataFrame
    df = pd.DataFrame(data)
    
    # Convert 'Date' column to datetime format
    df['Date'] = pd.to_datetime(df['Date'])
    
    # Extract year from the 'Date' column
    df['Year'] = df['Date'].dt.year
    
    # Calculate total spending by year and category
    spending_by_year = df.groupby(['Year', 'Category'])['Amount'].sum().unstack().fillna(0)
    total_spending_by_year = spending_by_year.sum(axis=1)
    
    # Print results
    print("Total Spending by Year:")
    print(total_spending_by_year)
    
    print("\nSpending by Category and Year:")
    print(spending_by_year)
    
    # Plot spending trends
    spending_by_year.plot(kind='bar', stacked=True, figsize=(10, 6))
    plt.title('Spending by Category Over Time')
    plt.xlabel('Year')
    plt.ylabel('Amount Spent ($)')
    plt.legend(title='Category')
    plt.tight_layout()
    plt.show()
    
    return total_spending_by_year, spending_by_year

# Sample spending data
spending_data = [
    {"Date": "2020-01-15", "Category": "Health Apps", "Amount": 150.00},
    {"Date": "2020-03-22", "Category": "Mindfulness Products", "Amount": 200.00},
    {"Date": "2021-06-10", "Category": "Wearable Technology", "Amount": 300.00},
    {"Date": "2021-09-05", "Category": "Virtual Consultations", "Amount": 250.00},
    {"Date": "2022-02-14", "Category": "Meditation Classes", "Amount": 100.00},
    {"Date": "2023-07-19", "Category": "Health Apps", "Amount": 175.00},
    {"Date": "2024-05-30", "Category": "Wearable Technology", "Amount": 320.00},
    {"Date": "2024-11-23", "Category": "Virtual Consultations", "Amount": 270.00}
]

# Analyze the sample data
total_spending_by_year, spending_by_category_and_year = analyze_spending(spending_data)
