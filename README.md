Aim: To perform extensive data cleaning, exploratory data analysis (EDA), and geospatial visualization on the global COVID-19 dataset using Python.

## Theory:
This experiment focuses on End-to-End Data Analysis and Predictive Modeling, specifically applied to a COVID-19 dataset.   
The theory centers on the data science lifecycle, which begins with data ingestion and cleaning, followed by exploratory analysis to find trends (such as growth rates in confirmed cases), and concludes with machine learning to predict future outcomes. 
By integrating libraries for data manipulation, visualization, and predictive modeling, this program demonstrates how to transform raw pandemic data into actionable insights, such as identifying hotspots or forecasting mortality trends.  

Parameter breakdown:
locations="Country/Region": The column containing the geographic identifiers (country names). 

locationmode="country names": Tells Plotly to match the string values against its built-in country name lookup table.   

color="Confirmed": The column whose values control the fill colour of each country.   

color_continuous_scale="reds": A sequential colour palette where low values appear light red and high values appear dark red. 

range_color=[0, 10000000]: Fixes the minimum and maximum of the colour scale explicitly, ensuring consistent colour mapping regardless of data extremes. Without this, the scale auto-adjusts, which can visually distort lightly affected regions.   

A second map is generated identically but with color="Recovered" and color_continuous_scale="greens", allowing a direct visual comparison of confirmed versus recovered case distributions across the globe.

<img width="1808" height="543" alt="image" src="https://github.com/user-attachments/assets/61ebb026-a0d5-4134-92c0-0a7b8c8a1d1d" />

<img width="1808" height="542" alt="image" src="https://github.com/user-attachments/assets/6c4a7125-1eb0-46ee-9994-a3fab639003a" />

India Choropleth Map — Custom GeoJSON with px.choropleth():

Unlike the world map which uses Plotly's built-in country boundaries, mapping Indian states requires custom geographic boundary data. A GeoJSON file containing state outlines is downloaded from a public GitHub URL using urllib.request.urlopen() and parsed into a Python dictionary using json.load(). A copy of top_state is made using copy() and an Active column is computed on it before passing it to the map function.

px.choropleth() is called with the following key parameters:

geojson=india_geojson: Passes the custom GeoJSON geometry so Plotly knows the boundaries of each Indian state. 

featureidkey="properties.NAME_1": The path within the GeoJSON feature properties that holds the state name. Plotly matches values at this path against the locations column to link each row of data to its corresponding boundary on the map.   

locations="Province/State": The DataFrame column containing state names to match against the GeoJSON.  
color="Confirmed": The column whose values determine the fill colour intensity.   

hover_name="Province/State": The column whose value appears as the primary label in the interactive tooltip when hovering over a state.  

hover_data={"Confirmed": True, "Recovered": True, "Active": True}: Specifies additional columns to display in the hover tooltip alongside the primary label.   

color_continuous_scale="Reds": The colour palette applied to the fill.   

title: Sets the figure title to "COVID-19 Confirmed Cases by Indian State".  

labels={"Confirmed": "Confirmed Cases"}: Renames the colour bar label for clarity.   

The full dataset is filtered using boolean indexing to keep only rows where Country/Region equals "India", producing a dedicated india DataFrame. Province-level exploration is then performed: nunique() counts how many distinct state names appear in the Province/State column, and unique() lists all of those state names as recorded in the dataset.

<img width="1807" height="592" alt="image" src="https://github.com/user-attachments/assets/1f8d275d-989a-4407-807c-89f0ac344a44" />



### Key pandas Commands Used:

pd.read_csv(): Loads a CSV file into a DataFrame.

data.head(n): Displays the first n rows (default 5).

data.drop(): Removes specified rows or columns.

data.info(): Displays column names, dtypes, and null counts.

col.astype(): Converts a column to a specified data type.

col.max(): Returns the maximum value in a column.

data[condition]: Filters rows using a boolean condition.

col.value_counts(): Counts occurrences of each unique value.

col.nunique(): Returns the count of distinct values.

col.unique(): Returns an array of distinct values.

data.groupby(): Groups data by a column for aggregation.

sum(): Sums values within each group.

reset_index(): Moves the group key back to a regular column.

sort_values(): Sorts rows by one or more columns.

col.fillna(): Replaces missing NaN values with a given value.

data.iloc[]: Accesses rows by integer position.

col.values[0]: Extracts the first value as a Python scalar.

data.shape: Returns a (rows, columns) tuple.

df.copy(): Creates an independent copy of a DataFrame.

### Plotly Express Commands Used:

px.choropleth(): Creates an interactive choropleth map.

locations=: Column containing geographic identifiers.

locationmode="country names": Matches strings to built-in country boundaries.

geojson=: Custom GeoJSON for sub-national boundaries.

featureidkey=: Path in GeoJSON properties to match locations.

color=: Column mapped to fill colour.

color_continuous_scale=: Named colour palette for the fill gradient.

range_color=: Fixes the minimum and maximum of the colour scale.

hover_name=: Primary label shown in the interactive tooltip.

hover_data=: Additional columns shown in the tooltip.

fig.update_geos(): Configures map zoom, fit, and base layer visibility.

fig.update_layout(): Sets title, margins, and colour bar appearance.

fig.show(): Renders and displays the final interactive figure.


5. Conclusion

This experiment successfully demonstrates the power of Python for handling large-scale datasets (300,000+ rows). By cleaning the data and standardizing types, we were able to transform raw observational logs into actionable insights.

Geospatial visualization provided a clear picture of the pandemic's global footprint, while Feature Engineering (Active cases) allowed for a deeper understanding of the pandemic beyond just cumulative totals. The analysis concludes that while total confirmed cases provide the scale of the pandemic, active case counts and recovery rates are more indicative of the current healthcare status of a region.
