# Predicting Car Accident Severity




## Introduction/Business Problem

This project will involve working on a case study where we will predict car accident severity. The stakeholders will be businesses that have employees that drive cars for their business operations. The reason why this matters for the stakeholders is because it's important for employee safety and the safety of others, and reduces liability as well as monetary loss for the company. For example, if employees are delivering cross country, ridesharing, delivering packages, or any other activity that requires driving, they would want to know the risk that their employees are going to a severe accident. A severe accident, meaning bodily injury or fatality to themselves or others. This is important because if there are severe accident prone conditions, then the stakeholder may want their employee to cease operations or re-route them depending on how severe a potential car accident can be. 


## Data

### Data Description

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


### How Data Will Be Used To Solve the Problem

We will use the severity description (*Injury Collision* or *Property Damage Only Collision*) to determine the accident severity. For this study, *Property Damage Only Collision* is less severe than an *Injury Collision*. We want to build a model to find out which combination of conditions might lead to one of these two cases. The feature sets of this dataset are listed above and will determine what combinations of these features are more likely to lead to a *Injury Collision* or *Property Damage Only Collision*.


