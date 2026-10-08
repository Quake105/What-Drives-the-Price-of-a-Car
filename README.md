What Drives Used Car Prices?

This project is a dive into used car data to find out exactly what impacts the price on vehicle valuation. It follows the classic CRISPDM framework to turning data into actionable insights for a dealership to help determine what car features to prioritize. 

The Goal    - Business Understanding 

A used car dealership needs to know which vehicle features actually drive value so they can make smart inventory choices. To figure this out, I treated the assignment as a supervised regression problem. Because car prices are heavily skewed toward the high end, I used log of price    as my target variable. This let me use model coefficients to isolate how much each specific feature increases or decreases a car's worth. 

The data set used is a Kaggle data containing 427K listings. Real world data can be messy so did some cleaning to get quality results. 

1. Duplicate listings were dropped 

2. Filtered out $0 prices, and other obvious errors and extreme outliers. 

3. Removed vehicles with impossible odometer readings. 

4. Capped the age of cars made after 1995. 

This left me with a data set of 237K listings. 

# Modeling 

I evaluated three different algorithms against a simple baseline model, using a 5- fold cross-validation grid search to fine-tune the parameters specifically testing polynomial degrees for age and mileage. 

While I tracked RMSE on log price to optimize the math, I also calculated the Mean Absolute Error (MAE) in actual dollars to make the results clear and useful for business understanding. 

Model - Test RMSE(log) - R^2 - MAE ($) Baseline - 0.855 - 0.000 - $10,655 Linear Regression - 0.0407 - 0.774 - $4,480 Ridge Regression (alpha=0.1, degree 3) - 0.399 - 0.783 - $4,417 Lasso Regression (alpha = 0.0001, degree 3) - 0.399 - 0.783 - $4,404 

# Findings 

By looking at the model coefficients and holding other variables constant, a few clear pricing patterns stand out: 

Age and mileage: drag prices down the fastest, losing about 7% per year of age and 4% for every 10,000 miles added. 

Power: Engine type matters, diesel vehicles command a 90% premium over standard gas cars, and 8-cylinder engines command roughly 50% more than 4- cylinders. 

Capability/Terrain options: 4WD capability adds about 29% to a vehicle's value compared to FWD, while trucks and pickups outpace standard sedans by about 38%. 

Title: A salvage or rebuilt title immediately slashes a car's value by 20–30%. If the title is missing entirely or marked as "parts-only", expect the value to cut in half. Brand Premium: Compared to a baseline brand like Ford, Toyotas +19% and Lexuses +40% hold their value incredibly well. On the flip side, brands like Kia, Nissan, Hyundai, Chrysler, and Mitsubishi lag behind, tracking 16–23% lower. Paint Color: Surprisingly, the exterior color had almost zero statistical impact on the final price. 

# Recommendations 

Prioritize newer, lower-mileage cars. Value drops fastest in the first few years; a 3-year-old car lists for about 34K on median vs 15K for a 6-10 year old one Stock trucks, pickups, 4WD and diesel vehicles. They hold value much better and customers pay a clear premium. 

Avoid or buy very cheaply bsalvage, rebuilt or missing-title cars. The title alone takes 20-50% off the resale value. 

Brand matters. Toyota and Lexus hold value much better than Ford at the same age/miles; Nissan, Kia, Hyundai, Chrysler and Mitsubishi sell for noticeably less, so what you pay for them at acquisition needs to reflect that. 

Don't worry about color. Paint color has very little effect on price, so don't pay extra for a particular color. 

# Next Steps 

Add the car model/trim (needs text cleaning) - probably the biggest missing piece. Use actual sale prices from the dealership instead of listing prices. Try non-linear models (e.g. random forest / gradient boosting) for better price 

predictions. Build a simple pricing tool from the model so staff can get a quick estimate when appraising trade-ins. 

Repo Structure 

README Car Price Assignment.pynb data/vehicle.csv.zip 

