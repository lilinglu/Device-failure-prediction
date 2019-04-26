# Device-failure-prediction
Liling Lu
Aprirl 20, 2019
## Overview
* This document has done some EDA and Data Engineering things based on the given csv data set and finnally built some high performance models.
* Some of the most import steps are: 1 dealing with imbalanced dataset. 2 exploration on the feature 'date'. 3 some devices are removed and then put back to use at different time period. 4 oversampling should be done before or within cross validation?
## project background
* Company has a fleet of devices transmitting daily aggregated telemetry attributes.Predictive maintenance techniques are designed to help determine the condition of in-service  equipment in order to predict when maintenance should be performed. This approach promises cost savings over routine or time-based preventive  maintenance, because tasks are performed only when warranted.
## Exploratory Data Analysis

![WeChat18b25b902e804c5765dc34bf1a476bd8](https://user-images.githubusercontent.com/40584525/56835120-2ded0780-6828-11e9-9a7a-1cb0aba4d1b3.png)
![WeChatf462cae8f8f9172e5f1b5de73c87be61](https://user-images.githubusercontent.com/40584525/56835125-30e7f800-6828-11e9-938c-471d42a15a4c.png)
* This dataset has 124494 rows and no missing values. All attributes are integer data type.
* It is imbalanced data set, as the failuer class is about 0.1% of unfailure class.Here oversampling approach is used to deal with imbalanced dataset.
* Some attributes have limited number of distictive values, very sparse, indicating that they are likely to be categorical variable, such as attibute 3, 5,7,9.
* Attribute7 and 8 seems like exactly same to each other, we can drop one of them.
* Attribute 2,3,4,7,9 are highly skewed.
* Attributes differ in their magnitudes. Scaling or centering is requried.
![WeChat4bfdb29bd5291137c9b8812f27227d45](https://user-images.githubusercontent.com/40584525/56835547-60e3cb00-6829-11e9-832c-cf98064e35af.png)
* As we can see that the  number of devices decreases as time goes on. And we have noticed there is a big jump in the middle. That maybe some devices get back again after failed first.

![WeChata43ff6dbc2273260633e7427903f4a50](https://user-images.githubusercontent.com/40584525/56835753-f54e2d80-6829-11e9-96c3-c38372360f36.png)
* For those devices get back again after failure, they failure date are different from their 'max date'
