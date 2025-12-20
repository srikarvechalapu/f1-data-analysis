
<img width="1329" alt="Screenshot 2023-12-30 at 12 06 02" src="https://github.com/andrewgrahampowell/f1-data-analysis/assets/98211756/37f73cd5-8d2e-41c7-af2d-13e7bee6f097">

# F1 Data Analysis Project

The Formula 1 Data Analysis project is a comprehensive exploration of the world of Formula 1 racing through the lens of data analytics. This project combines the power of SQL for data manipulation and Tableau for data visualisation to provide insights into the thrilling world of Formula 1 racing from 1953-2020.

## Key Components:

Data Collection and Preparation: The project begins by gathering extensive Formula 1 data, including race results, driver statistics, team information, and circuit details. This raw data is then cleaned and organised for analysis.

Database Design: A relational database is created using SQL to efficiently store and manage the Formula 1 data. This step includes defining tables, relationships, and constraints to ensure data integrity.

SQL Data Queries: SQL queries are crafted to extract meaningful insights from the database. This may involve calculating driver and team performance metrics, historical trend analysis, and identifying key patterns in the data.

Tableau Visualisation: The SQL-derived insights are visualised using Tableau, a powerful data visualisation tool, and Deepnote. Interactive dashboards and reports are designed to provide users with a user-friendly interface to explore the data.

Performance Analysis: Using SQL and Tableau, the project delves into various aspects of Formula 1 racing, such as driver performance across seasons, race track statistics, and the impact of rule changes.

Reporting and Presentation: The project concludes by creating comprehensive reports and presentations that summarise the findings, making it accessible to a wider audience.

## Benefits:

Gain a deeper understanding of Formula 1 racing from a data-driven perspective.

Enhance the overall Formula 1 fan experience by making complex data accessible and engaging.

This project offers a unique opportunity to combine the technical skills of SQL with the data visualisation capabilities of Tableau to unlock insights about one of the dynamic sports in the world.

## Links:

Link to full Deepnote Project Notebook: # 🏎️ Formula 1 Data Analysis (1953–2020)

A comprehensive exploration of Formula 1 racing through data analytics, combining SQL for data manipulation with Deepnote and Tableau for visualization. This project analyzes decades of F1 history to uncover performance insights and explore the debate: *Who is the greatest F1 driver of all time?*

