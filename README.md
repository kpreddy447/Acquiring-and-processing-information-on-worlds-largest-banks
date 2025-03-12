# Acquiring and Processing Information on the World's Largest Banks  

## 📌 Project Overview  
This project focuses on extracting, transforming, and analyzing data on the world's largest banks. Using **web scraping**, **ETL (Extract, Transform, Load) operations**, and **SQL database storage**, this project automates the retrieval of bank market capitalization data and enhances it with currency conversions.  

The processed data is saved in both **CSV format** and a **SQLite database**, enabling further analysis and insights.  

---

## 🚀 Features  
- **Web Scraping**: Extracts financial data from a Wikipedia archive.  
- **ETL Pipeline**: Automates data extraction, transformation, and loading.  
- **Data Transformation**: Converts market capitalization to multiple currencies.  
- **Database Storage**: Saves structured data into an SQLite database.  
- **Logging Mechanism**: Tracks the progress of each ETL step.  

---

## 📂 Project Structure  
```
📦 Acquiring-and-processing-information-on-worlds-largest-banks
│── 📜 .gitignore
│── 📜 README.md
│── 📜 Bank_ETL_webscraping.ipynb  # Jupyter notebook with ETL code  
│── 📜 Banks.db                     # SQLite database  
│── 📜 Largest_banks_data.csv        # Processed data  
│── 📜 code_log.txt                  # Log file tracking ETL progress  
```

---

## 🛠️ Technologies Used  
- **Python**: Core programming language  
- **BeautifulSoup**: Web scraping  
- **Pandas**: Data manipulation  
- **NumPy**: Numerical calculations  
- **SQLite**: Database storage  
- **Logging**: Process tracking  

---

## 📊 Data Pipeline Workflow  
1. **Extract**  
   - Scrapes banking data from a **Wikipedia archive**.  
   - Parses relevant details (Bank Name, Market Cap in USD).  

2. **Transform**  
   - Reads exchange rates from a **CSV file**.  
   - Converts Market Cap from **USD → GBP, INR, EUR**.  

3. **Load**  
   - Saves final dataset to **CSV format**.  
   - Stores structured data into an **SQLite database**.  

---

## 📌 Usage  
### 1️⃣ Clone the Repository  
```bash
git clone https://github.com/kpreddy447/Acquiring-and-processing-information-on-worlds-largest-banks.git
cd Acquiring-and-processing-information-on-worlds-largest-banks
```
### 2️⃣ Install Dependencies  
Ensure you have **Python 3.x** installed, then run:  
```bash
pip install requests beautifulsoup4 pandas numpy sqlite3
```
### 3️⃣ Run the ETL Process  
Execute the script in a Jupyter Notebook or Python environment:  
```python
# Import required functions
from Bank_ETL_webscraping import extract, transform, load_to_csv, load_to_db, run_query

# Define parameters
url = "https://web.archive.org/web/20230908091635/https://en.wikipedia.org/wiki/List_of_largest_banks"
csv_path = "exchange_rate.csv"
db_name = "Banks.db"
table_name = "Largest_banks"

# Run ETL
df = extract(url, pd.DataFrame(columns=["Name", "MC_USD_Billion"]))
df_transformed = transform(df, csv_path)
load_to_csv(df_transformed, "Largest_banks_data.csv")

# Load into Database
connection = sqlite3.connect(db_name)
load_to_db(df_transformed, connection, table_name)

# Run Query
run_query("SELECT * FROM Largest_banks", connection)
connection.close()
```

---

## 📈 Sample Output  
### Extracted Data:  
| Name                                      | MC_USD_Billion |
|-------------------------------------------|---------------|
| JPMorgan Chase                            | 432.92        |
| Bank of America                           | 231.52        |
| Industrial and Commercial Bank of China   | 194.56        |
| Agricultural Bank of China                | 160.68        |

### Transformed Data (After Currency Conversion):  
| Name                                      | MC_USD_Billion | MC_GBP_Billion | MC_INR_Billion | MC_EUR_Billion |
|-------------------------------------------|---------------|---------------|---------------|---------------|
| JPMorgan Chase                            | 432.92        | 346.34        | 35910.71      | 402.62        |
| Bank of America                           | 231.52        | 185.22        | 19204.58      | 215.31        |

---

## 📝 Logs  
The project tracks progress through a **log file** (`code_log.txt`), which records each step of the ETL process, such as:  
```plaintext
2025-03-11 16:00:05 : Preliminaries complete. Initiating ETL process  
2025-03-11 16:00:06 : Data extraction complete. Initiating Transformation process  
2025-03-11 16:00:07 : Data transformation complete. Initiating Loading process  
2025-03-11 16:00:07 : Data saved to CSV file  
2025-03-11 16:00:07 : SQL Connection initiated  
2025-03-11 16:00:07 : Process Complete  
```

---

## 📌 Future Enhancements  
🔹 Automate exchange rate updates via an API (e.g., Open Exchange Rates).  
🔹 Deploy as a **streaming pipeline** for real-time banking data updates.  
🔹 Implement a **dashboard** for interactive data visualization.  

---

## 🤝 Contributing  
Contributions are welcome! Feel free to **fork** this repo, create a new branch, and submit a **pull request**.  
