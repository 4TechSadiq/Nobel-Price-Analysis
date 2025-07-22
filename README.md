# Nobel Prize Data Analysis

## Overview

This project analyzes historical Nobel Prize data from 1901 to 2020 to uncover patterns and trends in Nobel Prize awards. The analysis explores various aspects including gender distribution, country representation, prize sharing trends, and temporal patterns in Nobel Prize awards.

## Dataset

The dataset contains **962 rows** and **16 columns** covering Nobel Prize winners from 1901 to 2020.

### Dataset Features

| Column | Description | Data Type |
|--------|-------------|-----------|
| `year` | Year the prize was awarded | int64 |
| `category` | Prize category (Chemistry, Literature, Physics, Medicine, Peace, Economics) | object |
| `prize` | Full prize name | object |
| `motivation` | Reason for the prize award | object |
| `prize_share` | Fraction of prize awarded (e.g., "1/2", "1/3") | object |
| `laureate_type` | Individual or Organization | object |
| `full_name` | Winner's full name | object |
| `birth_date` | Date of birth | datetime64[ns] |
| `birth_city` | Birth city | object |
| `birth_country` | Birth country (historical) | object |
| `birth_country_current` | Birth country (current borders) | object |
| `sex` | Gender (Male/Female) | object |
| `organization_name` | Affiliated organization | object |
| `organization_city` | Organization's city | object |
| `organization_country` | Organization's country | object |
| `ISO` | ISO country code | object |

## Data Quality Notes

- **Missing Values**: Organizations (particularly Peace Prize winners) have missing birth information
- **Date Estimates**: Some birth dates are estimated (e.g., Michael Houghton, Venkatraman Ramakrishnan, Nadia Murad use July 2nd as mid-year estimate)
- **No Duplicates**: Dataset contains no duplicate entries

### Missing Data Distribution
- `motivation`: 88 missing values
- `birth_date`: 28 missing values (primarily organizations)
- `organization_name`: 255 missing values (individuals without organizational affiliation)

## Installation & Setup

### Requirements

```python
pandas >= 1.3.0
numpy >= 1.21.0
plotly >= 5.0.0
seaborn >= 0.11.0
matplotlib >= 3.4.0
```

### Installation

```bash
pip install pandas numpy plotly seaborn matplotlib
```

For Google Colab users:
```bash
%pip install --upgrade plotly
```

## Usage

### Basic Setup

```python
import pandas as pd
import numpy as np
import plotly.express as px
import plotly.graph_objects as go
import seaborn as sns
import matplotlib.pyplot as plt

# Load the data
df_data = pd.read_csv('nobel_prize_data.csv')

# Convert birth_date to datetime
df_data.birth_date = pd.to_datetime(df_data.birth_date)

# Create prize share percentage column
separator_values = df_data.prize_share.str.split("/", expand=True)
numerator = pd.to_numeric(separator_values[0])
denominator = pd.to_numeric(separator_values[1])
df_data["share_pct"] = numerator / denominator
```

## Key Analysis Areas

### 1. Gender Distribution Analysis
- Overall male vs. female laureate distribution
- Gender trends by category
- Historical progression of female representation

### 2. Geographic Analysis
- Country-wise prize distribution
- Choropleth mapping of global Nobel Prize distribution
- Analysis by birth country vs. organization country

### 3. Temporal Analysis
- Prize frequency over time
- Impact of world wars on prize distribution
- 5-year rolling averages for trend identification

### 4. Prize Sharing Trends
- Evolution of shared vs. individual prizes
- Category-specific sharing patterns
- Correlation between prize sharing and total prizes awarded

### 5. Category Analysis
- Prize distribution across six categories
- Country specialization in specific categories
- Historical development of prize categories (Economics added in 1969)

## Key Visualizations

### Plotly Visualizations
- **Donut Charts**: Gender distribution
- **Bar Charts**: Prizes by category and country
- **Choropleth Maps**: Global prize distribution
- **Stacked Bar Charts**: Category breakdown by country
- **Line Charts**: Cumulative prizes over time

### Matplotlib Visualizations
- **Scatter Plots**: Annual prize counts with rolling averages
- **Dual-Axis Charts**: Prize frequency vs. sharing trends

## Notable Findings

### Historical Milestones
- **First Nobel Prize**: 1901
- **Latest Data**: 2020
- **Economics Prize**: First awarded in 1969
- **First Female Winners**: Marie Curie (Physics 1903), Bertha von Suttner (Peace 1905), Marie Curie (Chemistry 1911)

### Trends
- Increasing number of shared prizes over time
- Growth in total prizes awarded annually
- Significant impact of world wars on prize distribution
- United States emergence as leading prize-winning nation

## File Structure

```
nobel-prize-analysis/
│
├── nobel_prize_data.csv          # Main dataset
├── analysis_notebook.ipynb       # Jupyter notebook with complete analysis
├── README.md                      # This file
└── requirements.txt               # Python dependencies
```

## Data Sources

The Nobel Prize data spans from Alfred Nobel's 1895 will establishment through 2020, covering all six prize categories:
- Chemistry
- Literature  
- Physics
- Physiology or Medicine
- Peace
- Economic Sciences (added 1969)

## Contributing

When contributing to this analysis:
1. Ensure data integrity when adding new years
2. Maintain consistent date formatting
3. Handle missing values appropriately for organizations
4. Update visualizations to reflect new data ranges

## License

This project is for educational and research purposes. Nobel Prize data is publicly available information.

## Contact

For questions about this analysis, please refer to the original data sources and Nobel Prize official documentation.

---

*"Prizes to those who, during the preceding year, have conferred the greatest benefit to humankind"* - Alfred Nobel, 1895
