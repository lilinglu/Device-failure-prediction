# Device-failure-prediction
Liling Lu
April 20, 2019
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

![WeChat86a1951cc2f1259bab19346c19aa7e1c](https://user-images.githubusercontent.com/40584525/56835953-81f8eb80-682a-11e9-9998-9cb5e3a6ac17.png)

* For those devices get back again after failure, they failure date are different from their 'max date'

![WeChat18f5d9cd268981f4cef9df3bf283f909](https://user-images.githubusercontent.com/40584525/56836286-a1dcdf00-682b-11e9-964c-4adee3267e07.png)

* As for attribute 3,4,5,7,9, most of their values are vero, to change them to catagorical features may make more sense.

## Oversampling
* Mean while, I've tried two ways to do oversampling. If I upsample a dataset before splitting it into a train and validation set, I could end up with the same observation in both datasets. As a result, a complex enough model will be able to perfectly prdict the value for those observations when prediction on the validation set, inflating the metrix.
* The results turn out that we should upsamplint within the cross validation, which means we just oversample the data set used to train the model. For the validation set, it is still unseen.
![WeChat0f41fef78358121010eaf33e3be0a696](https://user-images.githubusercontent.com/40584525/56836325-bf11ad80-682b-11e9-82e2-c7285d6beeef.png)
* Here I drewed the ROC curve for the top 4 models I generated above.
 
 ## Deployment
![WeChatd008517b5a41192a946e6f51c6b15f17](https://user-images.githubusercontent.com/40584525/56856573-813b8480-6912-11e9-8056-ebe49627a9cf.png)

* The results are pretty good, which means the fitted model has very good generalization ability.
## Conclution
* So far, we've built a very good model after doing such works. But I think we still have much more things to do. One thing is doing more data engineering things. Second is try to use other classification models, for example neural network.
