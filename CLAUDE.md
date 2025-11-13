# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a **standalone single-file web application** for the LCLS (Linac Coherent Light Source) Maintenance Dashboard. The entire application is contained in `index.html` - there is no build process, package manager, or separate source files.

## Architecture

### Single-File Structure
- **index.html**: Contains the complete application including HTML, CSS (via Tailwind CDN), and JavaScript (React via CDN)
- **maintenance-dashboard.jsx**: Original React component file (legacy - not used in the deployed version)

### Technology Stack (All CDN-based)
- **React 18**: Loaded via unpkg CDN
- **Chart.js 4.4.0**: For all data visualizations
- **Tailwind CSS**: For styling
- **Babel Standalone**: For in-browser JSX transformation

### Data Architecture
- All maintenance data is embedded as CSV string within the component (lines 32-152 in index.html)
- Data is parsed on component mount into structured objects
- No external API calls or data persistence

### Application Structure
The React application uses a tab-based interface with 6 views:
1. **Overview**: Key metrics and summary statistics
2. **Equipment**: Maintenance frequency, on-time performance, and downtime by equipment
3. **Technicians**: Workload distribution and performance analysis
4. **Tasks**: Task type frequency and downtime patterns
5. **Trends**: Monthly trends over Q1 2024
6. **AI**: Interface for AI-powered analysis (currently demo mode)

### Chart Component Pattern
All charts use a custom `ChartComponent` wrapper (lines 300-335) that:
- Wraps Chart.js canvas in a fixed-height container div
- Prevents infinite height growth by using `position: relative` container with explicit height
- Properly destroys and recreates charts on data changes
- Default height: 200px (can be overridden via `height` prop)

### Data Processing Functions
The application includes several aggregation functions that process the CSV data:
- `calculateStats()`: Overall metrics (total tasks, on-time rate, downtime)
- `getEquipmentStats()`: Equipment-level aggregations
- `getTechnicianStats()`: Technician-level performance
- `getTaskStats()`: Task type analysis
- `getMonthlyTrend()`: Time-series data by month

## Running the Application

Simply open `index.html` in any modern web browser:
```bash
open index.html
```

No build, compilation, or server required.

## Modifying Charts

When adding or modifying charts:
1. Always wrap the canvas in a container div with explicit height
2. Use the `ChartComponent` wrapper to avoid height growth issues
3. Chart heights: 200px (default), 220px (medium), 250px (large)
4. Set `maintainAspectRatio: false` in Chart.js options

Example:
```javascript
<ChartComponent
  type="bar"
  height={250}
  data={{ labels: [...], datasets: [...] }}
  options={{ scales: { y: { beginAtZero: true } } }}
/>
```

## Modifying Data

To update the maintenance data:
1. Locate the `csvData` string constant (line 32)
2. Maintain CSV format: `Date,Equipment,Task Performed,Technician,Scheduled,Completed On Time,Downtime Impact (hrs)`
3. Date format: YYYY-MM-DD
4. Boolean fields: Y/N
5. Downtime: decimal hours

## Browser Console Warnings

The following console warnings are expected in development and can be ignored:
- Tailwind CSS CDN usage warning
- Babel in-browser transformer warning

These are suggestions for production builds but don't affect functionality in this standalone demo.
