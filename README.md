# london-sen-data

This data has messy split-level column headers:

| Code | New Code | Area | 2002 | | | 2003 | | | 2004 | | | ... |
|------|----------|------|------|------|------|------|------|------|------|------|------|-----|
| | | | Total pupils | Pupils with statements | %3 | Total pupils | Pupils with statements | %3 | Total pupils | Pupils with statements | %3 | ... |
| 00AA | E09000001 | City of London | 1,734 | 0 | 0.0 | 1,957 | x | x | 2,104 | 7 | 0.3 | ... |

**Header Structure:**
- **Row 1**: Years (2002-2019) - each year spans 3 columns
- **Row 2**: Repeating column names for each year:
  - `Total pupils` - Total number of pupils
  - `Pupils with statements` - Number of pupils with SEN statements
  - `%3` - Percentage of pupils with statements

**Fixed Columns:**
- `Code` - Original local authority code
- `New Code` - ONS area code (E09000xxx format)
- `Area` - London borough name

**Data Coverage:**
- 33 London boroughs (City of London + 32 London boroughs)
- Annual data from 2002 to 2019
- Some values marked as 'x' indicate suppressed/unavailable data


# Tidying 
First, we initialise the columns that **aren't** year by year (borough), then we loop through the metric columns and create a version for each year. E.g. total_pupils_2002/2003 etc. 

Then, we clean and convert numeric fields to actually be numeric. 
Next, we dropn the 'code', and 'new code' columns. We don't need these. 
Then, we convert it from a wide table to a long table. One row per borough per year. 

After that, we're in a position to start creating visualisations