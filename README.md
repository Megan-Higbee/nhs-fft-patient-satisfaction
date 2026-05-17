# NHS FFT Patient Satisfaction Insights
This project analyses the NHS Friends and Family Test (FFT) data for February 2026, performing exploratory data analysis to uncover patient satisfaction insights at both a national level and through a focused deep dive into Medway NHS Foundation Trust. Key skills demonstrated include Python, SQL (MySQL), and Tableau Public. The project was bukt to reflect a genuine interest in healthcare data analysis and to simulate the kind of analytical work performed by a data analyst embedded within an NHS organisation. 

## 🔗 Dashboard Links

- [National NHS Patient Satisfaction Dashboard](https://public.tableau.com/views/NHSPatientSatisfactionDashboard-February2026/National?:language=en-US&:sid=&:redirect=auth&:display_count=n&:origin=viz_share_link)
- [Medway NHS Foundation Trust Deep Dive](https://public.tableau.com/views/MedwayNHSFoundationTrustPatientSatisfactionDashboard-February2026/Medway?:language=en-US&:sid=&:redirect=auth&:display_count=n&:origin=viz_share_link)

## 📊 Data Source

Data sourced from the **NHS England Friends and Family Test (FFT)** monthly publications.

- **Coverage:** February 2026
- **Care settings:** A&E, Inpatient, Outpatient, Maternity (4 touch-points), Mental Health
- **Licence:** Open Government Licence v3.0
- **Source:** [NHS England FFT Data](https://www.england.nhs.uk/fft/friends-and-family-test-data/)

> Note: The FFT cannot be used to directly compare providers due to variation in data collection methods and local populations. Findings should be interpreted with this caveat in mind.

## 🛠️ Tools & Libraries

**Python Libraries:**
- **Pandas** — data cleaning, manipulation and analysis
- **NumPy** — conditional category assignments (busyness tiers)
- **openpyxl** — reading .xlsm Excel files
- **python-dotenv** — secure credential management
- **SQLAlchemy** — connecting Python to MySQL
- **mysql-connector-python** — MySQL database driver

**Database:**
- **MySQL** — SQL queries and data analysis

**Visualisation:**
- **Tableau Public** — interactive dashboard creation

## 📁 Project Structure

| Stage | Description |
|---|---|
| Stage 1 | Downloaded real NHS FFT data from NHS England, explored file structure and made key analytical decisions |
| Stage 2 | Built a reusable Python cleaning pipeline producing a single structured DataFrame across 8 departments |
| Stage 3 | Exploratory analysis answering 5 analytical questions including department performance, Trust rankings and a Medway deep dive |
| Stage 4 | SQL analysis in MySQL using subqueries, window functions and CASE WHEN binning |
| Stage 5/6 | Exported summary data from Python and built two interactive Tableau Public dashboards |
| Stage 7 | Project documentation and GitHub README |

## 🔍 Key Findings

1. **Department Performance** — Outpatient and Inpatient scored highest (95.3% and 94.9%), while A&E scored lowest at 79.3% — significantly below the national average of 91%. Maternity satisfaction increases across the journey, from Antenatal (88.9%) to Postnatal Community (94.6%). Mental Health scored second lowest at 88.2%.

2. **Trust Performance** — Top performing Trusts were predominantly smaller district general hospitals in less urban settings. The bottom 10 was dominated by larger urban Trusts, with The Princess Alexandra Hospital NHS Trust a recurring underperformer appearing in both the bottom 10 and the flagging analysis. Overall scores ranged from 77.6% to 98.9%, suggesting NHS satisfaction is generally high but meaningful variation exists.

3. **Low Response Flagging** — 122 rows (11.7%) were flagged for insufficient survey responses. Three NHS acute Trusts — Royal United Hospitals Bath, Shrewsbury and Telford, and Somerset — had over 50% of their departments flagged, indicating systemic survey collection issues. Royal United Hospitals Bath appeared in the top 10 performers despite this, meaning their satisfaction score should be treated with caution.

4. **Medway NHS Foundation Trust** — Ranked 60th out of 114 Trusts nationally. Strongest department was Maternity - Antenatal (100%, n=82). Weakest was A&E at 74.8%, approximately 4 percentage points below the national A&E average. No Mental Health data was available. Insufficient responses were recorded for Maternity - Postnatal Community.

5. **Busyness vs Satisfaction** — A weak negative correlation (-0.10) was found between Total Eligible patients and Percentage Positive, suggesting volume alone is not a reliable predictor of patient satisfaction.

6. **SQL Analysis** — Trusts were grouped into four busyness tiers based on Total Eligible patients (Low <1,000, Medium 1,000-5,000, High 5,000-20,000, Very High >20,000). Low volume services scored highest (94.9%) while High volume services scored lowest (88.0%). 115 out of 314 Trusts (36.6%) scored below the national average of 91%. A window function ranking analysis revealed each Trust's performance relative to similarly sized peers, providing more actionable benchmarking than a simple national comparison.

## ⚠️ Limitations

- **Provider Comparability** — NHS England explicitly states that FFT data cannot be used to directly compare providers due to flexibility in data collection methods and variation in local populations. Findings should be interpreted with this caveat in mind.

- **Single Month of Data** — Analysis covers February 2026 only. This is a snapshot rather than a trend and findings may not be representative of typical performance. Seasonal variation, staffing changes or local events could influence results.

- **Mode of Collection** — Data collection method (SMS, paper, online etc.) varies between Trusts and departments and was excluded from analysis due to inconsistency across files. Different collection methods may introduce response bias and could partially explain satisfaction differences between departments.

- **Total Eligible Gap in Maternity** — Three of the four Maternity sub-departments (Antenatal, Postnatal Ward, Postnatal Community) did not report Total Eligible figures, meaning response rate analysis and busyness tier classification could not be applied to these departments.

- **Low Response Suppression** — 122 rows (11.7%) were flagged and excluded from satisfaction calculations due to NHS England suppressing results where fewer than 5 responses were recorded. Trusts with consistently low responses are underrepresented in the analysis.

- **Independent Sector Providers** — The dataset includes independent sector providers alongside NHS Trusts. These operate differently and their inclusion may affect national average calculations and tier comparisons.

- ## ▶️ How to Run

### Prerequisites
- Python 3.x
- MySQL
- Tableau Public (free) — [Download here](https://public.tableau.com/en-us/s/download)
- Jupyter Notebook or VS Code with Jupyter extension

### Installation
Install the required Python libraries:
```bash
pip install pandas numpy openpyxl sqlalchemy mysql-connector-python python-dotenv
```

### Data
Download the NHS FFT data files for your chosen month from [NHS England](https://www.england.nhs.uk/fft/friends-and-family-test-data/) and save them to a local folder.

### Environment Setup
Create a `.env` file in the project root with the following variables:
DIRECTORY=path/to/your/raw/data/folder/
OUTPUT_DIRECTORY=path/to/your/tableau/output/folder/
MYSQL_USERNAME=your_mysql_username
MYSQL_PASSWORD=your_mysql_password
MYSQL_DATABASE=nhs_fft

### Running the Analysis
1. Open the Jupyter notebook `nhs_fft_code.ipynb`
2. Update the file names in the data loading section to match your downloaded files
3. Run all cells from top to bottom
4. CSV exports will be saved to your `OUTPUT_DIRECTORY`
5. Connect the exported CSVs to Tableau Public to recreate the dashboards

### Database Setup
Create a MySQL database called `nhs_fft` before running the notebook:
```sql
CREATE DATABASE nhs_fft;
```

## 👤 About
Megan Higbee - Aspiring Healthcare Data Analyst

[LinkedIn] (www.linkedin.com/in/megan-higbee)
