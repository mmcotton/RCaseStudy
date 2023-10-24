# Fitness Tracker Data Case Study Using R

## Description
Bellabeat is wellness technology company focused on health and fitness related products for women. The purpose of this analysis is to find trends in usage of fitness/wellness trackers from other companies to help Bellabeat drive marketing initiatives for its signature wearable, Leaf, and its corresponding app.

In this case study I will be following the preparation, cleaning, analysis, and visualization steps of the data analysis process, to ultimately make strategy and growth recommendations for Bellabeat's marketing team.

## Languages and Utilities Used
- R
- Posit Studio Cloud
- Kaggle notebook

## The data

The data in the FitBit dataset is third-party, collected via Amazon Mechanical Turk and stored in CSV files. Some of the data is organized in wide format, and some is organized in long format. I will be focusing primarily on the daily metric datasets, which are in wide format. 

The data is in the public domain. Consent was obtained to collect the data, and it has already been anonymized. The dataset was downloaded from Kaggle for free and is available to everyone.

Ideally, first-party data collected from a larger sample size would be used to increase reliability and reduce bias. The ideal dataset would also include users of other major fitness tracking devices, such as the Apple Watch and Oura Ring. 

### Potential Issues

There are several issues with the data that reduce its integrity and indicate bias:
1. This data only represents the stats of FitBit users, and the sample size is only 30 participants.
2. The data is third-party, collected via Amazon Mechanical Turk, thus its reliability cannot be verified.
3. Different types of FitBit devices were used, and individual’s recording and reporting habits can influence the data available.
4. The data has not been updated for three years
    
Ideally, first-party data collected from a larger sample size would be used to increase reliability and reduce bias. The ideal dataset would also include users of other major fitness tracking devices, such as the Apple Watch and Oura Ring. 

However, for the purposes of this case study, I will treat the dataset as though its is good and complete.

## Preparing the data for analysis

First I loaded the relevant packages and imported the datasets for daily calories, steps, intensities, and sleep.   

