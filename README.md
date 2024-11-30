
# Casing Design Analysis Tool with Welleng Integration

## Overview
A specialized Python-based tool that extends the welleng module capabilities for advanced casing design analysis in oil and gas well planning. This tool provides comprehensive calculations for burst loads, tension factors, and maximum anticipated pressures while integrating with welleng's wellbore trajectory and engineering calculations.

Original WellEng Author: <jonnycorcutt@gmail.com>

Original Repository: https://github.com/jonnymaserati/welleng

Modified by: Colton Goodrich <coltonlg@gmail.com>

Significant modifications:
- Changed from generic String class to specialized WellBore implementation
- Added wellbore-specific parameter validation and type checking
- Introduced casing mechanical properties and calculations
- Modified section management to use structured List[Dict] input
- Added cement volume and geometric property calculations
- Incorporated industry-specific validation rules
- Maintained original method='bottom_up'/'top_down' architecture

## Dependencies
```
Primary Dependencies:
- Python 3.7+
- numpy==1.26.4
- pandas==2.2.3
- welleng==0.8.5
- scipy==1.14.1

Visualization Dependencies:
- matplotlib==3.9.2
- vedo==2024.5.2
- vtk==9.3.1

Additional Requirements:
- certifi==2024.8.30
- contourpy==1.3.1
- pyproj==3.7.0
- PyYAML==6.0.2
- typing_extensions==4.12.2
```

## Core Functionality
### Well Design Analysis
- Integration with welleng trajectory calculations
- Casing seat depth optimization
- Formation pressure analysis
- Multi-string design verification

### Pressure Calculations
- MAPS (Maximum Anticipated Surface Pressure)
- Burst load analysis
- Internal/external pressure differentials
- Formation fracture pressure integration

### Safety Factor Analysis
- Burst design factors
- Tension load calculations
- Combined loading scenarios
- Section-to-section integrity verification

## Data Management
The tool utilizes SQL database integration for:
- Well parameters storage
- Casing specifications
- String design data
- Formation properties

## Calculations Performed
Calculations performed:
1. Formation fracture initial pressure
2. Annular cement volume
3. Cement column height
4. Top of cement (TOC)
5. Maximum allowable surface pressure (MASP)
6. Collapse loading conditions
7. Collapse design factor
8. Neutral point location
9. Air weight tension
10. Buoyed tension
11. Tension design factor
12. 
## Usage Guidelines
### Database Integration
```python
# Initialize database connection
conn = sqlite3.connect('sample_casing.db')
wb_df = pd.read_sql('SELECT * FROM wb_info', conn)
used_df = pd.read_sql('SELECT * FROM database', conn)
conn.close()
```

### Wellbore Configuration
```python
    wellbore = WellBoreExpanded(
        name='Wellbore (Planned)',
        top=100,
        bottom=20500,
        method='top_down',
        tol=9250,
        max_md_depth=20500,
        max_tvd_depth=9200,
        frac_gradient=1.0,
    )
```

## Installation
```
pip install -r requirements.txt
```
