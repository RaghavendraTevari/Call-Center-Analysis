# Call-Center-Analysis

Building a high-impact call center dashboard in Excel requires moving beyond simple lists and focusing on **trends** and **actionable KPIs**. To make this professional, you’ll want to structure your workbook with three distinct layers: **Data**, **Calculations**, and the **Dashboard** view.

Here is a blueprint to build a full, interactive dashboard.

---

## 1. Core KPIs to Track

Before building, ensure your data includes these vital metrics:

| Metric | Why it Matters | Goal (Standard) |
| --- | --- | --- |
| **CSAT** | Customer Satisfaction Score. | > 80% |
| **AHT** | Average Handle Time (Talk + Hold + Wrap). | Varies by Industry |
| **SLA** | Service Level (e.g., % of calls answered in < 20s). | 80/20 Rule |
| **FCR** | First Call Resolution. | > 70% |
| **Occupancy** | Time spent on calls vs. idle time. | 85% - 90% |

---

## 2. Step-by-Step Structure

### Phase 1: The "Data" Sheet

Format your raw data as an **Excel Table** (`Ctrl + T`). This ensures that as you add new rows, your charts update automatically. Your columns should include:

* Date/Time
* Agent Name
* Call Duration (Seconds)
* Wait Time (Seconds)
* Resolution Status (Yes/No)
* CSAT Score (1-5)

### Phase 2: The "Calculations" Sheet

* **Total Calls by Day** (to see volume trends).
* **Average CSAT by Agent** (for performance rankings).
* **AHT vs. FCR** (to see if faster calls are resulting in lower quality).

### Phase 3: The "Dashboard" View

1. **Remove Gridlines:** (View > Uncheck Gridlines) for a clean, app-like feel.
2. **Slicers:** Insert Slicers for *Date*, *Team*, and *Call Type*. Connect them to all Pivot Tables so the whole dashboard filters at once.
3. **Visuals:**
* **Big Number Cards:** Use simple text boxes linked to cells for "Total Calls" and "Overall CSAT."
* **Combo Chart:** Use a bar chart for Call Volume and a line chart for SLA % on the secondary axis.
* **Heat Map:** Use conditional formatting on an agent list to highlight who is meeting targets.



---

## 3. The Pro Formula Secret

To calculate **Service Level Agreement (SLA)** dynamically, use a formula like this (assuming 20 seconds is your target):

`=COUNTIF(Wait_Time_Range, "<=20") / COUNTA(Total_Calls_Range)`

---
I’d be happy to! To make this look like a real production environment, I’ll generate a dataset that includes "messy" elements like different call types, agent tiers, and varying satisfaction scores.

This script uses `pandas` and `numpy` to create 1,000 rows of data. It ensures that **Wait Time** and **Talk Time** follow a realistic distribution (most are short, a few are very long).

### Python Script: Call Center Data Generator

```python
import pandas as pd
import numpy as np
from datetime import datetime, timedelta
import random

# Configuration
rows = 1000
agents = ['Alex M.', 'Sarah J.', 'Kevin L.', 'Priyanka R.', 'Jordan T.', 'Maria G.']
teams = ['Billing', 'Technical Support', 'General Inquiry']
call_types = ['Inbound', 'Outbound']

data = []

for i in range(rows):
    # Generate random date within the last 30 days
    date = datetime.now() - timedelta(days=random.randint(0, 30), hours=random.randint(0, 23))
    
    # Generate realistic metrics (in seconds)
    wait_time = int(np.random.exponential(scale=30))  # Most waits are short
    talk_time = int(np.random.normal(loc=300, scale=100)) # Avg 5 mins
    wrap_time = random.randint(30, 120)
    
    # Logic for FCR and CSAT
    resolved = random.choice(['Yes', 'No'])
    csat = random.randint(1, 5) if resolved == 'Yes' else random.randint(1, 3)

    data.append([
        date.strftime("%Y-%m-%d %H:%M"),
        random.choice(agents),
        random.choice(teams),
        random.choice(call_types),
        wait_time,
        talk_time,
        wrap_time,
        resolved,
        csat
    ])

# Create DataFrame
columns = ['Timestamp', 'Agent', 'Team', 'Call Type', 'Wait Time (s)', 'Talk Time (s)', 'Wrap Time (s)', 'Resolved', 'CSAT']
df = pd.DataFrame(data, columns=columns)

# Save to CSV
df.to_csv('call_center_data.csv', index=False)
print("File 'call_center_data.csv' has been generated!")

```

---





