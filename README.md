# Wellbore Casing Design Analysis Tool

## Overview
A Python-based tool for analyzing and designing wellbore casing configurations. This tool processes wellbore data, casing specifications, and hole parameters to perform comprehensive casing design calculations.

## Features
- Wellbore configuration analysis
- Casing section property calculations
- Multi-section casing design
- Mechanical property verification
- Cement volume calculations

## Requirements
- Python 3.7+
- pandas
- sqlite3

## Database Schema
The tool requires a SQLite database (`sample_casing.db`) with the following tables:

### wb_info
- conductor_casing_bottom
- casing_depths
- top_of_liner
- max_depth_md
- max_depth_tvd
- frac_gradient

### hole_parameters
- label
- mw (mud weight)
- tvd
- hole_washout
- internal_gradient
- backup_mud

### casing
- label
- hole_size
- csg_size
- set_depth
- csg_weight
- csg_grade
- csg_collar
- lead_qty
- lead_yield
- tail_qty
- tail_yield

### string_parameters
- label
- collapse
- internalyieldpressure
- jointstrength
- bodyyield
- wall
- id

## Usage

```python
from wellbore_analyzer import WellBoreExpanded

# Initialize wellbore
wellbore = WellBoreExpanded(
    name='Wellbore (Planned)',
    top=conductor_casing_bottom,
    bottom=max_depth_md,
    method='top_down',
    tol=top_of_liner,
    max_md_depth=max_depth_md,
    max_tvd_depth=max_depth_tvd
)

# Add casing sections
wellbore.add_section_with_properties(sections=[...])  # List of section dictionaries

# Calculate parameters
wellbore.calcParametersContained()
```

## Section Properties
Each casing section requires the following properties:
- id: Section identifier
- casing_type: Type of casing
- coeff_friction_sliding: Coefficient of friction (default 0.39)
- frac_gradient: Formation fracture gradient
- od: Outside diameter
- bottom: Setting depth
- weight: Casing weight
- grade: Casing grade
- connection: Connection type
- hole_size: Hole diameter
- cement_cu_ft: Cement volume
- tvd: True vertical depth
- washout: Hole washout factor
- int_gradient: Internal gradient
- mud_weight: Mud weight
- backup_mud: Backup mud weight
- body_yield: Body yield strength
- burst_strength: Burst strength
- wall_thickness: Wall thickness
- csg_internal_diameter: Internal diameter
- collapse_pressure: Collapse pressure
- tension_strength: Tension strength

## Data Processing
The tool handles:
- Database connections and data retrieval
- String to list conversion for casing depths
- Parameter validation
- Section-wise calculations
- Mechanical property verification

## Error Handling
The system includes comprehensive error handling for:
- Database connection issues
- Data validation
- Parameter processing
- Section calculations

## Note
This tool is designed for professional wellbore engineering applications. All measurements should be in consistent units according to industry standards.
