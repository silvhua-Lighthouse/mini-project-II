# Miniproject 2

### [Assignment](assignment.md)
** Please note that I moved the notebook into the "data" directory for ease of running scripts.

## Project/Goals
Part 1:
* Get a list of all coworking spaces near Granville Skytrain Station to assist with selecting one based on reviews.
* Compare the quality of search results from Yelp vs. Foursquare.
* Consolidate search results so that one can see information from both from Yelp and Foursquare at the same time.

Part 2
* Get a ranked list of Ethiopian restaurants near Main Street Skytrain Station to help decide which restaurant to try.
## Process
### Requesting data from APIs
* Exploratory search on Google maps and Yelp.ca to know if there would be enough results.
* Looked at API documentation to determine how to create the right endpoints, parameters, and authentication methods.
* Endpoints used:
    * Yelp `/businesses/search`
    * Foursquare `/places/search`
* Parameters used:
    * Latitude and longitude
    * Part 1: 
        * 'coworking' search term in Yelp and Foursquare
        * Foursquare does not provide ratings in their core results, but this can be obtained by including the `fields=rating` paramter. I did a second search with this parameter after looking at the results from the initial search.
    * Part 2: 'Ethiopian' search term in Yelp

### Looking at the API data
* Visually inspected the text files and explored the JSON files in Jupyter Notebook to see what data was provided and how it was structured.

### Parsing the data
* Creating dataframes with the desired columns.

### Analysis
#### Part 1: Comparing Yelp vs. Foursquare
* Compared results from Yelp and Foursquare based on:
    * Number of businesses found
    * Quantity of ratings.
* Joined on address
    Used `df.merge()`, with `how='outer'`, I merged the dataframes from Yelp and Foursquare using:
    1. Address. This did not work due to formatting differences, e.g. "Street" vs. "St", "West" vs. "W", even within Yelp itself.
    2. Latitude. This is not useful because the businesses are too close to each other.

#### Parts 1 & 2: Plotted data 
Average rating vs. review count.
Large disparities in number of ratings (heterogeneity of variance!) means that just looking at number of ratings isn't representative of reality.

## Results
### Yelp vs. Foursquare
Site | Number of records | Attributes
--- | --- | -
Yelp | 20 results | 24: ['id', 'alias', 'name', 'image_url', 'is_closed', 'url', 'review_count', 'categories', 'rating', 'transactions', 'phone', 'display_phone', 'distance', 'coordinates.latitude', 'coordinates.longitude','location.address1', 'location.address2', 'location.address3','location.city', 'location.zip_code', 'location.country','location.state', 'location.display_address']
Foursquare | 10 results without ratings; 0 results with ratings | 10: ['fsq_id', 'categories', 'chains', 'distance', 'geocodes', 'link','location', 'name', 'related_places', 'timezone']

 Yelp has better coverage of coworking spaces as it provided more results. It also has more reviews, which is important.

![anotated dataframe](/projects/mini-project-II/images/dfCoworking_anotated.png)

I was unable to consolidate results from both Yelp and Foursquare because of inconsistencies with address formatting and multiple branches. If the databases adopted a universal unique business identifier such as GST number, that would make things easier (though GST number may not help if a company has a single GST number for multiple branches).

### Top Coworking Spaces
![image](/projects/mini-project-II/images/coworking-ratings.png)

### Top Ethiopian Restaurants
![image](/projects/mini-project-II/images/Ethiopian-rest.png)


## Challenges 
* Difficulty with coding.
* Difficulty finding a primary key on which to merge business information from the two sources.

## Future Goals
If I had more time, I would also:
* Get the hours of each coworking space. I would want access on weekends and evenings. Normally, after-hours access, if available, requires a higher membership fee.
* Get written reviews for each coworking space through Yelp.

## What I learned
* Look for more efficient ways to code.