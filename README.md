# Travel Recommendation System [TRS]
Repository here, explains the working of Travel Recommendation System (TRS), which aims to provide personalized recommendations to every user. TRS employs a subjective preference algorithm, in conjunction with the objective preference used in the commonly used recommendation systems, to provide travel suggestions more curated towards the individual user.

## Drawbacks of currently existing systems
- Focus is primarily on the objective constraints, i.e., Budget, time of travel, duration of travel.
- Subjective preference is compromised for the ease of use.
- Travel suggestions are not actually personalized, rather dependent on similarity between multiple users.
- Require immense user database to provide any meaningful recommendation.


## Proposed System
Starting with the awareness set, i.e., all the destination spots present in the database, the system will narrow it down to the final recommendation. Available-awareness set, the places user can visit based on objective constraints, will be obtained in the first step. Further applying the subjective constraints, relevant set, the places user want to visit, will be obtained. The final step is to compare the destination spots present in the relevant set and recommend the most suitable ones to the user.

<p align = "centre">
<img src = "https://github.com/SuyashGoylit/TravelRecommendationSystem/blob/main/Images/Proposed%20System.JPG">
</p>


## Working
The entire system has numerous modules working in conjunction to perform the required task. The basic idea is to scrape the information of tourist places from the web, classify and organize it into a database. Then, obtain the user preference, based on which the destinations from the database are suggested. To further understand the working process of the system, let's discuss the aforementioned modules in detail.

### Scraping 
The first step was to gather the data and organize it in the form of a database. Python package *Beautiful Soup* was utilized to perform the text scraping. The focus was on gathering data about three aspects: the destination itself, places to visit at the destination, and hotels at the tourist place. Following data was scraped for the destination itself;
- Place
- State
- Rating
- Ideal time to visit
- Ideal duration to visit
- Nearest airport
- Budget
- Main attraction
- Description
- Top places to visit

Scraping on the other two fronts was much less detailed, with each of them consisting of only four attributes.

For image scraping, shutil module came in very handy.

### Classification
The next step in the process was to classify this data. For the same, transfer learning on fine-tuned BERT model was utilized.The data was classified into across four parameters (discussed later in Subjective preference module). 

### Objective preference analysis module
This is a pretty standard module for any travel recommendation system. The objective of this module is to obtain the inputs for objective constraints from the user. Here, the objective constraints are:
- Budget, taken in as an integer value. 
- Duration of travel, taken in as an integer value. 
- Time of travel, divided into two parts: time of beginning and time of ending, both selected as the name of the month from the drop-down list.

Following is a screenshot of sample inputs for objective constraint evaluation.

<p align = "center">
<img src = "https://github.com/SuyashGoylit/TravelRecommendationSystem/blob/main/Images/Objective%20Analysis.jpg">
</p>

### Subjective preference analysis module
This is the novel module that is at the core of our project. The objective of this module is to obtain inputs for the subjective constraints from the user. The inputs corresponding to every parameter within this module is two folds: 
- First, a binary input that makes the user choose between two option based on the given question.  
- And second, taking the input corresponding to the importance of the question. 

These two inputs taken in for four parameters: 
- Religious interest (religious / non-religious)
- Type of traveler (conventional / adventurous)
- State of destination (noisy / serene)
- Type of destination (artificial fun / natural beauty)

These preferences makes up the subjective preference analysis module.

Following is a screenshot of sample inputs for subjective evaluation.

<p align = "center">
<img src = "https://github.com/SuyashGoylit/TravelRecommendationSystem/blob/main/Images/Subjective%20Analysis.jpg">
</p>

### Algorithm
The final step is to match the user preference gathered by the objective and subjective preference analysis modules with the pre-classified database to come up with fine tuned personalized suggestion. The inputs from the objective side of things can be handled very easily, as they are used to weed out the destinations from the database that doesn't fall under the chosen preferences. Dealing with the subjective preferences can be a little tricky, and this where the algorithm does its job. The basic idea of the algorithm is that inputs taken from the user are divided into two values (-1 and 1) for each parameter. Same is done with the parameters in the database. To come up with the best suggestion, value of destination and user preference are multiplied for each parameter, and then all these individual values are summed up. The destination with highest numeric value is suggested to the user.

### Output
Based on the user inputs for objective and subjective analysis parameters, the algorithm recommends the best three destinations for the user.

<p align = "center">
<img src = "https://github.com/SuyashGoylit/TravelRecommendationSystem/blob/main/Images/Sample%20Output.jpg">
</p>

## Future Scope
Although I have successfully achieved what I set out to do, there's always minor tweaks that can be made to futher improve the project. Here are few of them I can see in the near future:
- The most obvious one is adding more places to the database.
- Adding more parameters for subjective preference analysis.
- Instead of taking binary inputs from the user, taking preference in form of a description of the destination they want to visit.