![F1 Banner](https://img.shields.io/badge/Formula%201-Data%20Analysis-red?style=for-the-badge&logo=f1)
![SQL](https://img.shields.io/badge/SQL-Queries-blue?style=for-the-badge&logo=postgresql)
![Tableau](https://img.shields.io/badge/Tableau-Visualization-orange?style=for-the-badge&logo=tableau)
![Python](https://img.shields.io/badge/Python-Analysis-green?style=for-the-badge&logo=python)

---

## 📊 Key Findings at a Glance

| Metric | Result | Details |
|--------|--------|---------|
| 🏁 **Most Races** | Fernando Alonso | 358 career races |
| 🏆 **Most Career Points** | Lewis Hamilton | 4,396 points |
| ⚡ **Fastest Ever Lap** | Carlos Sainz | Red Bull Ring, 2020-07-12 (1:05.6) |
| 🥇 **Highest Avg Finish** | Alberto Ascari | 2.18 average position (min 20 races) |
| 📉 **Lowest Avg Finish** | Nikita Mazepin | 17.8 average position (min 20 races) |

---

## 🔍 Project Overview

This project performs in-depth exploratory data analysis on Formula 1 data spanning nearly seven decades (1953–2020). By leveraging SQL for data manipulation and combining it with powerful visualization tools, we uncover hidden patterns, analyze driver performance metrics, and provide data-driven insights into one of the world's most dynamic sports.

### 🎯 Objectives

- Identify candidates for the greatest Formula 1 driver of all time
- Analyze driver performance across multiple metrics and eras
- Detect anomalies and outliers in race data
- Visualize trends and patterns in F1 racing history
- Provide context for cross-era comparisons

---

## 🏗️ Project Architecture

```mermaid
flowchart TB
    subgraph Data Sources
        A[(results.csv)] 
        B[(drivers.csv)]
        C[(races.csv)]
        D[(circuits.csv)]
    end
    
    subgraph Data Processing
        E[Data Cleaning]
        F[SQL Queries]
        G[Anomaly Detection]
    end
    
    subgraph Analysis
        H[Driver Performance]
        I[Lap Time Analysis]
        J[Historical Trends]
    end
    
    subgraph Visualization
        K[Deepnote Charts]
        L[Tableau Dashboards]
    end
    
    subgraph Output
        M[Insights & Reports]
    end
    
    A --> E
    B --> E
    C --> E
    D --> E
    E --> F
    F --> G
    G --> H
    G --> I
    G --> J
    H --> K
    I --> K
    J --> K
    H --> L
    I --> L
    J --> L
    K --> M
    L --> M
```

---

## 🗄️ Database Schema

```mermaid
erDiagram
    DRIVERS {
        int driverId PK
        string forename
        string surname
        string nationality
        date dob
    }
    
    RACES {
        int raceId PK
        int circuitId FK
        string name
        date date
        int year
    }
    
    CIRCUITS {
        int circuitId PK
        string name
        string location
        string country
    }
    
    RESULTS {
        int resultId PK
        int raceId FK
        int driverId FK
        int position
        float points
        string fastestLapTime
        float fastestLapSpeed
    }
    
    DRIVERS ||--o{ RESULTS : "competes in"
    RACES ||--o{ RESULTS : "has"
    CIRCUITS ||--o{ RACES : "hosts"
```

---

## 📈 Analysis Workflow

```mermaid
flowchart LR
    subgraph EDA["Exploratory Data Analysis"]
        A[Load Data] --> B[Identify Structure]
        B --> C[Find Anomalies]
        C --> D[Clean Data]
    end
    
    subgraph Performance["Performance Analysis"]
        E[Career Points]
        F[Average Finish]
        G[Lap Times]
        H[Experience Quartiles]
    end
    
    subgraph Insights["Generate Insights"]
        I[Statistical Summary]
        J[Visualizations]
        K[Conclusions]
    end
    
    D --> E
    D --> F
    D --> G
    D --> H
    E --> I
    F --> I
    G --> I
    H --> I
    I --> J
    J --> K
```

---

## 🔬 Detailed Analysis Breakdown

### 1️⃣ Exploratory Data Analysis (EDA)

The analysis begins with understanding the data structure, identifying errors, and uncovering patterns:

- **Most Experienced Driver**: Fernando Alonso leads with 358 career races, followed by Kimi Räikkönen (352)
- **Anomaly Detection**: Identified RaceID 1046 (Bahrain 2020) as an outlier due to a reformatted COVID-era race with unusually fast lap times under 60 seconds
- **Data Cleaning**: Excluded anomalous data points to prevent skewing results

### 2️⃣ Lap Time Analysis

```mermaid
flowchart TD
    A[Raw Lap Times] --> B{Anomaly Check}
    B -->|Normal| C[Include in Analysis]
    B -->|Anomaly| D[Investigate]
    D --> E{Valid Exception?}
    E -->|Yes - COVID Race| F[Exclude from Analysis]
    E -->|No| C
    C --> G[Fastest Lap Rankings]
    G --> H[By Driver]
    G --> I[By Circuit]
```

**Key Findings:**
- **Fastest Ever Lap**: Carlos Sainz at Red Bull Ring (2020-07-12) — 1:05.6
- **Slowest Circuit**: Circuit de Spa-Francorchamps (Belgium) — longer track length
- **Fastest Circuit**: Red Bull Ring (Austria) — short, high-speed layout

### 3️⃣ Driver Performance Metrics

```mermaid
pie title Performance Quartile Distribution
    "Q1 - Elite (Top 25%)" : 25
    "Q2 - Strong (25-50%)" : 25
    "Q3 - Average (50-75%)" : 25
    "Q4 - Below Average (75-100%)" : 25
```

**Experience Level Categories:**
| Level | Race Count | Characteristics |
|-------|------------|-----------------|
| Rookie | 1–50 races | Learning phase, variable results |
| Developing | 51–100 races | Establishing consistency |
| Experienced | 101–150 races | Peak performance years |
| Veteran | 151+ races | Sustained excellence |

### 4️⃣ Points System Evolution

The F1 points system has changed significantly over the decades, making direct comparisons challenging:

```mermaid
timeline
    title Formula 1 Points System Evolution
    1950-1959 : 8-6-4-3-2 points
              : Only top 5 scored
    1960-1990 : 9-6-4-3-2-1 points
              : Top 6 scored
    1991-2002 : 10-6-4-3-2-1 points
              : Winner emphasis increased
    2003-2009 : 10-8-6-5-4-3-2-1 points
              : Top 8 scored
    2010-Present : 25-18-15-12-10-8-6-4-2-1
                 : Top 10 scored
```

---

## 🛠️ Technologies Used

| Technology | Purpose | Details |
|------------|---------|---------|
| **SQL** | Data Querying | Complex joins, window functions, CTEs, aggregations |
| **Deepnote** | Interactive Analysis | Notebook environment with built-in charting |
| **Tableau** | Dashboards | Interactive visualizations and reporting |
| **Python** | Data Processing | Automation and additional analysis |

---

## 📁 Data Sources

The project utilizes multiple interconnected datasets:

```
📦 data/
├── 📄 results.csv      # Race results, positions, points, lap times
├── 📄 drivers.csv      # Driver names, nationalities, DOB
├── 📄 races.csv        # Race metadata, dates, circuit references
└── 📄 circuits.csv     # Circuit names, locations, countries
```

**Data Coverage:**
- **Time Span**: 1953–2020 (67 years)
- **Total Races**: 1,000+ Grand Prix events
- **Drivers**: 800+ unique drivers
- **Circuits**: 70+ unique circuits worldwide

---

## 📊 Visualizations Included

| Visualization | Type | Insights |
|---------------|------|----------|
| Most Races by Driver | Bar Chart | Top 25 most experienced drivers |
| Alonso's Fastest Laps | Scatter Plot | Circuit-by-circuit performance |
| Fastest Laps by Track | Line Chart | Track characteristics comparison |
| Experience vs Points | Bar Chart | Correlation between races and points |
| Avg Finish Position | Bar Chart | Performance consistency metrics |
| Performance Quartiles | Grouped Analysis | Driver categorization by era |

---

## 🏁 The Greatest Driver Debate

### Why It's Complicated

```mermaid
mindmap
    root((GOAT Debate))
        Points System
            Changed multiple times
            Modern drivers score more
            Not directly comparable
        Technology
            Cars evolved dramatically
            Safety improvements
            Reliability factors
        Team Budgets
            Top teams dominate
            Resource disparity
            Driver vs car performance
        Competition Level
            Grid size changes
            Talent pool depth
            Era-specific challenges
        Longevity
            Career length varies
            Peak performance windows
            Injury risks
```

### The Case for Different Eras

| Era | Top Drivers | Context |
|-----|-------------|---------|
| **1950s** | Fangio, Ascari | Dangerous conditions, mechanical unreliability |
| **1960s-70s** | Clark, Stewart, Lauda | High fatality rates, driver courage paramount |
| **1980s-90s** | Prost, Senna, Schumacher | Technology revolution, fierce rivalries |
| **2000s-2010s** | Schumacher, Alonso, Vettel | Aerodynamic era, team dominance |
| **2010s-2020s** | Hamilton, Verstappen | Hybrid era, data-driven performance |

---

## 🚀 Getting Started

### Prerequisites

- SQL-compatible database or query environment
- Deepnote account (optional, for notebook access)
- Tableau Desktop/Public (optional, for dashboard)

### Installation

1. **Clone the repository:**
   ```bash
   git clone https://github.com/srikarvechalapu/f1-data-analysis.git
   cd f1-data-analysis
   ```

2. **Set up the data:**
   ```bash
   # Ensure CSV files are in the data/ directory
   ls data/
   # Expected: results.csv, drivers.csv, races.csv, circuits.csv
   ```

3. **Run SQL queries:**
   ```sql
   -- Example: Find the driver with most races
   SELECT 
       d.forename, 
       d.surname, 
       COUNT(r.RaceId) AS race_count
   FROM results r
   JOIN drivers d ON r.driverId = d.driverId
   GROUP BY r.driverId, d.surname, d.forename
   ORDER BY race_count DESC
   LIMIT 10;
   ```

4. **Explore visualizations:**
   - Open Deepnote notebook for interactive charts
   - Access Tableau dashboard for comprehensive views

---

## 📂 Project Structure

```
f1-data-analysis/
│
├── 📁 data/
│   ├── results.csv
│   ├── drivers.csv
│   ├── races.csv
│   └── circuits.csv
│
├── 📁 sql/
│   ├── eda_queries.sql
│   ├── driver_analysis.sql
│   └── lap_time_analysis.sql
│
├── 📁 notebooks/
│   └── f1_analysis.ipynb
│
├── 📁 visualizations/
│   └── tableau_dashboard.twbx
│
├── 📄 README.md
└── 📄 LICENSE
```

---

## 🔮 Future Enhancements

- [ ] Extend analysis to include 2021–2024 seasons
- [ ] Add constructor (team) performance analysis
- [ ] Implement predictive modeling for race outcomes
- [ ] Create interactive web dashboard
- [ ] Include weather impact analysis
- [ ] Add pit stop strategy evaluation

---

## 🤝 Contributing

Contributions are welcome! Please feel free to submit a Pull Request. For major changes, please open an issue first to discuss what you would like to change.

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

---

## 👤 Author & Maintainer

<table>
  <tr>
    <td align="center">
      <strong>Sai Srikar Vechalapu</strong><br>
      <em>Data Analyst</em><br>
      <sub>Expertise in SQL, Python, and Data Visualization</sub>
    </td>
  </tr>
</table>

📧 **Email:** vsrikar2025@gmail.com

🔗 **LinkedIn:** [linkedin.com/in/srikarvechalapu](https://www.linkedin.com/in/srikarvechalapu/)

---

## 📄 License

This project is licensed under the MIT License — see the [LICENSE](LICENSE) file for details.

---

## 🙏 Acknowledgments

- Formula 1 for inspiring generations of racing fans worldwide
- The open-source data community for making this analysis possible
- Ergast Developer API for historical F1 data
- All the legendary drivers who have made F1 the pinnacle of motorsport

---

<div align="center">

### 🏆 Who gets your vote for the greatest driver of all time?

*"Statistics provide valuable insights, but they may not fully capture a driver's skill, impact, or the context of their achievements."*

**⭐ Star this repository if you found it interesting!**

</div>

## Maintainer

This project is currently maintained by Sai Srikar Vechalapu, a Data Analyst with expertise in SQL, Python, and data visualization.

Contact: vsrikar2025@gmail.com | Linkedin: https://www.linkedin.com/in/srikarvechalapu/