![A9F39A34-30FB-47B3-983C-5B42C5D6E0D5](https://github.com/mmcotton/RCaseStudy/assets/148889213/235c44dc-dedd-405c-8ecd-752c6cb6b4a5)

After using the `head()` function to get a preview of each dataset and ensure it was imported correctly, I checked the structure of the dataframes.

![BC2C9239-5034-43BE-8185-C142103B8A3A](https://github.com/mmcotton/RCaseStudy/assets/148889213/0a84a79d-79cc-497d-85fe-979422df57a8)

Then I verified the number of participants in each dataset.

![008CC0A8-F4AF-4557-B3B9-46FA8B634235](https://github.com/mmcotton/RCaseStudy/assets/148889213/319e424e-ca7b-4763-9734-41cd7a9618ad)

I used the `summarize` function to retrieve the minimum, maxium, and average values from the daily calories and steps dataset.

![BCB1A1CD-F497-4635-A20F-44F167F3CCE8](https://github.com/mmcotton/RCaseStudy/assets/148889213/0ccafad3-e218-4fe3-b341-089e1fdd9aef)

I noticed the minimum values for both datasets were zero, and decided to investigate if both zero steps and zero calories were recorded the same number of times. If so, this would suggest that the tracker was not worn by an individual on certain days.

![D189B3E5-FAA5-43DC-BCE3-F79E434D21B9](https://github.com/mmcotton/RCaseStudy/assets/148889213/a9e6ab36-94b2-420c-9842-ffd6007eb7e8)

The result indicates that zero steps and zero calories were not recorded the same number of times, thus not only on the same days. I decided to merge the two dataframes for easier analysis, while excluding any day where zero calories OR zero steps were recorded to avoid including data that might be incorrect.

![7FBDC6BC-A1D4-4B89-A4C3-4D650D2AAF1D](https://github.com/mmcotton/RCaseStudy/assets/148889213/10c3b004-b944-4561-8c09-ef4051717b09)

Next up was the daily intensities dataset. For a quick statisitcal summary of the dataset, I ran the following code.

![11CB80D7-B5EA-47C8-96ED-B485CDE0BF54](https://github.com/mmcotton/RCaseStudy/assets/148889213/b370979e-b113-40d5-aafe-b7b576c4d35b)

For a high-level analysis, I decided to focus on total active minutes versus sendentary minutes. I ran the following code to create a new column with the sum of light, fairly, and very active minutes, then create a new dataframe with this information.

![079C740B-5FA3-426E-ADE7-40312A10631A](https://github.com/mmcotton/RCaseStudy/assets/148889213/41f97e54-162c-447d-9fe2-0fcf2b7f4cd1)

To make visualizing the relationships easier in the future, I merged the daily calorie, steps, and intensity data. 

![A21BC2C9-4B9F-4580-8631-D12D709E16B3](https://github.com/mmcotton/RCaseStudy/assets/148889213/0a810612-5574-4a48-a554-88b3977234df)

Before continuing on, I realized that the data in the ActivityDay column should be converted to date format. To do so, I ran the following code.

![35EEAE10-9579-41F1-BF77-8EE37CEFA70E](https://github.com/mmcotton/RCaseStudy/assets/148889213/eae7c1ec-e1b0-447c-b102-f1377ea388ed)

Before continuing on to analysis, I decided to include the sleep data as well. There are less participants in the sleep dataset than in the other three, but I still wanted to include this data in my merged dataframe, to more easily examine the relationship between sleep and activity.

First, I needed to fix the SleepDay column so the data is in the correct date format.

![E37635E4-F0F1-47B1-9A5D-5A41D05A4BB1](https://github.com/mmcotton/RCaseStudy/assets/148889213/5c6b7bcb-fa76-452b-96e7-92ea2638e442)

Now that the sleep dataframe has been cleaned, I merged it with the `daily_activity` dateframe. I used a `left_join` so all the data from `daily_activity` was retained. 

![BCB92AD4-1FFC-47E7-BF2C-B2AC1F1BE009](https://github.com/mmcotton/RCaseStudy/assets/148889213/2d17fa02-1f4d-4750-b3c1-adddacd45a50)

## Analysis 

Now that the data has been cleaned and merged, it is time for the analysis phase. Since I was looking for relationships between variables in the data, I decided to visualize the data using the `ggplot2` package from the `tidyverse`, which I loaded earlier.

![E5A1186B-F67C-4F11-8116-60385BEED050](https://github.com/mmcotton/RCaseStudy/assets/148889213/c19c0a51-565e-48c5-a060-534ca15a8211)

The scatterplot above demonstrates a positive correlation between steps taken and calories burned. This is, of course, something to be expected, and not a very useful takeaway for our business task.

Next, I examined the relationship between active minutes and steps taken:

![A2B48D8D-BB55-4D02-954D-29DB1F05A3BD](https://github.com/mmcotton/RCaseStudy/assets/148889213/d88a55b6-a4e2-423c-8968-7395b94e5e8e)

The positive correlation here is also expected. More steps taken equates to more minutes of activity. To possibly find some less expected trends, I moved on to exploring the relationship between activity and sleep.

To reduce the impact of day-to-day variability on the visualizations, and to focus more on trends over time, I ran the following code to calculate each participant's average activity versus average sleep, then create a visualization.

![83C83BF7-F104-4F41-B05F-0DFF6625CD43](https://github.com/mmcotton/RCaseStudy/assets/148889213/8f7e45e6-a0d1-4221-940e-5d6ab3d56315)

![45E0BCFB-17F1-45FE-9CA7-1DCC7C42E182](https://github.com/mmcotton/RCaseStudy/assets/148889213/0da2c424-a5d0-4fa7-9f55-057c9dec42c5)

We can see that there is not a very strong correlation between activity and sleep. Next, I explored the relationship between sedentary time and sleep using similar code:

![058CC62B-963C-44D4-82B2-649E31899F43](https://github.com/mmcotton/RCaseStudy/assets/148889213/cb18de0d-612a-4554-9e0f-b675019dfeb7)

![AC76331C-7035-42B7-ACD0-2B23093EF503](https://github.com/mmcotton/RCaseStudy/assets/148889213/157e567f-d94b-4ffd-9f54-88d92ae88841)

We can see a clear negative correlation between an individual's sedentary time and minutes asleep. I was surprised to see that active time didn't have as strong a relationship with sleep as increased sedentary time. This is something unexpected that Bellabeat's marketing team could puruse further.

Lastly, I ran the following code to investigate and visualize any trends in average activity over time.

![F43F292A-9FAC-47EC-8675-600725DB2485](https://github.com/mmcotton/RCaseStudy/assets/148889213/edb140ea-aa82-46ec-9c95-b9588fc3ed28)

No strong patterns jump out, but activity levels seem generally higher at the middle and end of April, and the beginning of May.

## Suggestions for Bellabeat

Given the trends in the data, I recommend Bellabeat implement the following strategies:

1. Run a campaign bringing awareness to the impact of sedentary time on sleep, and how even very minor activity, like standing as opposed to sitting, can improve users' sleep, even if they're not necessarily moving very much. 

2. Enable notifications within the app that reminds users to stand up and move, even just a little, after the Leaf detects they have been sedentary for a certain length of time.

3. Implement customzied reports at the beginning of each month highlighting users 30-day activity levels, encouraring them to carry momentum from the previous month's end into the new month when applicable. 

### Addressing Limitations of the Data

If I was given this dataset as an analyst, I would recommend to the stakeholders that Bellabeat collect its own data if possible, or obtain second-party data from a reliable source. I would also recommend they target a much higher sample size that is reprensentative of the fitness wearable-user population as a whole, and data that was gathered over a period of at least twelve months. 






