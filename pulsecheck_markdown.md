# PulseCheck - Employee Sentiment & Culture Analytics Platform

**Author:** Amira Ghazy  
**Date:** October 2025  
**Version:** 1.0

## Overview

PulseCheck is a Python-based HR analytics tool designed to analyze employee survey data and provide actionable insights into employee sentiment, engagement, and organizational culture. The platform helps HR teams identify trends, at-risk employees, and areas for improvement.

## Features

- **eNPS (Employee Net Promoter Score) Calculation** - Measure employee advocacy and loyalty
- **Sentiment Analysis** - Analyze text responses using natural language processing
- **Department Comparisons** - Compare metrics across different departments
- **Trend Analysis** - Track sentiment changes over time
- **Word Frequency Analysis** - Identify common themes in feedback
- **Attrition Risk Analysis** - Flag employees at risk of leaving
- **Executive Summaries** - Generate comprehensive reports for leadership

## Requirements

```python
pandas
numpy
matplotlib
seaborn
textblob
```

## Installation

```bash
pip install pandas numpy matplotlib seaborn textblob
```

## Quick Start

```python
from pulsecheck import PulseCheck

# Initialize with your survey data
pulse = PulseCheck('employee_survey_data.csv')

# Get overview
pulse.get_overview()

# Calculate eNPS
pulse.calculate_enps()

# Analyze sentiment
pulse.analyze_sentiment()
```

## Expected Data Format

Your CSV file should contain the following columns:

| Column Name | Type | Description |
|------------|------|-------------|
| `survey_date` | datetime | Date when survey was completed |
| `department` | string | Employee's department |
| `location` | string | Employee's work location |
| `role_level` | string | Employee's job level |
| `enps_score` | int | Net Promoter Score (0-10) |
| `overall_satisfaction` | int | Overall satisfaction rating (1-10) |
| `work_life_balance` | int | Work-life balance rating (1-10) |
| `career_growth` | int | Career growth satisfaction (1-10) |
| `compensation_satisfaction` | int | Compensation satisfaction (1-10) |
| `management_rating` | int | Management effectiveness rating (1-10) |
| `culture_rating` | int | Culture rating (1-10) |
| `what_you_enjoy` | string | Open text: What do you enjoy most? |
| `what_to_improve` | string | Open text: What should be improved? |

## Class Reference

### `PulseCheck`

Main class for employee sentiment and culture analytics.

#### `__init__(filepath)`

Initialize PulseCheck with survey data.

**Parameters:**
- `filepath` (str): Path to CSV file with employee survey data

**Example:**
```python
pulse = PulseCheck('data/q3_survey.csv')
```

---

#### `get_overview()`

Display high-level overview of the dataset including total responses, departments, locations, and date range.

**Returns:** None (prints to console)

**Example:**
```python
pulse.get_overview()
```

---

#### `calculate_enps(segment=None)`

Calculate Employee Net Promoter Score (eNPS).

**Formula:** eNPS = % Promoters (9-10) - % Detractors (0-6)

**Parameters:**
- `segment` (str, optional): Column name to segment by (e.g., 'department', 'location')

**Returns:** 
- Float (overall eNPS) or DataFrame (segmented eNPS)

**Interpretation:**
- **> 30**: Excellent - Strong employee advocacy
- **0-30**: Good - Room for improvement
- **< 0**: Negative - Urgent action needed

**Example:**
```python
# Overall eNPS
overall = pulse.calculate_enps()

# eNPS by department
by_dept = pulse.calculate_enps(segment='department')
```

---

#### `analyze_sentiment(text_column='what_you_enjoy')`

Perform sentiment analysis on text responses using TextBlob.

**Parameters:**
- `text_column` (str): Column containing text to analyze

**Returns:** Series of sentiment polarity scores (-1 to +1)

**Sentiment Categories:**
- **Negative**: < -0.1
- **Neutral**: -0.1 to 0.1
- **Positive**: > 0.1

**Example:**
```python
# Analyze what employees enjoy
sentiment = pulse.analyze_sentiment('what_you_enjoy')

# Analyze improvement suggestions
improvement_sentiment = pulse.analyze_sentiment('what_to_improve')
```

---

#### `department_comparison()`

Compare key metrics across all departments with visualization.

**Returns:** DataFrame with average scores by department

**Output:**
- Console table with department metrics
- Bar chart saved as `department_comparison.png`

**Example:**
```python
dept_scores = pulse.department_comparison()
```

---

#### `trend_analysis()`

