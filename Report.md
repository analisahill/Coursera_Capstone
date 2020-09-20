# Predicting Car Accident Severity 


## 1. Introduction/Business Problem

This project will involve working on a case study where we will predict car accident severity given that we have information about an accident that has just occurred. The stakeholders will be emergency operators, first responders, and healthcare workers. The reason why this matters for the stakeholders is because if there is an accident, then the first responders would be able to input information about the accident into a model which will give them a report telling them how probable it is that someone was injured given preliminary information that was given to them about the accident. From that information they can decide how many ambulances, firetrucks or police to dispatch based on whether there was an injury or non-injury accident. This saves time, money, resources, and can be the difference between life or death for the individuals involved in the accident.



## 2. Data

### 2.1 Data Description

Our dataset consists of collisions reported by the Seattle Police Department and recorded by traffic records from 2004 to present time. Each row represents a collision and the dataset is updated weekly according to the [metadata](https://github.com/analisahill/Coursera_Capstone/blob/master/Capstone_Metadata.pdf). 
There are several columns in each row that tell us about the accident severity. The severity code, is a code that labels the severity of the collision. The severity code can be the following:

| Accident Type      | Severity code    
| :------------- | :----------: | 
| Property Damage| 1            |
| Injury         | 2            |



The severity code will be our labels in our supervised machine learning model. The following are the features that will be used in our model.

**Feature sets**
* Severity code 
* Collision type (*Angles*, *Sideswipe*, *Parked Car*, *Other*, *Cycles*, *Rear Ended*, *Head On*, *Unknown*, *Left Turn*, *Pedestrian*, and *Right Turn*. )
* Location
* Number of pedestrians 
* Number of cyclists 
* Number of vehicles
* Number of injuries
* Number of serious injuries
* Number of fatalities
* Date of incident
* Time of incident
* Road conditions (*Wet*, *Dry*, *Unknown*, *Snow/Slush*, *Ice*, *Other*, *Sand/Mud/Dirt*, *Standing Water*, *Oil*)
* Light conditions (*Daylight*, *Dark - Street Lights On*, *Dark - No Street Lights*, *Unknown*, *Dusk*, *Dawn*, *Dark - Street Lights Off*, *Other*, *Dark - Unknown Lighting*)
* Weather (*Overcast*, *Raining*, *Clear*, *Unknown*, *Other*, *Snowing*, *Fog/Smog/Smoke*, *Sleet/Hail/Freezing Rain*, *Blowing Sand/Dirt*, *Severe Crosswind*, *Partly Cloudy*)
* Other data that is described in
[metadata](https://github.com/analisahill/Coursera_Capstone/blob/master/Capstone_Metadata.pdf)


### 2.2 How Data Will Be Used To Solve the Problem

We will use the severity description (*Injury Collision* or *Property Damage Only Collision*) to determine the accident severity. For this study, *Property Damage Only Collision* is less severe than an *Injury Collision*. We want to build a model to find out which combination of conditions might lead to one of these two cases. The feature sets of this dataset are listed above and will determine what combinations of these features are more likely to lead to a *Injury Collision* or *Property Damage Only Collision*.


### 2.3 Data Feature Selection

The final features/columns selected from the dataframe are listed below.

**Features Kept**


* SEVERITYCODE (severity code)
* ROADCOND (road condition)
* LIGHTCOND (light condition)
* VEHCOUNT (vehicle count)
* WEATHER  (weather)
* ADDRTYPE (address type) 
* COLLISIONTYPE (collision type)
* JUNCTIONTYPE (junction type)


**Features Dropped**

* X
* Y
* OBJECTID
* INCKEY
* COLDETKEY
* REPORTNO
* STATUS
* INTKEY
* LOCATION
* EXCEPTRSNCODE
* EXCEPTRSNDESC
* SEVERITYDESC
* INCDATE
* INCDTTM
* JUNCTIONTYPE
* SDOT_COLCODE
* SDOT_COLDESC
* INATTENTIONIND
* UNDERINFL
* PEDROWNOTGRNT
* SDOTCOLNUM
* ST_COLCODE 
* ST_COLDESC
* SEGLANEKEY
* CROSSWALKKEY

The the dropped data was either incomplete or involved written description of the accidents and scenarios. Perhaps some of these descriptions could be looked more closely at using NLP, but shall be left for another project. The other data would have required more data mining and monetary resources to obtain useful information for those features.

### 2.4 Data Cleaning 

There were some parts of the dataset that needed to be cleaned up. There were nan values in the following columns:

* LIGHTCOND (light condition)
* WEATHER (weather)
* ADDRTYPE (address type)
* JUNCTIONTYPE (junction type)
* COLLISIONTYPE (collision type)

Since these nan values and their rows only took up about 6% of the data, therefore, those rows were dropped. 


## 3. Exploratory Data Analysis

#### 3.1 Target Variable

Conveniently, our target was already labeled as a severity description code, but there was also a little more information that tells us about this data set. The total number of collision incidents in our dataset is 194,673. Here is a breakdown of the target:


|               | Counts| Percent of Collisions 
 :------------- | :----------: | :----------: |
|Property Damage Only Collision|136485|	70.1 
|Injury Collision|	58188|       29.9 	


<br /> 

![severitydescription_vs_counts](https://github.com/analisahill/Coursera_Capstone/blob/master/images/severitydescription_vs_counts.png?raw=true)

In the table and plot, we can see that a non-injury collision occurs ~70% of the time versus an injury collision ~30% of the time. So here we can tell that we have an unbalanced dataset, but in the future if we want to make this more balanced by finding additional datasets to join with this data.

#### 3.2 Break-down of collision types

The collision types for this dataset are labeled as: head on, right turn, unkown, cycles, pedestrian, left turn, sideswipe, other, rear ended, angles and parked car. This data shows that accidents involving parked cars occur 25.3% of the time, followed by accidents at an angle (18.3%), and then rear-ended (~18.0%). The lowest collision types were head-on (1.0%), right-turn (1.6%), and cycles (2.9%).

<br /> 


![Collision Type Histogram](https://github.com/analisahill/Coursera_Capstone/blob/master/images/collision_type_vs_counts.png?raw=true)

A key take-away is that some of the less prevalent types of collisions may be associated with injury. Since, this dataset is 30% injury and 70% non-injury, it would make sense if the larger population of accidents (non-injury) occured more with parked cars involved. 

#### 3.3 Break-down of junction types and address types

Sometimes accidents in general can be related to the location or circumstances of where they occur. That is why it's important to look at junction and address types to determine is there a certain layout of the road that leads to having more accidents.

![addresstype vs counts](https://github.com/analisahill/Coursera_Capstone/blob/master/images/addresstype_vs_counts.png?raw=true)

The data shows that 66% of the time the accident occurs on a block, then 34% at an intersection, and less than 1% in an alley. Logically this makes sense because most driving experiences are not done in alleys. It would make more sense that they happen where there are many other cars present. Looking into the junction type we broke down more about the block and intersection accidents shown below in the histogram.


![Junctiontype vs counts](https://github.com/analisahill/Coursera_Capstone/blob/master/images/junctiontype_vs_counts.png?raw=true)

From the data, it was calculated that around 48% of these accidents are mid-block and not related to intersections, which coincides with the address type data. The second prevalent is at an intersection or intersection related, which is also confirmed by the address type histogram a shown before this plot.


#### 3.4 Break-down of road conditions, weather, and light conditions

Another contributing factor to an accident besides the layout of the road is what are other conditions such as weather, light, and other road conditions. We look further into these topics and see that there are also important features in this data.

![Road conditions versus counts](https://github.com/analisahill/Coursera_Capstone/blob/master/images/roadcondition_vs_counts.png?raw=true)

Suprisingly, 66% of the accidents occured when the road was dry and 25% of the time when the road was wet. We delved into this further by looking at what the weather conditions.

![Weather versus counts](https://github.com/analisahill/Coursera_Capstone/blob/master/images/weather_vs_counts.png?raw=true)

The weather conditions also confirmed what is seen in the road conditions. It is reported that 59% of the accidents occured during clear weather and 17% occured when there was rain. The weather is a little more informative than the road condition data because it also gives the option of overcast which contributes alost 15% of the accidents. To understand this more, we can look further into the light conditions for the accidents.


![light conditions versus counts](https://github.com/analisahill/Coursera_Capstone/blob/master/images/lightcondition_vs_counts.png?raw=true)

Around 61% of the accidents happened during the day and almost 26% of the accidents happened at night with the street lamps on. So now, we can see that there is a relationship between the weather, light, and road conditions. Their top two percentage values are similar in ratio to each other, which could help separate out whether someone was injured in an accident or not. 


## 4.Methodology 

For our methodology we will use logistic regression, decision tree and random forest for our initial investigations. 

#### Logistic Regression

#### Decision Tree
![dtree](https://github.com/analisahill/Coursera_Capstone/blob/master/images/dtree_render.png?raw=true)

#### Random Forest

### Model Performance



## Conclusion

## Future Directions

