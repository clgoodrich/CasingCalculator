
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

## Usage Guidelines
### Database Integration
```python
# Initialize database connection
wb_df = pd.read_sql('SELECT * FROM hole_parameters', conn)
casing_df = pd.read_sql('SELECT * FROM casing', conn)
string_df = pd.read_sql('SELECT * FROM string_parameters', conn)
```

### Wellbore Configuration
```python
wellbore = WellBoreExpanded(
    name='Wellbore (Planned)',
    top=wb_df['conductor_casing_bottom'].iloc[0],
    bottom=wb_df['max_depth_md'].iloc[0],
    method='top_down',
    tol=wb_df['top_of_liner'].iloc[0],
    max_md_depth=wb_df['max_depth_md'].iloc[0],
    max_tvd_depth=wb_df['max_depth_tvd'].iloc[0]
)
```

## Best Practices
- Avoid global state modifications
- Use module-level constants for configuration
- Implement proper encapsulation
- Document design decisions
- Follow PEP 8 style guidelines
- Use type hints for better code maintainability

## Performance Considerations
- Optimized numerical calculations
- Efficient database queries
- Memory management for large datasets
- Vectorized operations where possible

## Future Development
- Enhanced temperature effects modeling
- Machine learning integration for design optimization
- Real-time monitoring capabilities
- Advanced visualization features
- Cloud deployment options

## Installation
```
pip install -r requirements.txt
```

## Contributing
- Follow PEP 8 style guidelines
- Include comprehensive documentation
- Add unit tests for new features
- Maintain backward compatibility
- Update requirements.txt as needed

## Support
For technical support and feature requests:
- Submit issues through the project tracker
- Consult the technical documentation
- Contact the development team