Analyze sentiment trends over time with monthly aggregation.

**Returns:** DataFrame with monthly trends

**Metrics Tracked:**
- Overall satisfaction
- eNPS score
- Work-life balance
- Culture rating

**Output:**
- Console table with monthly data
- 4-panel trend chart saved as `trend_analysis.png`

**Example:**
```python
monthly_data = pulse.trend_analysis()
```

---

#### `word_frequency_analysis(text_column='what_to_improve', top_n=15)`

Analyze most common words in text responses.

**Parameters:**
- `text_column` (str): Column to analyze
- `top_n` (int): Number of top words to display

**Returns:** List of tuples [(word, count), ...]

**Output:**
- Console list of top words
- Horizontal bar chart saved as `word_frequency_{text_column}.png`

**Example:**
```python
# Analyze improvement suggestions
top_words = pulse.word_frequency_analysis('what_to_improve', top_n=20)

# Analyze positive feedback
enjoy_words = pulse.word_frequency_analysis('what_you_enjoy', top_n=15)
```

---

#### `identify_at_risk_employees(threshold=5)`

Identify employees at risk of leaving based on low satisfaction scores.

**Parameters:**
- `threshold` (int): Satisfaction score below which employee is considered at risk

**Criteria for At-Risk:**
- Overall satisfaction ≤ threshold, OR
- eNPS score ≤ 6

**Returns:** DataFrame of at-risk employees

**Output:**
- Total count and percentage
- Breakdown by department
- Common issues from improvement suggestions

**Example:**
```python
at_risk = pulse.identify_at_risk_employees(threshold=5)

# Get list of at-risk departments
risk_by_dept = at_risk['department'].value_counts()
```

---

#### `generate_executive_summary()`

Generate a comprehensive executive summary with key metrics and insights.

**Returns:** Dictionary with summary statistics

**Included Metrics:**
- Average satisfaction scores
- eNPS
- Culture rating
- At-risk employee percentage
- Department highlights

**Example:**
```python
summary = pulse.generate_executive_summary()
```

## Workflow Example

Complete analysis workflow:

```python
from pulsecheck import PulseCheck

# 1. Load data
pulse = PulseCheck('employee_survey_data.csv')

# 2. Get overview
pulse.get_overview()

# 3. Calculate overall eNPS
overall_enps = pulse.calculate_enps()

# 4. Calculate eNPS by department
dept_enps = pulse.calculate_enps(segment='department')

# 5. Analyze sentiment in feedback
pulse.analyze_sentiment('what_you_enjoy')
pulse.analyze_sentiment('what_to_improve')

# 6. Compare departments
dept_comparison = pulse.department_comparison()

# 7. View trends over time
trends = pulse.trend_analysis()

# 8. Analyze common themes
improvement_words = pulse.word_frequency_analysis('what_to_improve')
enjoy_words = pulse.word_frequency_analysis('what_you_enjoy')

# 9. Identify at-risk employees
at_risk = pulse.identify_at_risk_employees(threshold=5)

# 10. Generate executive summary
summary = pulse.generate_executive_summary()
```

## Output Files

PulseCheck generates the following visualization files:

- `department_comparison.png` - Bar chart comparing metrics across departments
- `trend_analysis.png` - 4-panel line chart showing trends over time
- `word_frequency_{column}.png` - Horizontal bar chart of most common words

All visualizations are saved at 300 DPI for presentation quality.

## Best Practices

1. **Data Quality**: Ensure your CSV has no missing values in critical columns
2. **Date Format**: Survey dates should be in a standard format (YYYY-MM-DD)
3. **Regular Analysis**: Run monthly or quarterly for trend tracking
4. **Segmentation**: Analyze by department, location, and role level to identify specific issues
5. **Action Planning**: Use at-risk analysis to prioritize retention efforts
6. **Text Analysis**: Review word frequency results to identify recurring themes

## Limitations

- **Stop Words**: Uses basic English stop words list (can be customized)
- **Sentiment Analysis**: TextBlob may not capture complex sentiment or sarcasm
- **Text Processing**: Basic tokenization without stemming or lemmatization
- **Statistical Tests**: No significance testing implemented

## Future Enhancements

- Advanced NLP with spaCy or transformers
- Topic modeling for open text responses
- Predictive modeling for attrition risk
- Real-time dashboard integration
- Multi-language support
- Benchmark comparisons

## Support

For questions or issues, please contact the HR Analytics team or refer to the internal documentation portal.

---

*Last updated: October 2025*