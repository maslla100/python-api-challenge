
# City Weather and Hotel Finder

## Project Overview

This project analyzes city weather data and identifies suitable cities based on user-defined weather criteria. It then finds hotels in those cities using the Geoapify API and visualizes the data on an interactive map using Bokeh.

## Table of Contents

- [Installation](#installation)
- [Usage](#usage)
- [Data](#data)
- [Visualization](#visualization)
- [API Usage](#api-usage)
- [Contributing](#contributing)
- [License](#license)

## Installation

To get started with this project, clone the repository and install the necessary dependencies.

```bash
git clone https://github.com/maslla100/python-api-challenge
cd city-weather-hotel-finder
pip install -r requirements.txt
```

## Usage

1. **Data Preparation**: Prepare your city weather data and save it in a CSV file named `cities.csv` under the `output_data` directory.
2. **API Key**: Ensure you have your Geoapify API key stored in a file named `api_keys.py` with the variable `geoapify_key`.
3. **Run the Notebook**: Execute the Jupyter notebook to perform the analysis and visualization.

## Data

The `cities.csv` file should contain the following columns:
- `City`: The name of the city.
- `Country`: The country where the city is located.
- `Lat`: Latitude of the city.
- `Lng`: Longitude of the city.
- `Humidity`: Humidity level in the city.

## Visualization

The project uses Bokeh to create an interactive map that visualizes the city data along with nearby hotels. The map includes:
- A scatter plot of cities colored by city name.
- An interactive legend to filter cities by name.
- Hover tooltips to display city, country, humidity, and hotel name.

## API Usage

This project uses the Geoapify API to find hotels in the selected cities. The following parameters are used in the API call:
- `categories`: Specifies the type of places to search for (e.g., "accommodation.hotel").
- `filter`: Specifies the geographical area to search within.
- `bias`: Specifies the center point of the search.

Example code to call the Geoapify API:

```python
import requests

radius = 10000
params = {
    "categories": "accommodation.hotel",
    "apiKey": geoapify_key
}

for index, row in hotel_df.iterrows():
    lat = row['Lat']
    lng = row['Lng']
    params["filter"] = f"circle:{lng},{lat},{radius}"
    params["bias"] = f"proximity:{lng},{lat}"
    
    base_url = "https://api.geoapify.com/v2/places"
    response = requests.get(base_url, params=params)
    name_address = response.json()

    try:
        hotel_df.loc[index, 'Hotel Name'] = name_address['features'][0]['properties']['name']
    except (KeyError, IndexError):
        hotel_df.loc[index, 'Hotel Name'] = "No hotel found"
```

## Contributing

Contributions are welcome! Please create a pull request or open an issue to discuss your ideas.

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.


