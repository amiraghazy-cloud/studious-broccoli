# Employee Satisfaction Analysis

## Project Overview
A comprehensive data analysis project examining employee satisfaction patterns and trends.

## Objectives
- Analyze satisfaction trends across departments
- Identify correlation between satisfaction, salary, performance, and tenure
- Flag high-risk employees for retention efforts
- Provide data-driven HR recommendations

## Key Findings
- **Average company satisfaction:** 3.73/5
- **Engineering department** shows lowest satisfaction (2.67/5) despite highest salaries
- **Weak correlation** between salary and satisfaction (r=0.12)
- **Strong correlation** between performance and satisfaction (r=0.45)
- **4 employees** identified as high retention risk

## Technologies Used
- **Python 3.x**
- **Pandas** - Data manipulation and analysis
- **Matplotlib** - Data visualization
- **NumPy** - Numerical calculations

## Project Structure
```
employee-satisfaction-analysis/
├── data/
│   └── employee_data.csv
├── visualizations/
│   └── satisfaction_dashboard.png
├── employee_satisfaction_analysis.py
├── README.md
└── requirements.txt
```

## How to Run

1. **Clone this repository:**
```bash
git clone https://github.com/yourusername/employee-satisfaction-analysis.git
cd employee-satisfaction-analysis
```

2. **Install dependencies:**
```bash
pip install -r requirements.txt
```

3. **Run the analysis:**
```bash
python employee_satisfaction_analysis.py
```

4. **View results:**
- Check console output for detailed statistics
- Find visualization in `visualizations/satisfaction_dashboard.png`

## Business Recommendations

### Immediate Actions
- Investigate Engineering department concerns through focus groups
- Schedule retention conversations with 4 at-risk employees
- Review compensation competitiveness in low-satisfaction areas

### Long-term Strategies
- Implement quarterly satisfaction pulse surveys
- Create mentorship programs for employees with <2 years tenure
- Invest in management training for department leaders

## Sample Visualizations

![Satisfaction Dashboard](visualizations/satisfaction_dashboard.png)

## Insights
1. **Department patterns**: Engineering has high pay but low satisfaction, suggesting non-monetary factors drive engagement
2. **Performance matters**: High performers show higher satisfaction, indicating recognition effectiveness
3. **Tenure effect**: New employees (<1 year) show variable satisfaction, highlighting onboarding importance

## Author
**Amira Ghazy**
- LinkedIn: https://www.linkedin.com/in/amira-ghazy/
- Email: miraghazy@yahoo.com
- Portfolio: https://github.com/amiraghazy-cloud/studious-broccoli

## License
MIT License - feel free to use this project for learning purposes

---

*This project demonstrates skills in data analysis, statistical thinking, and business intelligence for HR analytics roles.*
```

## For requirements.txt (separate file):
```
pandas
matplotlib
numpy